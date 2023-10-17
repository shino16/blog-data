---
title: "My in PFN 2023 Summer Internship Experience"
date: 2023-10-17T15:00:00+01:00
images:
- 'img/pfn.jpg'
hidden: true
---

[Japanese version](https://shino16.github.io/blog/post/work/intern-pfn/)

I completed a summer internship at Preferred Networks from August 10th to September 29th, focusing on the development of CuPy.

<div class="iframely-embed"><div class="iframely-responsive" style="height: 140px; padding-bottom: 0; margin-top: 1.5em; margin-bottom: 1.5em;"><a href="https://www.preferred.jp/ja/news/internship2023/" data-iframely-url="//iframely.net/ptE20rS?card=small"></a></div></div><script async src="//iframely.net/embed.js"></script>

I selected Preferred Networks for my summer internship due to its established reputation in the Japanese machine learning and competitive programming community and the appealing nature of their internship projects.

## Project Focus: "CuPy Development"

CuPy is a GPU version of NumPy/SciPy, allowing data processing on GPUs. Its APIs are highly compatible with its original counterparts.

Example: [https://cupy.dev](https://cupy.dev/)

```py
>>> import cupy as cp
>>> x = cp.arange(6).reshape(2, 3).astype('f')
>>> x
array([[ 0.,  1.,  2.],
       [ 3.,  4.,  5.]], dtype=float32)
>>> x.sum(axis=1)
array([  3.,  12.], dtype=float32)
```

The goal of this project was to add new features to CuPy.

In [the list of recruiting projects](https://www.preferred.jp/wp-content/uploads/2023/03/831d7079054f3a9adf79bef7f143a578-1.pdf), NumPy and CUDA were listed as essential requirements, with NCCL, MPI and Metal as preferred skills. At that time I had only a superficial understanding of CUDA, but I made up my mind and studied CUDA extensively in line with the project-specific selection tasks.​

This year, I applied for several internships with selection assignments, and realized that challenging myself provided significant learning opportunities. The desire to intern at specific places drove me to learn new languages and frameworks, as well as gain practical experience with them.

## What I have done

Summary: I submitted a [PR](https://github.com/cupy/cupy/pull/7881) to CuPy's GitHub repository. This PR added [`DistributedArray`](https://cupy--7881.org.readthedocs.build/en/7881/reference/generated/cupyx.distributed.array.DistributedArray.html), a multi-GPU version of CuPy's [N-dimensional array (`ndarray`)](https://docs.cupy.dev/en/stable/reference/generated/cupy.ndarray.html).

### Basic API

We assume an environment where multiple devices (GPUs) are connected to a single host (CPU).

```py
a = numpy.arange(10)
A = distributed_array(a, {0: slice(5), 1: slice(5, 10)})
```

This code puts the part `a[:5]` on device 0, and `a[5:10]` on device 1. The same applies to higher dimensions, where you can specify any basic indexing keys for each device.

`DistributedArray` supports `ufunc`, allowing various element-wise operations such as `A+B` and `sin(A)`. I also added basic support for reduction like `A.sum(axis=0)` and matrix multiplication `A @ B`.

There are some unique concepts for `DistributedArray`, with a particular challenge being *resharding*.

### Resharding

Consider:

```py
A = distributed_array(a, {0: slice(5), 1: slice(5, 10)})
B = distributed_array(b, {0: slice(5), 1: slice(5, 10)})
C = distributed_array(b, {0: slice(7), 1: slice(7, 10)})
```

Calculating `A+B` is straightforward, where each device computes its corresponding part, `a[:5] + b[:5]` and `a[5:10] + b[5:10]`. However `A+C` is challenging, where the segments held by each device do not match. That's when we `reshard`, like:

```py
C2 = C.reshard(A.index_map)
```

This reconfigures the data in `C` to match the layout of `A`. In this example, it transfers the `c[5:7]` portion from device 0 to device 1. This way, `C2` is structured just as `A` is, with `c[0:5]` on device 0 and `c[5:10]` on device 1. Calculating `A+C2` is trivial.

This `reshard` is implemented in a way that enables *parallel execution of data transfer and subsequent operations*, using NCCL for asynchronous data transfer. For example, consider:

```py
A + C.reshard(A.index_map)
```

This code performs the following steps:

1. [Transfer] Transfer `c[5:7]` from device 0 to device 1
2. [Operation] Calculate `a[0:5] + c[0:5]` on device 0
3. [Operation] Calculate `a[5:7] + c[5:7]` on device 1
4. [Operation] Calculate `a[7:10] + c[7:10]` on device 1

`reshard` executes 1. as an asynchronous operaation. Simultaneously, step 2. and 4. are also executed in parallel. 3. follows as soon as 1. is completed. In this way, programmers can easily utilize the idle time during data transfer for other operations.

## Reflection

### My Work

Each trial and improvement deepened my understanding of CUDA-related concepts, and provided satisfaction in seeing my efforts turn into tangible results. I would have liked more time to refine my work.

Being recruited as an intern and having my efforts recognized as remarkable performance during the internship allowed me to recognize my strengths and gain confidence. I am now proud of my design and implementation skills.

### Inspiration from Others

PFN provided opportunities to interact with other interns and full-time employees. They had exceptional skills and actively took action to learn and apply new technologies. People in my team were all kind and talented, making the experience intellectually satisfying. I highly appreciate their support.

### Future Plans

This internship significantly increased my interest in GPU-related technologies. Dealing with technologies that maximizes performance is fascinating, and fortunately this field seems to be demanded in machine learning.

Consdering that six months ago I knew almost nothing about CUDA, I am amazed that I was able to learn so much in such a short time. It was an invaluable opportunity to discover and acquire new skills in practice. I intend to continue to actively apply for more internships and learn various technologies.
