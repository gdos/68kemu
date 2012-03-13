CC = m68k-atari-mint-gcc
CPUFLAGS = -mcpu=5475
CFLAGS = -Wall -O3 -fomit-frame-pointer
AR = m68k-atari-mint-ar

NATIVE_CC = gcc
NATIVE_CFLAGS = -O -Wall -pedantic

M68KMAKE_SOURCES = m68kmake.c
M68KMAKE_INPUT = m68k_in.c

CFILES = m68kcpu.c m68kdasm.c
HFILES = m68k.h m68kconf.h m68kcpu.h
FILES = $(CFILES) $(HFILES) $(M68KMAKE_SOURCES) $(M68KMAKE_INPUT)

GENCFILES = m68kops.c m68kopnz.c m68kopdm.c m68kopac.c
GENHFILES = m68kops.h
GENFILES = $(GENCFILES) $(GENHFILES)

OBJS = $(patsubst %.c,%.o,$(CFILES) $(GENCFILES))

.PHONY: all
all:	libmusashi.a

m68kmake: $(M68KMAKE_SOURCES)
	$(NATIVE_CC) $(NATIVE_CFLAGS) $^ -o $@

$(GENFILES): m68kmake $(M68KMAKE_INPUT)
	./m68kmake . $(M68KMAKE_INPUT)

$(OBJS): %.o: %.c
	$(CC) $(CPUFLAGS) $(CFLAGS) -c $<

libmusashi.a: $(OBJS)
	$(AR) cr $@ $^
	
clean:
	rm -f *.a *.o $(GENFILES) m68kmake

# Dependencies
m68kcpu.c: m68kops.h