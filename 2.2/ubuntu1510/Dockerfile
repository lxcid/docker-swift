FROM ubuntu:15.10
MAINTAINER Stan Chang Khin Boon <me@lxcid.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
	&& rm -rf /var/lib/apt/lists/*

RUN gpg --keyserver hkp://pool.sks-keyservers.net \
        --recv-keys \
		'7463 A81A 4B2E EA1B 551F  FBCF D441 C977 412B 37AD' \
		'1BE1 E29A 084C B305 F397  D62A 9F59 7F4D 21A5 6D5F'

ENV SWIFT_PLATFORM_NAME ubuntu
ENV SWIFT_PLATFORM_VERSION 15.10
ENV SWIFT_VERSION 2.2
ENV SWIFT_SNAPSHOT 2015-12-01-b

RUN apt-get update && apt-get install -y --no-install-recommends \
		build-essential \
		clang \
		libicu-dev \
		libedit-dev \
		python2.7 \
		python2.7-dev \ 
	&& rm -rf /var/lib/apt/lists/*

RUN set -x \
	&& mkdir -p /usr/local/swift \
	&& gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift \
	&& curl -fsSL "https://swift.org/builds/$SWIFT_PLATFORM_NAME$(echo $SWIFT_PLATFORM_VERSION | tr -d .)/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT-$SWIFT_PLATFORM_NAME$SWIFT_PLATFORM_VERSION.tar.gz" -o swift.tar.gz \
	&& curl -fsSL "https://swift.org/builds/$SWIFT_PLATFORM_NAME$(echo $SWIFT_PLATFORM_VERSION | tr -d .)/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT-$SWIFT_PLATFORM_NAME$SWIFT_PLATFORM_VERSION.tar.gz.sig" -o swift.tar.gz.sig \
	&& gpg --verify swift.tar.gz.sig \
	&& tar -C /usr/local/swift --strip-components=2 -xzf swift.tar.gz \
	&& rm swift.tar.gz swift.tar.gz.sig

ENV PATH /usr/local/swift/bin:$PATH

CMD ["swift"]
