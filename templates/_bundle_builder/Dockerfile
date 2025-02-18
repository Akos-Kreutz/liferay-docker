FROM --platform=${TARGETPLATFORM} liferay/base:latest

# Common
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --yes build-essential

RUN	mkdir /build

# Ffmpeg
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --yes yasm pkg-config libx264-dev libx265-dev libvpx-dev libopus-dev libvorbis-dev libtheora-dev libfaac-dev libmp3lame-dev libass-dev libfreetype6-dev libsdl2-dev

RUN curl -L -o /build/ffmpeg.tar.gz https://ffmpeg.org/releases/ffmpeg-7.1.tar.gz && \
	cd /build && \
	tar -xvzf ffmpeg.tar.gz && \
	cd ffmpeg-* && \
	mkdir build && \
	cd build && \
	../configure --enable-gpl --enable-version3 --enable-shared --enable-nonfree --enable-libx264 --enable-libx265 --enable-libvpx --enable-libopus --enable-libvorbis --enable-libtheora --enable-libmp3lame --enable-libass --enable-libfreetype --enable-sdl2 && \
	make -j$(nproc) && \
	make install && \
	rm -rf /build/*

# Ghostscript
RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --yes libpng-dev libjpeg-dev libtiff-dev zlib1g-dev libfreetype6-dev libcups2-dev libxext-dev libx11-dev libfontconfig1-dev

RUN curl -L -o /build/ghostscript.tar.gz https://github.com/ArtifexSoftware/ghostpdl-downloads/releases/download/gs10040/ghostscript-10.04.0.tar.gz && \
	cd /build && \
	tar -xvzf ghostscript.tar.gz && \
	cd ghostscript-* && \
	./configure --prefix=/usr/local && \
	make -j$(nproc) && \
	make install && \
	rm -rf /build/*

RUN apt-get update && \
	DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get install --no-install-recommends --yes bc ffmpeg file fonts-dejavu google-perftools imagemagick gifsicle libtcnative-1 && \
	apt-get upgrade --yes && \
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