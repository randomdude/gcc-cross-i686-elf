This will build an i686-elf-gcc toolchain. I use it to build code which runs without an OS present (ie, GRUB loads it).

The resulting image is of an Debian stretch image with the built toolchain installed and ready to go.

To use it, you can simply build and run this container, and then 'docker exec i686-elf-gcc ...' to compile.
Or, you can build your project in a container based on this one. For an example, see the 'btstestbench' project, which does this:
```
FROM randomdude/gcc-cross-i686-elf

RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get install -y grub-common

COPY ./ /root/

WORKDIR /root/
ENTRYPOINT build.sh # which invokes gcc/make for your own code
```

There's a docker image on dockerHub, so if you use that as a base, there's no need to build it yourself.

> docker pull randomdude/gcc-cross-i686-elf

This code was adapted from https://github.com/beevik/docker - almost all of the work was from that repo, so thanks to Brett Vickers for that.

