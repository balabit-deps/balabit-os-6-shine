# Emscriptem compilation

EMCC:=emcc
EXPORTED_FUNCTIONS:='["_shine_check_config", "_shine_js_init",\
	"_shine_samples_per_pass", "_shine_encode_buffer",\
  "_shine_flush", "_shine_close"]'
CFLAGS:=-O2 -s ASM_JS=1 -s USE_TYPED_ARRAYS=2 -s EXPORTED_FUNCTIONS=$(EXPORTED_FUNCTIONS)

C_FILES:=$(wildcard ../src/lib/*.c) src/wrapper.c
HEADER_FILES:=$(wildcard ../src/lib/*.h)
SOURCES:=$(C_FILES) $(HEADER_FILES)
OBJECTS:=$(C_FILES:%.c=%.bc)

all: dist/libshine.js

dist/libshine.js: $(SOURCES) $(OBJECTS) src/pre.js src/post.js
	$(EMCC) $(CFLAGS) --pre-js src/pre.js --post-js src/post.js $(OBJECTS) -o dist/libshine.js

%.bc: %.c
	$(EMCC) $(CFLAGS) -I../src/lib -c $< -o $@

clean:
	rm -f *.bc ../src/lib/*.bc
