# Docker for Apple Swift

[Swift](https://swift.org/) is a general-purpose programming language built using a modern approach to safety, performance, and software design patterns.

```Shell
docker pull lxcid/swift:latest
```

- [`2.2-ubuntu.14.04`, `latest` (2.2/ubuntu1404/Dockerfile)](https://github.com/lxcid/docker-swift/blob/master/2.2/ubuntu1404/Dockerfile)
- [`2.2-ubuntu.15.10` (2.2/ubuntu1510/Dockerfile)](https://github.com/lxcid/docker-swift/blob/master/2.2/ubuntu1510/Dockerfile)
- [`master-ubuntu.14.04`, `master` (master/ubuntu1404/Dockerfile)](https://github.com/lxcid/docker-swift/blob/master/master/ubuntu1404/Dockerfile)

## Getting Started

#### Run Swift REPL

```Shell
# Swift REPL requires kernel capabilities thus the container have to run in privileged mode. See SR-54
docker run -it --privileged lxcid/swift
```

## FAQ

#### Fail to run `swift` with the following error: `error: failed to launch REPL process: process launch failed: 'A' packet returned an error: 8`.

Swift REPL seems to requires access to kernel capabilities that docker dropped by default. Run your container with `--privileged` will resolve this issue.

Referenced from:

- https://github.com/swiftdocker/docker-swift/issues/9#issuecomment-162172540
- https://bugs.swift.org/browse/SR-54

## Credits

- https://github.com/swiftdocker/docker-swift for figuring out the minimum dependencies needed.
