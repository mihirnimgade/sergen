# sergen
Automatic JSON serialization generator for C types

## Building the project

Building the `sergen` binary requires the following:

1) CMake (version 3.22.1 or higher)

* To generate the build system:

```bash
cmake -S . -B ./build
```

* To build the `sergen` binary`:

```bash
cmake --build ./build --target sergen
```

* To install the binaries to the project `bin` directory:

```bash
cmake --install ./build
```
