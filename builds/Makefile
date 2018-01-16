.PHONY : build clean

.DEFAULT_GOAL := build

SANDBOXING_NACL_DIR=$(shell realpath ../../Sandboxing_NaCl)
ZLIB_DIR=$(shell realpath ../../zlib_nacl)
NACL_CLANG32=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/i686-nacl-clang
NACL_CLANG64=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/x86_64-nacl-clang
NACL_LIBM32=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32/libm.a
NACL_LIBM64=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib/libm.a

x32/non_nacl_build:
	-mkdir -p ./x32/non_nacl_build
	cd ./x32/non_nacl_build && cmake -D CMAKE_C_COMPILER=clang -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x32/non_nacl_build -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x32/non_nacl_build

x64/non_nacl_build:
	-mkdir -p ./x64/non_nacl_build
	cd ./x64/non_nacl_build && cmake -D CMAKE_C_COMPILER=clang -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x64/non_nacl_build -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x64/non_nacl_build

x32/nacl_build:
	-mkdir -p ./x32/nacl_build
	cd ./x32/nacl_build && cmake -D CMAKE_C_COMPILER=$(NACL_CLANG32) -D M_LIBRARY=$(NACL_LIBM32) -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x32/nacl_build -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x32/nacl_build

x64/nacl_build:
	-mkdir -p ./x64/nacl_build
	cd ./x64/nacl_build && cmake -D CMAKE_C_COMPILER=$(NACL_CLANG64) -D M_LIBRARY=$(NACL_LIBM64) -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x64/nacl_build -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x64/nacl_build

build: x32/non_nacl_build x64/non_nacl_build x32/nacl_build x64/nacl_build

clean:
	-rm -rf ./x32
	-rm -rf ./x64
