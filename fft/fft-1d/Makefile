#INPUT_SIZE = SMALL
#INPUT_SIZE = MEDIUM
INPUT_SIZE = LARGE

CC = gcc -std=c99 -O2

CFLAGS = -pedantic -Wall -O0 -g -DINPUT_SIZE=INPUT_SIZE_$(INPUT_SIZE)
INCLUDES =
LFLAGS =
LIBS = -lm

OBJ_DIR = obj
G_OBJ_DIR = obj_g
T_OBJ_DIR = obj_t

TARGET = main
SRC = fft.c octave.c timer.c

OBJECTS = $(SRC:%.c=$(OBJ_DIR)/%.o)
G_OBJECTS = $(SRC:%.c=$(G_OBJ_DIR)/%.o)
T_OBJECTS = $(SRC:%.c=$(T_OBJ_DIR)/%.o)

all: $(TARGET) gp-$(TARGET) t-$(TARGET)

$(TARGET): $(OBJ_DIR) $(OBJECTS)
	$(CC) $(OBJECTS) $(CFLAGS) $(INCLUDES) -o $@.exe $(TARGET).c $(LFLAGS) $(LIBS)

gp-$(TARGET): $(G_OBJ_DIR) $(G_OBJECTS)
	$(CC) $(G_OBJECTS) $(CFLAGS) $(INCLUDES) -g -pg -o $@.exe $(TARGET).c $(LFLAGS) $(LIBS)

t-$(TARGET): $(T_OBJ_DIR) $(T_OBJECTS)
	$(CC) $(T_OBJECTS) $(CFLAGS) $(INCLUDES) -DINT_TIME -o $@.exe $(TARGET).c $(LFLAGS) $(LIBS)


$(OBJ_DIR)/%.o: %.c
	$(CC) $(CFLAGS) -o $@ -c $<

$(G_OBJ_DIR)/%.o: %.c
	$(CC) $(CFLAGS) -g -pg -o $@ -c $<

$(T_OBJ_DIR)/%.o: %.c
	$(CC) $(CFLAGS) -DINT_TIME -o $@ -c $<


$(OBJ_DIR):
	mkdir $@

$(G_OBJ_DIR):
	mkdir $@

$(T_OBJ_DIR):
	mkdir $@


clean:
	$(RM) $(TARGET).exe $(OBJECTS) $(G_TARGET).exe gp-$(OBJECTS) t-$(TARGET).exe $(T_OBJECTS) *.mat
	$(RM) -rf $(OBJ_DIR) $(G_OBJ_DIR) $(T_OBJ_DIR)
