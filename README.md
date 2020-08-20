# WebAssembly System Interface Test Suite

This repository contains a runtime agnostic test suite for the WebAssembly
System Interface.

The tests are written as standalone WebAssembly command modules compiled
against a specific snapshot of the ABI.

Failure of a test is typically signaled by assertions but may also come from
post conditions specified in the test configuration which is a JSON object
contained at the top of the source code of a test case.

## Prerequisites

- Python (optional)
- Rust

## Building

To build all the tests run the following command:

```shell
cargo install cargo-wasi
cargo build --target wasm32-wasi
```

## Testing

To run a compatability check on all the tests run the following command:

```shell
python compat.py
```

## Testing on CentOS 7.6

Pull the docker image:

```shell
docker pull centos:7.6.1810
```

Prepare ssvm executable and copy to working folder.

```shell
cp <path/to/ssvm/binary> ssvm
```

Install ssvm and python 3.6 and run tests in docker:

```shell
docker run -it --rm -v $(pwd):/demo centos:7.6.1810
(docker)$ cd /demo
(docker)$ cp ssvm /bin
(docker)$ yum install -y python3
(docker)$ python3 compat.py
```
