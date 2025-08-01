# Standard stuff

.SUFFIXES:
$(VERBOSE).SILENT:

MAKEFLAGS+= --no-builtin-rules          # Disable the built-in implicit rules.
MAKEFLAGS+= --warn-undefined-variables  # Warn when an undefined variable is referenced.

UNAME:=$(shell uname)
ifeq (${UNAME},Darwin)
CXX=g++-15
CC=g++-15
endif

CXXFLAGS=-std=c++23 -Wall -Wextra -Wpedantic -Wunused
LDFLAGS=-stdlib=libstdc++
CPPFLAGS=-I/usr/local/include

.PHONY: all clean distclean working headeronly failing format docker-build docker-run

all: working headeronly # XXX failing with cmake v3.28.3
working:
	cd module-lib && cmake --workflow --preset default --fresh && cmake --build --preset default --target install
	# XXX cd module-exe && cmake --workflow --preset default --fresh && cmake --build --preset default --target test

failing:
	TEST_FORCING_MODULE_ERROR=ON $(MAKE) working
	#XXX -run-clang-tidy -p build/module-exe

headeronly:
	cd header-lib && cmake --workflow --preset default --fresh && cmake --build --preset default --target install
	cd header-exe && cmake --workflow --preset default --fresh && cmake --build --preset default --target test
	#XXX -run-clang-tidy -p build/header-lib

docker-run:
	docker run -it -v ${PWD}:/home/workdir setup-cpp-ubuntu

docker-build:
	docker build -f .devcontainer/Dockerfile -t setup-cpp-ubuntu .

clean:
	rm -rf build stagedir

distclean:
	git clean -xdf

format:
	find . -name CMakeLists.txt -o -name '*.cmake' | xargs cmake-format -i
	git clang-format main
