.PHONY : build clean

.DEFAULT_GOAL := build

SANDBOXING_NACL_DIR=$(shell realpath ../../Sandboxing_NaCl)
ZLIB_DIR=$(shell realpath ../../zlib_nacl)
NACL_CLANG32=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/i686-nacl-clang
NACL_CLANG64=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/x86_64-nacl-clang
NACL_CLANG++32=$(NACL_CLANG32)++
NACL_CLANG++64=$(NACL_CLANG64)++
NACL_LIBM32=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32/libm.a
NACL_LIBM64=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib/libm.a
NACL_AR32=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/i686-nacl-ar
NACL_AR64=$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/bin/x86_64-nacl-ar

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
	mkdir -p ./x32/nacl_build/mainCombine
	cd ./x32/nacl_build/mainCombine && $(NACL_AR32) -x ../libpng.a
	cd ./x32/nacl_build/mainCombine && $(NACL_CLANG++32) -fPIC -m32 -I/home/shr/Code/LibrarySandboxing/zlib_nacl -B$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib/ -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32 -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib ./*.o -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -L$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32 -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -ldyn_ldr_sandbox_init /home/shr/Code/LibrarySandboxing/zlib_nacl/builds/x32/nacl_build/libz.a -o ./libpng.nexe

x64/nacl_build:
	-mkdir -p ./x64/nacl_build
	cd ./x64/nacl_build && cmake -D CMAKE_C_COMPILER=$(NACL_CLANG64) -D M_LIBRARY=$(NACL_LIBM64) -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x64/nacl_build -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x64/nacl_build
	mkdir -p ./x64/nacl_build/mainCombine
	cd ./x64/nacl_build/mainCombine && $(NACL_AR64) -x ../libpng.a
	cd ./x64/nacl_build/mainCombine && $(NACL_CLANG++64) -fPIC -m64 -I/home/shr/Code/LibrarySandboxing/zlib_nacl -B$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib/ -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib ./*.o -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -L$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -ldyn_ldr_sandbox_init /home/shr/Code/LibrarySandboxing/zlib_nacl/builds/x64/nacl_build/libz.a -o ./libpng.nexe

###########################################

x32/non_nacl_build_debug:
	-mkdir -p ./x32/non_nacl_build_debug
	cd ./x32/non_nacl_build_debug && cmake -D CMAKE_BUILD_TYPE=Debug -D CMAKE_C_COMPILER=clang -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x32/non_nacl_build_debug -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x32/non_nacl_build_debug

x64/non_nacl_build_debug:
	-mkdir -p ./x64/non_nacl_build_debug
	cd ./x64/non_nacl_build_debug && cmake -D CMAKE_BUILD_TYPE=Debug -D CMAKE_C_COMPILER=clang -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x64/non_nacl_build_debug -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x64/non_nacl_build_debug

x32/nacl_build_debug:
	-mkdir -p ./x32/nacl_build_debug
	cd ./x32/nacl_build_debug && cmake -D CMAKE_BUILD_TYPE=Debug -D CMAKE_C_COMPILER=$(NACL_CLANG32) -D M_LIBRARY=$(NACL_LIBM32) -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x32/nacl_build_debug -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x32/nacl_build_debug
	mkdir -p ./x32/nacl_build_debug/mainCombine
	cd ./x32/nacl_build_debug/mainCombine && $(NACL_AR32) -x ../libpng.a
	cd ./x32/nacl_build_debug/mainCombine && $(NACL_CLANG++32) -fPIC -m32 -I/home/shr/Code/LibrarySandboxing/zlib_nacl -B$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib/ -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32 -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib ./*.o -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -L$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib32 -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-32/lib -ldyn_ldr_sandbox_init /home/shr/Code/LibrarySandboxing/zlib_nacl/builds/x32/nacl_build_debug/libz.a -o ./libpng.nexe

x64/nacl_build_debug:
	-mkdir -p ./x64/nacl_build_debug
	cd ./x64/nacl_build_debug && cmake -D CMAKE_BUILD_TYPE=Debug -D CMAKE_C_COMPILER=$(NACL_CLANG64) -D M_LIBRARY=$(NACL_LIBM64) -D ZLIB_INCLUDE_DIR=$(ZLIB_DIR) -D PNG_BUILD_ZLIB=$(ZLIB_DIR)/builds/x64/nacl_build_debug -D PNG_SHARED=0 ../../../
	$(MAKE) -C ./x64/nacl_build_debug
	mkdir -p ./x64/nacl_build_debug/mainCombine
	cd ./x64/nacl_build_debug/mainCombine && $(NACL_AR64) -x ../libpng.a
	cd ./x64/nacl_build_debug/mainCombine && $(NACL_CLANG++64) -fPIC -m64 -I/home/shr/Code/LibrarySandboxing/zlib_nacl -B$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib/ -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib -Wl,-rpath-link,$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib ./*.o -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -L$(SANDBOXING_NACL_DIR)/native_client/toolchain/linux_x86/pnacl_newlib/x86_64-nacl/lib -L$(SANDBOXING_NACL_DIR)/native_client/scons-out/nacl-x86-64/lib -ldyn_ldr_sandbox_init /home/shr/Code/LibrarySandboxing/zlib_nacl/builds/x64/nacl_build_debug/libz.a -o ./libpng.nexe

###########################################

build: x32/non_nacl_build x64/non_nacl_build x32/nacl_build x64/nacl_build x32/non_nacl_build_debug x64/non_nacl_build_debug x32/nacl_build_debug x64/nacl_build_debug 
clean:
	-rm -rf ./x32
	-rm -rf ./x64
