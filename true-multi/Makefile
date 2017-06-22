.PHONY: publish images build dockerfiles
IMAGE_NAME:=zambon/true

publish: build dockerfiles images
	manifest-tool push from-spec true-multi-latest.yaml

images:
	cd build/linux/amd64 && docker build -t $(IMAGE_NAME):amd64 .
	docker push $(IMAGE_NAME):amd64
	cd build/linux/ppc64le && docker build -t $(IMAGE_NAME):ppc64le .
	docker push $(IMAGE_NAME):ppc64le
	@echo "Image\t\t\tDigest"
	@docker image ls --digests --format "{{.Repository}}:{{.Tag}}\t{{.Digest}}" $(IMAGE_NAME)
	docker image prune -f

build: \
	build/linux/ppc64le/true \
	build/linux/amd64/true
	@file build/*/*/true

build/linux/ppc64le/true:
	GOOS=linux GOARCH=ppc64le go build -o $@ true.go

build/linux/amd64/true:
	GOOS=linux GOARCH=amd64 go build -o $@ true.go

dockerfiles: \
	build/linux/ppc64le/Dockerfile \
	build/linux/amd64/Dockerfile

build/linux/ppc64le/Dockerfile:
	@mkdir -p build/linux/ppc64le
	@cp Dockerfile $@

build/linux/amd64/Dockerfile:
	@mkdir -p build/linux/amd64
	@cp Dockerfile $@
