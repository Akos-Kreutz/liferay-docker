FROM --platform=${TARGETPLATFORM} liferay/base:latest

#
#  Common Start
#

RUN mkdir /build

RUN apt-get update && \
	\
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --no-install-recommends --yes build-essential ca-certificates curl libfreetype6-dev libjpeg-dev liblzma-dev libpng-dev libtiff-dev pkg-config zlib1g-dev

#
#  Common End
#

#
#  Image Magick Start
#

RUN apt-get update && \
	\
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --no-install-recommends --yes libgif-dev libltdl-dev libwebp-dev libx11-dev libxext-dev libxml2-dev

RUN curl --location --output /build/ImageMagick.tar.gz https://download.imagemagick.org/ImageMagick/download/releases/ImageMagick-7.1.1-47.tar.gz && \
	\
	cd /build && \
	\
	tar --extract --verbose --gzip --file ImageMagick.tar.gz && \
	\
	cd ImageMagick-* && \
	\
	./configure --prefix=/usr/local && \
	\
	make && \
	\
	make install && \
	\
	ldconfig /usr/local/lib && \
	\
	rm -fr /build/*

#
#  Image Magick End
#

RUN apt-get update && \
	\
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --no-install-recommends --yes bc file fonts-dejavu google-perftools gifsicle libtcnative-1 && \
	\
	apt-get upgrade --yes && \
	\
	apt-get clean

ARG LABEL_BUILD_DATE
ARG LABEL_NAME
ARG LABEL_VCS_REF
ARG LABEL_VCS_URL
ARG LABEL_VERSION
ARG TARGETPLATFORM

ENV LANG="C.UTF-8"

LABEL org.label-schema.build-date="${LABEL_BUILD_DATE}"
LABEL org.label-schema.name="${LABEL_NAME}"
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.vcs-ref="${LABEL_VCS_REF}"
LABEL org.label-schema.vcs-url="${LABEL_VCS_URL}"
LABEL org.label-schema.vendor="Liferay, Inc."
LABEL org.label-schema.version="${LABEL_VERSION}"