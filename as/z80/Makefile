PRJDIR = ../

include $(PRJDIR)/Makefile.common

OBJDIR	= obj/$(EXT)

SDC	= .

SRC	= asdata.c asexpr.c aslex.c aslist.c asmain.c asout.c \
	  assubr.c assym.c gbadr.c gbext.c gbmch.c gbpst.c

OBJS	= $(SRC:%.c=$(OBJDIR)/%.o)

BINS	= $(BUILDDIR)as$(EXT)

CFLAGS	+= $(CPPFLAGS) $(OPTS) -I. -DINDEXLIB -DMLH_MAP -DUNIX -DSDK
CFLAGS	+= -funsigned-char
CFLAGS	+= -I$(SLIB) 

LDFLAGS += -lm $(EXTRALIBS)

all:	$(OBJDIR) $(BUILDDIR) dep $(BINS)

dep: Makefile.dep

Makefile.dep: $(SRC) *.h
	$(CPP) $(CPPFLAGS) $(M_OR_MM) $(SRC) > Makefile.dep

include Makefile.dep

$(OBJDIR):
	mkdir -p $(OBJDIR)
	
$(BUILDDIR):
	mkdir -p $(BUILDDIR)

$(BINS): $(OBJS)
	$(CC) -o $(BINS) $(OBJS) $(LDFLAGS)


$(OBJDIR)/%.o:	%.c
	$(CC) -c $(CFLAGS) -o $@ $<

$(OBJDIR)/%.o:	$(SLIB)/%.c
	$(CC) -c $(CFLAGS) -o $@ $<

_as-z80:
	$(MAKE) EXT=-z80$(E)

_as-gbz80:
	$(MAKE) EXT=-gbz80$(E) OPTS=-DGAMEBOY

include clean.mk
