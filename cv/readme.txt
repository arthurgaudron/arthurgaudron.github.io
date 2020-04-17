wkhtmltopdf index.html index.pdf

pandoc index.html --pdf-engine=wkhtmltopdf --css=media/kjhealy-print.css -o test.pdf

