# Default optimization level
O ?= 2

# Work around missing UTF locale
LANG=C

all: shell

-include build/rules.mk

%.o: %.c shell.h $(BUILDSTAMP)
	$(call run,$(CC) $(CPPFLAGS) $(CFLAGS) $(O) $(DEPCFLAGS) -o $@ -c,COMPILE,$<)

shell: shell.o helpers.o
	$(call run,$(CC) $(CFLAGS) $(O) -o $@ $^ $(LDFLAGS) $(LIBS),LINK $@)

sleep61: sleep61.c
	$(call run,$(CC) $(CFLAGS) $(O) -o $@ $^ $(LDFLAGS) $(LIBS),BUILD $@)

check: shell
	perl check.pl

check-%: shell
	perl check.pl $(subst check-,,$@)

clean: clean-main
clean-main:
	$(call run,rm -rf shell *.o *~ *.bak core *.core,CLEAN)
	$(call run,rm -rf $(DEPSDIR) out *.dSYM)

realclean: clean
	@echo + realclean
	$(V)rm -rf $(DISTDIR) $(DISTDIR).tar.gz

.PRECIOUS: %.o
.PHONY: all clean clean-main check check-%
