CC         = gcc
CFLAGS     = -g -Wall -fomit-frame-pointer -O2
LDFLAGS    =
TST_FILES  = $(sort $(wildcard *.tst))
INIT_FILES = $(addsuffix .init,$(basename $(wildcard *.tst)))
RES_FILES  = $(sort $(addsuffix .result,$(basename $(wildcard *.tst))))
TEST_OPTS  = --verbose --show code,regs,data,acc,io,ints,attr,time

export LD_LIBRARY_PATH=..

.PHONY: all test clean
.SECONDARY: $(INIT_FILES)

test: x86test $(RES_FILES)

all: x86test
	@./prepare_test *.tst
	@./x86test $(TEST_OPTS) *.init

x86test: x86test.c
	$(CC) $(CFLAGS) $< -I ../include -L .. -lx86emu -o $@ $(LDFLAGS)

%.result: %.init
	@./x86test $(TEST_OPTS) $<

%.init: %.tst
	@./prepare_test $<

clean:
	rm -f *~ *.o x86test *.init *.result *.log

