PASSWORD=somethingsomething
build:
	docker build . -t ic_rstudio	
run:
	docker run -d -p 54321:54321 -p 8787:8787 -e PASSWORD=$(PASSWORD) -e ROOT=TRUE -v `pwd`/data:/home/rstudio/data -v `pwd`/libs:/home/rstudio/libs/extra ic_rstudio 

stop:
	docker container ls | grep ic_rstudio | cut -c 1-20 | xargs docker container stop

.PHONY: run build stop
