

# Simple Distribution Problem - Tuple as a key

Another data structure can be used for the cost in the Simple Distribution Problem.

It is handy to have the same data structure for the "cost" and the decision variable "flow". Then, they can be called in the same way.

```python
farms = ["Farm1", "Farm2"]
cities = ["City1", "City2", "City3"]


cost = { "Farm1" : { "City1" : 250,
                     "City2" : 325,
                     "City3" : 445},
        "Farm2" : {  "City1" : 275,
                     "City2" : 260,
                     "City3" : 460}}

# New data structure for the cost
cost_tuple = { ("Farm1", "City1") : 250,
               ("Farm1", "City2") : 325,
               ("Farm1", "City3") : 445,
               ("Farm2", "City1") : 275,
               ("Farm2", "City2") : 260,
               ("Farm2", "City3") : 460}

#### cost[farm][city] => cost_tuple[farm, city] ####

# Objective function
obj = quicksum(flow[farm, city] * cost[farm][city] 
               for farm in farms 
               for city in cities)


# Objective function with tuple_cost
obj = quicksum(flow[farm, city] * cost_tuple[farm, city] 
               for farm in farms 
               for city in cities)
```


Even better, now the objective function can be directly declared through the addVars function.

```python
# Decision variables
flow = m.addVars(farms, cities, obj=cost_tuple, name="flow")

```

Let’s run the code !

```python
from gurobipy import *


farms = ["Farm1", "Farm2"]
cities = ["City1", "City2", "City3"]

supply = { "Farm1" : 100,
           "Farm2" : 125}

demand = { "City1" : 25,
           "City2" : 95,
           "City3" : 80}

# New data structure for the cost
#cost = { "Farm1" : { "City1" : 250,
#                    "City2" : 325,
#                    "City3" : 445},
#        "Farm2" : { "City1" : 275,
#                    "City2" : 260,
#                    "City3" : 460}}

cost_tuple = { ("Farm1", "City1") : 250,
         ("Farm1", "City2") : 325,
         ("Farm1", "City3") : 445,
         ("Farm2", "City1") : 275,
         ("Farm2", "City2") : 260,
         ("Farm2", "City3") : 460}

m = Model("transportation_pb")

# Decision variables
flow = m.addVars(farms, cities, obj=cost_tuple, name="flow")

# Supply constraint
supply_constr = m.addConstrs((flow.sum(farm, "*")
                              <= supply[farm] for farm in farms), 
                              name="supply_constraint")

# Demand constraint
demand_constr = m.addConstrs((flow.sum("*", city)
                             >= demand[city] for city in cities),
                             name="supply_constraint")

m.optimize()
```

Done !
