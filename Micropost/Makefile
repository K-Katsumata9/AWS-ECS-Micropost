.PHONY: test build release clean version login logout publish

export APP_VERSION ?= $(shell git rev-parse --short HEAD)

version:
	@ echo '{"Version": "$(APP_VERSION)"}'

login:
	aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin 410898520882.dkr.ecr.ap-northeast-1.amazonaws.com

logout:
	docker logout 410898520882.dkr.ecr.ap-northeast-1.amazonaws.com

build:
	docker-compose build release
	docker-compose build app

release:
	docker-compose up release
	docker-compose up --abort-on-container-exit migrate
	docker-compose up app

#追記箇所
publish:
	docker-compose push release app

clean:
	docker-compose down -v
	docker images -q -f dangling=true -f label=application=micropost | xargs -I ARGS docker rmi -f --no-prune ARGS