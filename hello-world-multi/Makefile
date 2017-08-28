.PHONY: publish

publish:
	@for MANIFEST in *.y*ml; do \
		manifest-tool \
			--username "${DOCKER_USERNAME}" \
			--password "${DOCKER_PASSWORD}" \
			push from-spec $$MANIFEST; \
	done
