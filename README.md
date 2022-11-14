# cabextract
`cabextract` is Free Software for extracting **Microsoft cabinet files**, also called `.CAB` files. It is distributed under the GNU GPL license and is based on the portable LGPL `libmspack` library. 

`cabextract` is released at https://www.cabextract.org.uk/

# libmspack
`libmspack` is a library for some loosely related Microsoft compression formats: CAB, CHM, HLP, LIT, KWAJ and SZDD.

`libmspack` is released at https://www.cabextract.org.uk/libmspack/

## Dockerization
### Building
Cloning the repository (add `--depth 1` to save bandwidth)
```
git clone https://github.com/rmaksimov/libmspack
cd libmspack/libmspack
```

Building a Docker image containing statically linked (by default) binaries
```
docker build -t libmspack:latest .
```

(If there is a need to compile dynamically linked binaries, uncomment the corresponding section and comment out the section related to the statically linked binaries)

### Getting The Binary
The following steps help to copy the specific statically linked binary from the Docker container (using the `oabextract` binary file as an example)

**Linux:** Copy the `oabextract` binary with the current user as owner from the Docker container to the `bin` directory in the current directory
```
mkdir bin
docker run --rm -v "${PWD}/bin:/opt/bin" -w /opt/libmspack/examples --entrypoint sh libmspack:latest -c "chown $(id -u):$(id -g) oabextract && cp -p oabextract /opt/bin"
```

**Windows:** Copy the `oabextract` binary from the Docker container to the `bin` directory in the current directory
```
mkdir bin
docker run --rm -v "%cd%/bin:/opt/bin" -w /opt/libmspack/examples --entrypoint sh libmspack:latest -c "cp oabextract /opt/bin"
```

### Running The Binary From a Container
Running the `oabextract` binary inside a Docker container based on the image
```
docker run --rm -v "${PWD}/data:/opt/data" -w /opt/data --entrypoint /opt/libmspack/examples/oabextract libmspack:latest {INPUT}.lzx {OUTPUT}
```

In case of Windows replace `${PWD}` with `%cd%`