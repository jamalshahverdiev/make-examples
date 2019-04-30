include make_env

NS ?= jamalshahverdiev
VERSION ?= latest

IMAGE ?= nginx
CONTAINER ?= web
CONTAINER_INSTANCE ?= default

.PHONY: build push login shell run start stop rm release

build: Dockerfile
	docker build -t $(NS)/$(IMAGE):$(VERSION) -f Dockerfile .

push: login
	docker push $(NS)/$(IMAGE):$(VERSION)
    
login: 
	cat ~/my_docker_pass.txt | docker login --username $(NS) --password-stdin

shell:
	docker run --rm --name $(CONTAINER)-$(CONTAINER_INSTANCE) -i -t $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE):$(VERSION) /bin/bash

run:
	docker run --rm --name $(CONTAINER)-$(CONTAINER_INSTANCE) $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE):$(VERSION)

start:
	docker run -d --name $(CONTAINER)-$(CONTAINER_INSTANCE) $(PORTS) $(VOLUMES) $(ENV) $(NS)/$(IMAGE):$(VERSION)

stop:
	docker stop $(CONTAINER)-$(CONTAINER_INSTANCE)

rm:
	docker rm $(CONTAINER)-$(CONTAINER_INSTANCE)

release: build
	make push -e VERSION=$(VERSION)
    
default: build
