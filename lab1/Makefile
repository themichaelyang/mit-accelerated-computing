CXX = clang++
CXXFLAGS = -std=c++17 -march=x86-64 -O3
ARCH = arch -x86_64

all: mandelbrot

mandelbrot: mandelbrot_cpu.cpp
	mkdir -p out
	$(ARCH) $(CXX) $(CXXFLAGS) -o $@ $<

run: mandelbrot
	$(ARCH) ./mandelbrot

clean:
	rm -f mandelbrot
	rm -rf out

.PHONY: all run clean
