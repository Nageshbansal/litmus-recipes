.PHONY: help
help:
	@echo ""
	@echo "Usage:-"
	@echo "\tmake all   -- [default] builds the litmus containers"
	@echo ""\

.PHONY: deps
deps: _build_check_docker

_build_check_docker:
	@echo "------------------"
	@echo "--> Check the Docker deps"
	@echo "------------------"
	@if [ $(IS_DOCKER_INSTALLED) -eq 1 ]; \
		then echo "" \
		&& echo "ERROR:\tdocker is not installed. Please install it before build." \
		&& echo "" \
		&& exit 1; \
		fi;

.PHONY: docker.buildx
docker.buildx:
	@echo "------------------------------"
	@echo "--> Setting up Builder        "
	@echo "------------------------------"
	@if ! docker buildx ls | grep -q multibuilder; then\
		docker buildx create --name multibuilder;\
		docker buildx inspect multibuilder --bootstrap;\
		docker buildx use multibuilder;\
		docker run --rm --privileged multiarch/qemu-user-static --reset -p yes;\
	fi

.PHONY: push-docker
push-docker:
    docker buildx build -f Dockerfile --progress plain --push --no-cache --platform "linux" -t "node2534534"/"server":"ci"  .


.PHONY: push-gql
push-gql:
	@echo "------------------------------"
	@echo "--> Pushing image"
	@echo "------------------------------"
	@cd graphql/server  && cp -R ../../../../chaos-operator . && docker buildx build -f Dockerfile --progress plain --push --no-cache --platform "linux" -t "node2534534"/"server":"ci"  . && rm -rf ./chaos-operator

.PHONY: push-sub
push-sub:
	@echo "------------------------------"
	@echo "--> Pushing image"
	@echo "------------------------------"
	@cd subscriber/ && cp -R ../../../chaos-operator . && docker buildx build -f Dockerfile --progress plain --push --no-cache --platform "linux" -t "node2534534"/"subscriber":"ci"  . && rm -rf ./chaos-operator

.PHONY: build-push
build-push: deps docker.buildx push-gql push-sub
