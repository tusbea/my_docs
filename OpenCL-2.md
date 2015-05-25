OpenCL tutorial : http://liminia.tistory.com/64

## clGetDeviceIDs()

- `num_entries` : `devices`(4th arg)에 추가될 수 있는 device의 최대 개수
- `devices` : device가 저장된다.
- `num_devices` : `device_type`(2th arg)에 맞는 device의 개수가 저장된다.

```c
cl_int clGetDeviceIDs(
  cl_platform_id platform,
  cl_device_type device_type,
  cl_uint num_entries,	 
  cl_device_id *devices,	 
  cl_uint *num_devices) 
```

## clCreateContext()

- `num_devices` : `devices`에 저장된 device의 개수
- `devices` : `clGetDeviceIDs`로 구한 devices

```c
cl_context clCreateContext(
  cl_context_properties *properties,
  cl_uint num_devices,
  const cl_device_id *devices,
  void *pfn_notify (
    const char *errinfo, 
    const void *private_info, 
    size_t cb, 
    void *user_data),
  void *user_data,
  cl_int *errcode_ret)
```

## clCreateCommandQueue()

```c
cl_command_queue clCreateCommandQueue(
  cl_context context,
  cl_device_id device,
  cl_command_queue_properties properties,
  cl_int *errcode_ret)
```

## clBuildProgram error 확인하기

```c
if (err == CL_BUILD_PROGRAM_FAILURE) {
  size_t log_size;
  clGetProgramBuildInfo(program, device, CL_PROGRAM_BUILD_LOG, 0, NULL, &log_size);

  char *log = (char *) malloc(log_size);

  clGetProgramBuildInfo(program, device, CL_PROGRAM_BUILD_LOG, log_size, log, NULL);

  printf("%s\n", log);
}
```

## amd printf 활성화

활성화하는 전처리 과정이다. 하지만 실제로 효과가 있는지는 의문.

```c
#pragma OPENCL EXTENSION cl_amd_printf : enable
```

## 계속 에러났던 이유

buffer 관련 함수 호출시 바이트 단위이므로 sizeof(float)를 곱해야 했다.

## event

