# unity testing made by throw the switch

[https://github.com/ThrowTheSwitch/Unity/blob/master/docs/UnityGettingStartedGuide.md](https://github.com/ThrowTheSwitch/Unity/blob/master/docs/UnityGettingStartedGuide.md)

## a simple example code from scratch with single target

- unity are small files download it:
 + [https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity.c](https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity.c)
 + [https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity.h](https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity.h)
 + [https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity_internals.h.h](https://raw.githubusercontent.com/ThrowTheSwitch/Unity/master/src/unity_internals.h.h)


- create model.h

```c
#ifndef _MODEL_H_
#define _MODEL_H_

int wrong(void);
int right(void);

#endif
```

- create model.c

```c
#include "model.h"

int wrong(void){
  return 0;
}


int right(void){
  return 1;
}
```

- create test_model.c

```c
#include "unity.h"
#include "model.h"

void setUp(void){
}

void tearDown(void){
}


void test_wrong_return_zero(void){
  TEST_ASSERT_EQUAL_INT(0, 0);
}

void test_right_return_one(void){
  TEST_ASSERT_EQUAL_INT(1, 1);
}


int main(void){
  UNITY_BEGIN();
  RUN_TEST(test_wrong_return_zero);
  RUN_TEST(test_right_return_one);
  return UNITY_END();
}

```

- create makefile

```makefile
CC=gcc

CFLAGS=-std=c89
CFLAGS += -Wall
CFLAGS += -Wextra
CFLAGS += -Wpointer-arith
CFLAGS += -Wcast-align
CFLAGS += -Wwrite-strings
CFLAGS += -Wswitch-default
CFLAGS += -Wunreachable-code
CFLAGS += -Winit-self
CFLAGS += -Wmissing-field-initializers
CFLAGS += -Wno-unknown-pragmas
CFLAGS += -Wstrict-prototypes
CFLAGS += -Wundef
CFLAGS += -Wold-style-definition
#CFLAGS += -Wno-misleading-indentation

UNITY_ROOT=.

default: model.o unity.o
	${CC} $(CFLAGS) -o model_test.o test_model.c model.o unity.o

unity.o:
	${CC} ${CFLAGS} -c unity.h unity.c

model.o:
	${CC} ${CFLAGS} -c model.h model.c

clean:
	rm model.o unity.o
```


now run into terminal

```bash
make clean; make

./model_test.o 
test_model.c:24:test_wrong_return_zero:PASS
test_model.c:25:test_right_return_one:PASS
```


## complements with Ceedling (ruby Test Build Management)