##
## blzpack - BriefLZ example
##
## GCC Makefile
##

.SUFFIXES:

.PHONY: clean all

CFLAGS = -std=c99 -Wall -Wno-unused-function -msse2 -mfpmath=sse -O3 -flto
CPPFLAGS = -DNDEBUG -I../include

ifeq ($(OS),Windows_NT)
  LDFLAGS += -static
  ifeq ($(CC),cc)
    CC = gcc
  endif
endif

objs = blzpack.o parg.o brieflz.o depack.o depacks.o
objs2 =  parg.o brieflz.o depack.o depacks.o
target = blzpack
target2 = blzpack_lib

all: $(target)

%.o : %.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $<

%.o : ../src/%.c
	$(CC) $(CFLAGS) $(CPPFLAGS) -c -o $@ $<

$(target): $(objs)
	$(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) $^ $(LDLIBS) -o $@

$(target2): $(objs2)
	gcc -shared -o blzpack_lib.so $(objs2)

clean:
	$(RM) $(objs) $(target)
	$(RM) $(objs2) $(target2).so

blzpack.o: ../include/brieflz.h parg.h
blzpack_lib.o: ../include/brieflz.h parg.h
parg.o: parg.h
brieflz.o: ../include/brieflz.h
depack.o: ../include/brieflz.h
depacks.o: ../include/brieflz.h
