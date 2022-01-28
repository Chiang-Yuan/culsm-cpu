CC      =	gcc
CPP     = 	g++
CFLAGS  =	-O3 -Wall -g --std=c++11


NVCC    = 	nvcc
CUDIR   = 	/usr/local/cuda
NVFLAGS = 	-O3 -I$(CUDIR)/include -m64 -arch=compute_75 -code=sm_75 -Xptxas -v -rdc=true

TARGET	=	culsm-cpu

SRC_DIRS	?=	../../src

SRCS 	:=	$(shell find $(SRC_DIRS) -name *.cpp -or -name *.c -or -name *.cu -or -name *.s)

OBJS	= 	$(SRCS:.c=.o)


INC		= 	-I/src
LFLAGS	= 
#LIBS    =	-lm -lcudart
LIBS	=	-lm

MKFILE	= 	Makefile 


$(TARGET) : $(OBJS)
		$(CPP) $(CFLAGS) $(INC) -o $(TARGET) $(OBJS) $(LFLAGS) $(LIBS)

.c.o:
		$(CPP) $(CFLAGS) $(INC) -c $< -o $@


.PHONY: clean

clean:
		rm -f $(TARGET) $(patsubst %,$(SRC_DIRS)/%.o,$(basename $(SRCS)))

depend: $(SRCS)
		makedepend $(INC) $^

#
