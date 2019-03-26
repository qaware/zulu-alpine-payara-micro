ZULU_VERSION=8u202
PAYARA_VERSION=5
PAYARA_RELEASE=191.QA1
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

docker:
	docker build --build-arg ZULU_VERSION=${ZULU_VERSION} --build-arg PAYARA_TAG=${PAYARA_TAG} --build-arg PAYARA_RELEASE=${PAYARA_RELEASE} -t zulu-alpine-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} .

tag: docker
	docker tag zulu-alpine-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-alpine-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}
	docker push qaware/zulu-alpine-payara-micro:${ZULU_VERSION}-${PAYARA_TAG}

latest: tag
	docker tag zulu-alpine-payara-micro:${ZULU_VERSION}-${PAYARA_TAG} qaware/zulu-alpine-payara-micro:latest
	docker push qaware/zulu-alpine-payara-micro:latest
