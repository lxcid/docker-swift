FROM ubuntu:14.04
MAINTAINER Stan Chang Khin Boon <me@lxcid.com>

ENV SWIFT_PLATFORM_NAME ubuntu
ENV SWIFT_PLATFORM_VERSION 14.04
ENV SWIFT_VERSION 2.2
ENV SWIFT_SNAPSHOT 2015-12-01-b

# Installing development dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		clang \
		cmake \
		git \
		icu-devtools \
		libbsd-dev \
		libedit-dev \
		libicu-dev \
		libncurses5-dev \
		libpython-dev \
		libsqlite3-dev \
		libxml2-dev \
		ninja-build \
		pkg-config \
		python \
		rsync \
		swig \
		uuid-dev \
	&& rm -rf /var/lib/apt/lists/*

# (Only for Ubuntu 14.04 LTS) Upgrade clang compiler for C++14 support and create a symlink
RUN apt-get update && apt-get install -y --no-install-recommends \
		clang-3.6 \
	&& rm -rf /var/lib/apt/lists/* \
	&& update-alternatives --install /usr/bin/clang clang /usr/bin/clang-3.6 100 \
	&& update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-3.6 100

ENV SWIFT_SOURCE_ROOT /usr/src/swift

RUN set -x \
	&& mkdir -p $SWIFT_SOURCE_ROOT \
	&& cd $SWIFT_SOURCE_ROOT \
	&& git clone https://github.com/apple/swift.git swift \
	&& git clone https://github.com/apple/swift-llvm.git llvm \
	&& git clone https://github.com/apple/swift-clang.git clang \
	&& git clone https://github.com/apple/swift-lldb.git lldb \
	&& git clone https://github.com/apple/swift-cmark.git cmark \
	&& git clone https://github.com/apple/swift-llbuild.git llbuild \
	&& git clone https://github.com/apple/swift-package-manager.git swiftpm \
	&& git clone https://github.com/apple/swift-corelibs-xctest.git \
	&& git clone https://github.com/apple/swift-corelibs-foundation.git \
	&& ./swift/utils/build-script --preset=buildbot_linux_$(echo $SWIFT_PLATFORM_VERSION | tr -d .) installable_package=/tmp/swift.tar.gz install_destdir=/tmp/swift-install \
	&& mkdir -p /usr/local/swift \
	&& tar -C /usr/local/swift --strip-components=1 -xzf /tmp/swift.tar.gz \
	&& rm -rf $SWIFT_SOURCE_ROOT /tmp/*

ENV PATH /usr/local/swift/bin:$PATH

CMD ["swift"]
