osx에서 OpenCL 컴파일 방법

```
$ gcc -framework OpenCL hello.c
```

`clCreateCommandQueue`함수에서 3번째 인자는 property를 의미하는데 osx에서는 `CL_QUEUE_OUT_OF_ORDER_EXEC_MODE_ENABLE`를 못 쓰는 듯하다. 이 인자를 전달하면 에러가 발생한다.

# AMD OpenCL tutorial

## context

device와 memory를 만들고, program을 컴파일하여 실행하는 작업 모두 context 내에서 이루어진다.  
context는 많은 device(CPU or GPU)를 가질 수 있다.  
또한 device간에 memory consistency를 보장한다.