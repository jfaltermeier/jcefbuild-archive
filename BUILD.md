# Build instructions

```sh
export ARCH_DIST=linux64
export CC=clang-8
export CXX=clang++-8
export TRAVIS_BUILD_DIR=/travis
export TRAVIS_OS_NAME=linux
export JCEF_DIR="$PWD/src"
docker build --rm --tag travis-build .
docker run --volume "$PWD:$TRAVIS_BUILD_DIR" \
             --workdir "$TRAVIS_BUILD_DIR" \
             --env ARCH_DIST --env CC --env CXX --env TRAVIS_OS_NAME \
             --name travis-build --detach --tty --interactive --rm travis-build
docker exec -it travis-build bash
export ARCH_DIST=linux64
export CC=clang-8
export CXX=clang++-8
export TRAVIS_BUILD_DIR=/travis
export TRAVIS_OS_NAME=linux
export JCEF_DIR="$PWD/src"
# rm -rf src/ jdk_switcher/ && source ./prepare-build.sh && ./build.sh && cd ./packaging && ../prepare-deploy.sh $JCEF_DIR/binary_distrib && cd ..
rm -rf src/
source ./prepare-build.sh
./build.sh
cd ./packaging && ../prepare-deploy.sh $JCEF_DIR/binary_distrib
exit
docker container stop travis-build
```
