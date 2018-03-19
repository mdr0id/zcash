# Makefile for ZCash 1.0.15
#

GREEN_COLOR     = \033[0;92m
BLUE_COLOR      = \033[0;36m
DGREEN_COLOR    = \033[0;32m
RED_COLOR 		= \033[0;31m
ORANGE_COLOR 	= \033[0;33m
NO_COLOR   		= \033[m

OK_STRING       = "[OK]"
ERROR_STRING    = "[ERROR]"
WARN_STRING     = "[WARNING]"
DEBUG_STING     = "[DEBUG]"
COMPILE_STRING  = "[COMPILING]"

MAKE=make
BUILD="$(./../depends/config.guess)"
HOST=$(BUILD)
CC=gcc
CXX=g++
CONFIGURE_FLAGS=""
LCOV_ARG=''
HARDENING_ARG='--enable-hardening'
TEST_ARG=''
MINING_ARG=''
RUST_ARG=''
PROTON_ARG='--enable-proton=no'
LIBS_ARG=''
PREFIX="$(pwd)/depends/$BUILD/"
CXXFLAGS= -g --enable-werror

#DEBUG FLAGS / THREAD SANITY CHECKS
#CXXFLAGS= "-g -ggdb -O0"
#CXXFLAGS= "-DDEBUG_LOCKORDER"

#DEBUG CLI PARAMS
#-debug=zrpc
#-debug=zrpcunsafe

#PLATFORMS
#i686-w64-mingw32 for Win32
#x86_64-w64-mingw32 for Win64
#x86_64-apple-darwin11 for MacOSX
#arm-linux-gnueabihf for Linux ARM

#.DEFAULT_GOAL := help

.PHONY: all
all:
#HOST=$(HOST) BUILD=$(BUILD) NO_RUST=$(RUST_ARG) NO_PROTON=$(PROTON_ARG) $(MAKE) -C ./../depends/ V=1
	HOST=x86_64-unknown-linux-gnu BUILD=x86_64-unknown-linux-gnu NO_RUST=--enable-rust=no NO_PROTON=--enable-proton=no make -j4 -C ./../depends/ V=1
	
	./../autogen.sh
	
#CC="$CC" CXX="$CXX" ./configure --prefix="${PREFIX}" --host="$HOST" --build="$BUILD" "$RUST_ARG" "$HARDENING_ARG" "$LCOV_ARG" "$TEST_ARG" "$MINING_ARG" "$PROTON_ARG" "$LIBS_ARG" $CONFIGURE_FLAGS --enable-werror CXXFLAGS='-g'
	CC=gcc CXX=g++ ./../configure --prefix=/home/marsh/zcash_dev_hub/zc_test_fresh/zcash/depends/x86_64-unknown-linux-gnu --host=x86_64-unknown-linux-gnu --build=x86_64-unknown-linux-gnu --enable-rust=no --enable-hardening '' '' '' --enable-proton=no '' --enable-werror CXXFLAGS=-g

#"$MAKE" "$@" V=1
	cd src && make -j4 V=1

zcashd:
	@echo "$(GREEN_COLOR)zcashd"	

zcash-cli:
	@echo "$(BLUE_COLOR)zcash-cli"		

zcash-tx:
	@echo "$(DGREEN_COLOR)zcash-tx"		

zcash-gtest:
	@echo "$(ORANGE)zcash-gtest"
 

.PHONY: clean
clean:
	../make clean

.PHONY: help
help:
	@echo "Usage: "
	@echo 
	@echo "$0 --help "
	@echo "  Show this help message and exit."
	@echo 
	@echo "$0 [ --enable-lcov || --disable-tests ] [ --disable-mining ] [ --disable-rust ] [ --enable-proton ] [ --disable-libs ] [ MAKEARGS... ] "
	@echo "Build Zcash and most of its transitive dependencies from "
	@echo "source. MAKEARGS are applied to both dependencies and Zcash itself. "
	@echo 
	@echo "If --enable-lcov is passed, Zcash is configured to add coverage "
	@echo "instrumentation, thus enabling to work. "
	@echo "If --disable-tests is passed instead, the Zcash tests are not built. "
	@echo 
	@echo "If --disable-mining is passed, Zcash is configured to not build any mining "
	@echo "code. It must be passed after the test arguments, if present. "
	@echo 
	@echo "If --disable-rust is passed, Zcash is configured to not build any Rust language "
	@echo "assets. It must be passed after test/mining arguments, if present. "
	@echo 
	@echo "If --enable-proton is passed, Zcash is configured to build the Apache Qpid Proton "
	@echo "library required for AMQP support. This library is not built by default. "
	@echo "It must be passed after the test/mining/Rust arguments, if present. "
	@echo 
	@echo "If --disable-libs is passed, Zcash is configured to not build any libraries like "
	@echo "	libzcashconsensus'. "
	  
