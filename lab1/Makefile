CXX = clang++
CXXFLAGS = -std=c++17 -march=native -mavx2 -O3

all: mandelbrot

mandelbrot: mandelbrot_cpu.cpp
	mkdir -p out
	$(CXX) $(CXXFLAGS) -o $@ $<

run: mandelbrot
	./mandelbrot

clean:
	rm -f mandelbrot
	rm -rf out

.PHONY: all run clean
