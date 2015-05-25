## getopt()

`optarg`는 `char*`형으로 인자가 저장된다.

```c
#include <unistd.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
  int opt;
  int n = 0;

  // -n 옵션 뒤에 오는 인자를 optarg로 받으려면 :을 붙인다.
  while ((opt = getopt(argc, argv, "n:")) != -1)
  {
    switch (opt)
    {
      case 'n':
        n = atoi(optarg);
        break;
    }
  }

  printf("%d\n", n);

  return 0;
}
```

```sh
$ ./a.out -n 10
10
```