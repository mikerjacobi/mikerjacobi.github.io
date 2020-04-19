THEME=stackoverflow

make:
	chronic cat resume.json | jq .
	chronic docker run -p9000:9000 -v `pwd`:/data resume resume export --theme $(THEME) resume.html

serve:
	chronic cat resume.json | jq .
	chronic docker run -p9000:9000 -v `pwd`:/data resume resume export --theme $(THEME) resume.html 
	python3 -m http.server 9000

build:
	docker build -t resume .

