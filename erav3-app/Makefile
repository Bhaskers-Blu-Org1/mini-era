CC = gcc -std=c99
MFILE = Makefile

COPTF0 = -O0
COPTF2 = -O2
COPTF3 = -O3

CFLAGS = -pedantic -Wall -g $(COPTF2)
#CFLAGS += -L/usr/lib/python2.7/config-x86_64-linux-gnu -L/usr/lib -lpython2.7 -lpthread -ldl  -lutil -lm  -Xlinker -export-dynamic -Wl,-O1 -Wl,-Bsymbolic-functions
CFLAGS +=  -lm -Xlinker -export-dynamic

INCLUDES =


LFLAGS = 
#LFLAGS += 
#LIBS = -lviterbi -lfmcwdist -lpthread -ldl -lutil -lm -lpython2.7
LIBS     = 

OBJDIR      = obj
V_OBJDIR    = obj_v

# The full mini-era target, etc.
TARGET = erav3c
V_TARGET = verbose_erav3c

XMIT_SRC = xmit_pipe.c \
	   crc.c
RECV_SRC = recv_pipe.c\
	   complex_ops.c \
	   delay.c \
	   gr_equalizer.c \
	   ofdm.c \
	   sync_long.c \
	   fir.c \
	   sync_short.c \
	   viterbi_flat.c \
	   descrambler_function.c \
	   simple_dft.c \
	   fft-1d.c 

SRC    = main.c kernels_api.c $(XMIT_SRC) $(RECV_SRC)
OBJ    = $(SRC:%.c=$(OBJDIR)/%.o)
OBJ_V  = $(SRC:%.c=$(V_OBJDIR)/%.o)

#$(info $$SRC is [${SRC}])
#$(info $$OBJ is [${OBJ}])


all: $(TARGET) $(V_TARGET)

$(TARGET): $(OBJDIR)  $(OBJ) 
	$(CC) $(OBJ) $(CFLAGS) $(INCLUDES) -o $@ $(LFLAGS) $(LIBS)

$(V_TARGET): $(V_OBJDIR)  $(OBJ_V) 
	$(CC) $(OBJ_V) $(CFLAGS) $(INCLUDES) -DDEBUG_MODE -o $@ $(LFLAGS) $(LIBS)




$(OBJDIR):
	mkdir $@

$(V_OBJDIR):
	mkdir $@



$(OBJDIR)/%.o: %.c
	$(CC) $(CFLAGS) $(PYTHONINCLUDES) -o $@ $(PYTHONLIBS) -c $<

$(V_OBJDIR)/%.o: %.c
	$(CC) $(CFLAGS) $(PYTHONINCLUDES) -DDEBUG_MODE -o $@ $(PYTHONLIBS) -c $<


clean:
	$(RM) $(TARGET) $(OBJ) $(V_TARGET) $(V_OBJ)

clobber: clean
	$(RM) -rf $(OBJDIR) $(V_OBJDIR)

allclean: clobber


depend:;	makedepend -f$(MFILE) -- $(CFLAGS) -- $(SRC)
# DO NOT DELETE THIS LINE -- make depend depends on it.


