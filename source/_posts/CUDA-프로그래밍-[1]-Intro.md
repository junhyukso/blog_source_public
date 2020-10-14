---
title: CUDA 프로그래밍 [1] Intro
date: 2020/10/14 3:53:00
updated: 2020/10/14 00:01:00
categories:
- GPU
- CUDA
- CUDA 프로그래밍 연재
tags:
- GPU
- CUDA
---

![](https://user-images.githubusercontent.com/41286195/95903113-aeaf1300-0dd0-11eb-8b4f-e9c83d302e0b.png)

## CUDA ?

**CUDA** (Computed Unified Device Architecture)는 NVIDIA사에서 개발한 **GPU 개발 플랫폼**입니다. 

CUDA를 사용하는 이유는 간단한데, GPU를 그래픽 처리만이 아닌 **일반적인 계산**(General Purpose)에 사용하는 것입니다. 즉 CUDA는 **GPU를 Programmable 하게 만들기 위한 플랫폼**입니다.

## Why GPU?

![](https://user-images.githubusercontent.com/41286195/96006875-e6719580-0e78-11eb-90e6-3f09eda8dce3.png)

GPU를 사용하는 가장 큰 이유는 바로 **매우 많은 연산을 동시에 처리하기 위함**입니다.

CPU는 일반적으로 적은 수의 코어(1~16개)를 가집니다. 각각의 코어의 연산성능은 강력하지만, 결국 **실제로 동시에 진행될수 있는 명령**의 최대는 **코어수**에 Bound 됩니다.

그러나 GPU는 개개의 연산능력은 약하지만, 수천개의 코어를 가지고 있습니다.(최신 Ampere architecture의 경우 약 10000개의 CUDA Core를 가지고 있습니다.)  
따라서 **병렬성이 큰 연산**이라면, GPU에서 실행시 CPU에 비해 **수백~수천배의 가속**을 얻을 수 있습니다.

GPU의 장점을 잘 보여주는 유튜브 동영상을 첨부합니다.

[https://youtu.be/-P28LKWTzrI](https://youtu.be/-P28LKWTzrI)

## How to Start CUDA? Any prerequisite?

```c
// Example of CUDA kernel
__global__ void addKernel( int *c, const int *a, const int *b )
{
    int i = threadIdx.x;

	if( i < arraySize )
		c[i] = a[i] + b[i];
}
```

CUDA 프로그래밍의 핵심은 **CUDA 커널**의 작성입니다. 

- CUDA커널은 기본적으로 C언어 문법을 사용하여 작성됩니다. 따라서, **C언어에 대한 지식이 필수적**입니다.
  - 최소한 메모리와 Pointer의 개념까지는 필요합니다.
- 또한, 이 강의에선 각종 CUDA API의 사용 편의를 위해 python wrapper인 PyCUDA를 사용할 예정입니다. 따라서 Python 언어에 대한 간단한 지식도 필요합니다.
- 추가적으로, 컴퓨터 구조에 대한 지식이 있다면 좋습니다. 단순한 CUDA커널의 작성으로도 CPU에 비해 큰 가속을 얻을 수 있지만, CUDA의 효율을 100% 이끌어내기 위해선 **컴퓨터 아키텍쳐에 대한 지식**이 필요합니다.

2편부터, 본격적인 CUDA 프로그래밍을 시작해보도록 하겠습니다.