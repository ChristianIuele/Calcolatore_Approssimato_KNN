CC = gcc
NASM = nasm

# Aggiunto -mavx per forzare il supporto AVX
CFLAGS = -m64 -O3 -march=native -mavx -Wall -g -fopenmp
# Aggiunto -DPIC per codice Position Independent (buona norma su 64bit)
NASMFLAGS = -f elf64 -DPIC

LIBS = -lm -fopenmp

# Lista degli oggetti assembly da compilare
# Include sia la logica del pivot che le utils SSE/AVX
ASM_OBJ = quantpivot64omp_asm.o sseutils64.o

all: main64omp

# Regola per il file assembly principale
quantpivot64omp_asm.o: quantpivot64omp.nasm
	$(NASM) $(NASMFLAGS) quantpivot64omp.nasm -o quantpivot64omp_asm.o

# Regola per le utility SSE/AVX
sseutils64.o: sseutils64.nasm
	$(NASM) $(NASMFLAGS) sseutils64.nasm -o sseutils64.o

# Regola principale
# Nota: quantpivot64omp.c è una dipendenza ma non viene compilato separatamente
# perché è incluso via #include dentro main.c
main64omp: main.c common.h quantpivot64omp.c $(ASM_OBJ)
	$(CC) $(CFLAGS) main.c $(ASM_OBJ) $(LIBS) -o main64omp

clean:
	rm -f *.o main64omp

.PHONY: all clean