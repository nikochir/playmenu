# init #

include config.mk

NAME?=dmenu

SRC?=./src
OBJ?=./bin
BIN?=./bin

SRCS:=$(wildcard $(SRC)/*.c)
OBJS:=$(SRCS:.c=.o)
BINS:=$(BIN)/$(NAME).exe

CFLAGS?=$(CFLAGS)
LFLAGS?=$(LDFLAGS)

# work #

all: build

build: $(BINS)
clean:
	rm -f $(BINS) $(OBJS)
print:
	$(info "[CFLAGS]=($(CFLAGS))")
	$(info "[LFLAGS]=($(LFLAGS))")
	$(info "[SRC]=($(SRC))")
	$(info "[OBJ]=($(OBJ))")
	$(info "[BIN]=($(BIN))")
	$(info "[SRCS]=($(SRCS))")
	$(info "[OBJS]=($(OBJS))")
	$(info "[BINS]=($(BINS))")
install: all
	mkdir -p $(DESTDIR)$(PREFIX)/bin
	cp -f $(BINS) dmenu_path dmenu_run $(DESTDIR)$(PREFIX)/bin
	chmod 755 $(DESTDIR)$(PREFIX)/bin/dmenu
	chmod 755 $(DESTDIR)$(PREFIX)/bin/dmenu_path
	chmod 755 $(DESTDIR)$(PREFIX)/bin/dmenu_run
	chmod 755 $(DESTDIR)$(PREFIX)/bin/stest
	mkdir -p $(DESTDIR)$(MANPREFIX)/man1
	sed "s/VERSION/$(VERSION)/g" < dmenu.1 > $(DESTDIR)$(MANPREFIX)/man1/dmenu.1
	sed "s/VERSION/$(VERSION)/g" < stest.1 > $(DESTDIR)$(MANPREFIX)/man1/stest.1
	chmod 644 $(DESTDIR)$(MANPREFIX)/man1/dmenu.1
	chmod 644 $(DESTDIR)$(MANPREFIX)/man1/stest.1
uninstall:
	rm -f $(DESTDIR)$(PREFIX)/bin/$(NAME)\
		$(DESTDIR)$(PREFIX)/bin/$(NAME)_path\
		$(DESTDIR)$(PREFIX)/bin/$(NAME)_run\
		$(DESTDIR)$(MANPREFIX)/man1/$(NAME).1\

.PHONY: all options clean dist install uninstall

# rule #

$(BINS): $(OBJS)
	$(CC) -o $@ $< $(LDFLAGS)

%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@

config.h:
	cp config.def.h $@

# endf #
