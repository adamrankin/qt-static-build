#
# Parameters
#

# Name of the docker executable
DOCKER = docker

# Docker organization to pull the images from
ORG = adamrankin

#
# Targets
#

all: qt-static

qt-static:
	$(DOCKER) build -t $(ORG)/qt-static:5.12.10-ubuntu-20.04 \
		--build-arg IMAGE=$(ORG)/qt-static \
		--build-arg VCS_REF=`git describe --exact-match 2> /dev/null || git rev-parse --short HEAD` \
		--build-arg VCS_URL=`git config --get remote.origin.url` \
		--build-arg BUILD_DATE=`date -u +"%Y-%m-%dT%H:%M:%SZ"` \
	.

.PHONY: all qt-static
