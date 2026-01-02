CC = gcc

CFLAGS = -m64 -O3 -march=native -Wall -g

LIBS = -lm

all: main64

main64: main.o quantpivot64.o
	$(CC) $(CFLAGS) main.o quantpivot64.o $(LIBS) -o main64

main.o: main.c common.h
	$(CC) $(CFLAGS) -c main.c -o main.o

quantpivot64.o: quantpivot64.c common.h
	$(CC) $(CFLAGS) -c quantpivot64.c -o quantpivot64.o

clean:
	rm -f *.o main64

.PHONY: all clean