#####################################################################
## file        : test makefile for build current dir .c            ##
## author      : jernymy                                           ##
## date-time   : 05/06/2010                                        ##
#####################################################################

CC      = gcc
CPP     = g++
RM      = rm -rf

## debug flag
DBG_ENABLE   = 0

## source file path
SRC_PATH   := .

## target exec file name
TARGET     := robot

## get all source files
SRCS       += $(wildcard $(SRC_PATH)/*.c $(SRC_PATH)/*.cpp )
SRCS2      += $(wildcard $(SRC_PATH)/rt_type/*.c)

#OBJS       := $(SRCS:.c=.o)
OBJS := $(wildcard $(SRC_PATH)/*.o)

## need libs, add at here
LIBS := pthread m native pthread_rt xenomai rt ethercat_rtdm

## used headers  file path
INCLUDE_PATH := . ../include ../include/rt_type /usr/xenomai/include /usr/xenomai/include/posix

## used include librarys file path
LIBRARY_PATH := /lib /usr/xenomai/lib /home/igh/etherlabmaster-code/lib/.libs

## debug for debug info, when use gdb to debug
ifeq (1, ${DBG_ENABLE}) 
	CFLAGS += -D_DEBUG -O0 -g -DDEBUG=1
endif

## get all include path
CFLAGS  += $(foreach dir, $(INCLUDE_PATH), -I$(dir)) 
CFLAGS += -Wl,@/usr/xenomai/lib/posix.wrappers 

## get all library path
LDFLAGS += $(foreach lib, $(LIBRARY_PATH), -L$(lib))

## get all librarys
LDFLAGS += $(foreach lib, $(LIBS), -l$(lib))

all: build

build:
	$(CPP) -c $(CFLAGS) $(SRCS) $(SRCS2)
	$(CPP) $(CFLAGS) -o $(TARGET) $(OBJS) $(LDFLAGS)
#	$(RM) $(OBJS)

clean:
	$(RM) $(OBJS) $(TARGET)
