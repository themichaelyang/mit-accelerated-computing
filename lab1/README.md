Code for 6.S894 [Lab 1](https://accelerated-computing-class.github.io/fall24/labs/lab1).

# Write-up

> How does the run time of the scalar GPU implementation compare to the scalar CPU implementation? What factors do you think might contribute to each of their run times?

The scalar GPU implementation has a slower runtime than the scalar CPU implementation. I assume this is due to the added cost of copying memory into the GPU, while still having comparable compute times.

> How did you initialize cx and cy? How did you handle differences in the number of inner loop iterations between pixels in the same vector? How does the performance of your vectorized implementation compare to the scalar versions?

I initialized `cx` and `cy` as vectors (`cxs` and `cys`). I used a bitwise mask to handle differences in the inner loop while in the same vector, so the vector positions would only update based the condition bitmap. 

AVX2 handles 32 bytes, and each float/integer is 4 bytes, so vectorization should give a theoretical 32/4 = 8x speedup.

The actual performance is about 7x faster.

# CPU

Used AVX2 since my cluster didn't have AVX-512. AVX2 is similar but supports 256-bit (32 bytes) operations instead of 512-bit (64 bytes), and less convenient masking operations.

```
$ lscpu | grep -oP 'Model name:\s*\K.*'
Intel(R) Core(TM) i7-6850K CPU @ 3.60GHz
```

```
$ make run_cpu
./mandelbrot_cpu
Testing with image size 256x256 and 1000 max iterations.
Running mandelbrot_cpu_scalar ...
  Runtime: 72.2459 ms
Running mandelbrot_cpu_vector ...
  Runtime: 10.5942 ms
  Correctness: average output difference from reference = 0
```

# GPU

```
$ nvidia-smi --query-gpu=compute_cap --format=csv
compute_cap
6.1
6.1
```

```
$ nvidia-smi --query-gpu=name --format=csv
name
NVIDIA TITAN X (Pascal)
NVIDIA TITAN X (Pascal)
```

```
$ make run_gpu
./mandelbrot_gpu
Testing with image size 256x256 and 1000 max iterations.
Running launch_mandelbrot_gpu_scalar ...
  Runtime: 1235.93 ms
  Correctness: average output difference from reference = 0
Running launch_mandelbrot_gpu_vector ...
  Runtime: 57.9646 ms
  Correctness: average output difference from reference 0
```
