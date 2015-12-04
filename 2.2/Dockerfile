FROM ubuntu:14.04
MAINTAINER Stan Chang Khin Boon <me@lxcid.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		wget \
	&& rm -rf /var/lib/apt/lists/*

RUN gpg --keyserver hkp://pool.sks-keyservers.net \
        --recv-keys \
		'7463 A81A 4B2E EA1B 551F  FBCF D441 C977 412B 37AD' \
		'1BE1 E29A 084C B305 F397  D62A 9F59 7F4D 21A5 6D5F'

ENV SWIFT_VERSION 2.2
ENV SWIFT_SNAPSHOT 2015-12-01-b

# Installing development dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
		git \
		cmake \
		ninja-build \
		clang \
		uuid-dev \
		libicu-dev \
		icu-devtools \
		libbsd-dev \
		libedit-dev \
		libxml2-dev \
		libsqlite3-dev \
		swig \
		libpython-dev \
		libncurses5-dev \
		pkg-config \
	&& rm -rf /var/lib/apt/lists/*

# (Only for Ubuntu 14.04 LTS) Upgrade clang compiler for C++14 support and create a symlink
RUN apt-get update && apt-get install -y --no-install-recommends \
        clang-3.6 \
	&& rm -rf /var/lib/apt/lists/* \
	&& update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100 \
	&& update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100

RUN set -x \
	&& mkdir -p /usr/local/swift \
	&& gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys Swift \
	&& curl -fsSL "https://swift.org/builds/ubuntu1404/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT-ubuntu14.04.tar.gz" -o swift.tar.gz \
	&& curl -fsSL "https://swift.org/builds/ubuntu1404/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT/swift-$SWIFT_VERSION-SNAPSHOT-$SWIFT_SNAPSHOT-ubuntu14.04.tar.gz.sig" -o swift.tar.gz.sig \
	&& gpg --verify swift.tar.gz.sig \
	&& tar -C /usr/local/swift --strip-components=2 -xzf swift.tar.gz \
	&& rm swift.tar.gz swift.tar.gz.sig

ENV PATH /usr/local/swift/bin:$PATH

CMD ["swift"]
