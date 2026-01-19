all: cpu gpu

# -mavx2
# enables avx2
mandelbrot_cpu: mandelbrot_cpu.cpp	
	mkdir -p out
	g++ -std=c++17 -march=native -mavx2 -O3 -o $@ $<

# $ nvidia-smi --query-gpu=compute_cap --format=csv
# 6.1
# So using -arch=sm_61 (streaming multiprocessing version 6.1)
mandelbrot_gpu: mandelbrot_gpu.cu
	mkdir -p out
	nvcc -O3 -arch=sm_61 -o $@ $<

run_cpu: mandelbrot_cpu
	./mandelbrot_cpu

run_gpu: mandelbrot_gpu
	./mandelbrot_gpu

clean:
	rm -f mandelbrot_cpu
	rm -f mandelbrot_gpu
	rm -f mandelbrot
	rm -rf out

.PHONY: all run clean
