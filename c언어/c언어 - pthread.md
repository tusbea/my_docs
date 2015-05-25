
# Pthreads

## what is Pthreads?

Pthreads = POSIX threads

## thread 예제

array를 데이터로 받아 double 변수 리턴한다.  
array 변수를 인자로 전달하면 call by ref이기 때문에 다른 쓰레드 생성시 같은 array 변수를 사용하게 되면 주의해야 한다.

```c
#include <pthread.h>

void *f(void *data)
{
  int *arr = (int *)data;
  int s = arr[0], e = arr[1];
  double sum = 0.0;
  double *ret = (double *)malloc(sizeof(double));
  ...
  *ret = sum;
  return (void *)ret;
}

int main()
{
  pthread_t thread;
  int data[2];
  pthread_create(&thread, NULL, f, (void*)data);
  
  pthread_join(thread, NULL);	// 쓰레드 종료 기다리기
}

```

## mutex

```c
pthread_mutex_t mutex[100];
for (i = 0; i < 100; i++)
  pthread_mutex_init(&mutex[i], NULL);
  // 또 다른 init 방법
  // pthread_mutex_t mymutex = PTHREAD_MUTEX_INITIALIZER;
  
pthread_mutex_lock(&mutex[1]);
...
pthread_mutex_unlock(&mutex[1]);
```