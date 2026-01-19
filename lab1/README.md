Code for 6.S894 [Lab 1](https://accelerated-computing-class.github.io/fall24/labs/lab1).

# AVX2 vectorization

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

# GPU scalar

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
  Runtime: 1217.06 ms
  Correctness: average output difference from reference = 0
```
