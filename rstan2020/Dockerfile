FROM  rocker/r-ver:3.6.2
# See
# https://github.com/rocker-org/rocker-versioned/blob/master/VERSIONS.md
# https://github.com/jrnold/docker-stan/blob/master/rstan/Dockerfile
# jrnold installs rstan twice, maybe a typo?
# Unlike jrnold, We dont want rstudio, so build from a tagged r-ver

RUN apt-get update \
	&& apt-get install -y --no-install-recommends apt-utils ed libnlopt-dev \
            openssl libssl-dev curl libcurl4-openssl-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/



# Install rstan
RUN install2.r --error --deps TRUE \
    rstan \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

RUN mkdir -p $HOME/.R/ \
    && echo "CXXFLAGS=-O3 -mtune=native -march=native -Wno-unused-variable -Wno-unused-function -flto -ffat-lto-objects  -Wno-unused-local-typedefs -Wno-ignored-attributes -Wno-deprecated-declarations\n" >> $HOME/.R/Makevars \

RUN install2.r --error --deps TRUE \
    rstan \
	edstan \
	mass \
    && rm -rf /tmp/downloaded_packages/ /tmp/*.rds

