CFLAGS ?= -Werror -Wall -I..
LDFLAGS ?= -L../build -lvedis

tests = $(wildcard *-test.c)
tobjs = $(tests:.c=.o)

.PHONY: check
check: ct/_ctcheck
	+ct/_ctcheck

.PHONY: bench
bench: ct/_ctcheck
	+ct/_ctcheck -b

ct/ct.o: ct/ct.h

$(tobjs): ct/ct.h

ct/_ctcheck: ct/_ctcheck.o ct/ct.o $(objs) $(tobjs)

ct/_ctcheck.c: $(tobjs) ct/gen
	ct/gen $(tobjs) > $@.part
	mv $@.part $@

.PHONY: clean
clean:
	rm -f ct/_* *.o ct/*.o
