.PHONY: all env list stop clean
SHELL=/bin/bash
args = `arg="$(filter-out $@,$(MAKECMDGOALS))" && echo $${arg:-${1}}`

%:    
	@:

all:
	@echo "make env"
	@echo "    Create Nginx docker for entered environment."
	@echo "make stop"
	@echo "    Stop environment from entered console argument."
	@echo "make list"
	@echo "    List environment from entered console argument."
	@echo "make clean"
	@echo "    Stop and delete environment from entered console argument."

env:
	docker run -dt --name=$(args) -p 80:80 nginx

list:
	docker ps -a | grep $(args)

stop:
	docker stop $(args)

clean:
	docker stop $(args) && docker rm $(args)
