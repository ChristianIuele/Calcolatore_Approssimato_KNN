CC = gcc
CFLAGS = -m64 -O3 -march=native -mavx -Wall -g -fopenmp
LIBS = -lm -fopenmp

#Assembler NASM
ASM = nasm
ASMFLAGS = -f elf64

# Target principale
all: main64omp

#Linking con assembly
main64omp: main.o quantpivot64omp.o quantpivot64_asm.o
	$(CC) $(CFLAGS) -o $@ $^ $(LIBS)

# Compila main.c
main.o: main.c common.h
	$(CC) $(CFLAGS) -c main.c

# Compila quantpivot64omp.c
quantpivot64omp.o: quantpivot64omp.c common.h
	$(CC) $(CFLAGS) -c quantpivot64omp.c

# Compila assembly AVX
quantpivot64_asm.o: quantpivot64.nasm
	$(ASM) $(ASMFLAGS) -o $@ $

# Pulizia
clean:
	rm -f *.o main64omp out_*.ds2

# Test rapido
test: main64omp
	./main64omp

.PHONY: all clean test
