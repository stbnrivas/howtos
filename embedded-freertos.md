# FreeRTOS

- a FreeRTOS application is a strutured as one or more tasks
- a task is a function run by the scheduler
- each task runs in its own context
- the scheduler switches the processor between tasks




## 1 task apis


```
xTaskCreate()

vTaskDelay()   | xTaskAbortDelay() | vTaskDelayUntil()

vTaskSuspend() | vTaskResume()     | xTaskResumeFromISR()
```

a typical skeleton of a task

```
void vTaskFunction(void *pvParameters){

	for(;;){
		// task code
	}

	vTaskDelete(NULL);
}
```

a task creation

```
xTaskCreate(vTaskFunction,"myTask",size_stack_for_task_in_words,NULL,taskIDLE_PRIORITY,&taskHandle); //
```

task scheduler call (critical), the stask dont start until run scheduler

```
vTaskStartScheduler()
vTaskEndScheduler()
```



## 2 FreeRTOS interaction between 2 or more tasks

- I want to communicate directly to another task         ==> Task notification
- someone needs to block or unblock a task, no care who  ==> semaphore
- only the task that blocks another task can unblock     ==> mutex
- I need to pass data from one to other task to anohter  ==> queue
- multiple things need to happen before I unblock a task ==> Event Group






### semaphores / mutex APIs

#### 2.1 semaphores

- used to control access to a common resource by multiple tasks
- semaphores are a construct to ensure that only a certain number of tasks can accesses teh semaphore at once
- FreeRTOS provide both binary and counting semaphores


```
xSemaphoreCreateBinary() | xSemaphreCreateCounting()

xSemaphoreDelete()

xSemaphoreTake() | xSemaphoreTakeFromISR()

xSemaphoreGive() | xSemaphoreGiveFromISR()

xSemaphoreCreateMutex()
```

a typical pattern use of semaphore

- declare semaphore variable
- create binary semaphore
- start master task
- start worker task

```
SemaphoreHandle_t xSemaphore;
vSemaphoreCreateBinary(xSemaphore);
xTaskCreate(pvMasterTask, ...)
xTaskCreate(pvWorkerTask, ...)


// master task
void pvMasterTask(void *pvTaskParams){
	while(pdTRUE){
		vTaskDelay(pdMS_TO_TICKS(2000)); // simulate work
		xSemaphoreGive(xSemaphore);
	}
}

void pvWorkerTask(void* pvTaskParams){
	while(pdTRUE){
		if(xSemaphoreTake(xSemaphore,portMAX_DELAY)){
			// code
		}
	}
}
```


#### mutexes

- specialized use of binary semaphore
- a mutex allows only one task to execute while the mutex is owned
- only the task that locked the mutex can unlocks the mutex
- cannot be used from ISR


```
char sharedResource[20];

SemaphoreHandle_t xMutex;
vSemaphoreCreateMutex(xMutex);
xTaskCreate(pvTaskA, ...);
xTaskCreate(pvTaskB, ...);


void pvTaskA(void* pvTaskParams){
	while(pdTRUE){
		if(xSemaphoreTake(xMutex,(TickType_t)10)){
			xSemphoreGive(xMutex);
			vTaskDelay(...); // tipically it's good practice delay after the release
		}
	}
}

void pvTaskB(void* pvTaskParams){
	while(pdTRUE){
		if(xSemaphoreTake(xMutex,(TickType_t)10)){
			xSemphoreGive(xMutex);
			vTaskDelay(...); // tipically it's good practice delay after the release
		}
	}
}
```


## Event bits and Groups

- event bit is a flag which can be waited upon set to 1
- event group are a set of event bits
- a task can then wait on an event group for a specific set of bits to be set


```
xEventGroupCreate()
xEventGroupSetBits()
xEventGroupWaitBits()




#define BIT_0 (1<<0)
#define BIT_1 (1<<1)

EventGroupHandle_t xEventGroup = xEventGroupCreate();
xCreateTask(pvTask1,...);
xCreateTask(pvTask2,...);


void pvTask1(void* pvTaskParams){
	xEventGroupSetBits(xEventGroup,BIT_0);
	while(pdTRUE){}
}


uint32_t result = xEventGroupWaitBits(xEventGroup,BIT_0|BIT_1,pdTRUE,pdTRUE,pdMS_TO_TICKS(5000))
if((result & (BIT_0 | BIT_1))== (BIT_0 | BIT_1)){
	// all task ready
} else {
	// not all task signaled ready in time
}
```




## Timers

```
xTimerCreate()
xTimerStart()
xTimerStop()
xTimerGetTimerID() | xTimerSetTimerID()

TimerHandle_t timer = xTimerCreate("Timer",pdMS_TO_TICKS(1000),pdTRUE,(void*)0,vTimerCallback);
xTimerStart(timer,0);

void vTimerCallback(TimerHandle_t xTimer){
	uint32_t ulCount = (uint32_t)pvTimerGetTimerID(xTimer);
	if(ulCount<4){
		// 4 is because you want to repeat 4 times
		vTimerSetTimerID(xTimer, (void*)(ulCount++));
	} else {
		xTimerStop(xTimer,0);
	}
}
```



## Memory management

- embedded system can have many different RAM requirements, memory management in FreeRTOS is implemented in portability layer
- provide 5 different heap implementations
- 

```
vPortMalloc()
vPortFree()

#define configTOTAL_HEAP_SIZE ((size_t)(2048U*1024U))
#define configUSE_STATIC_ALLOCATION 1
```


## sensors reading

- sensors can be reached by interfaces like GPIO and I2C
- access is typically platform specific
- accesibles via Board Support Packages (BSP) assist in standardizing `BSP_* functions`


```
void vStartTSensorDemo(){
	BSP_TSENSOR_Init();
	xTaskCreate(pvReadTSensorTaskk,"temp-task",200,NULL,tskIDLE_PRIORITY,NULL)
}

void pvReadTSensorTask(void* pvTaskParameters){
	while(pdTRUE){
		uint32_t temp_value = BSP_TSENSOR_ReadTemp();
		vTaskDelay(pdMS_TO_TICKS(1000));
	}
}
```




## handling button pressed with ISR's


- button can be handled by polling or by interrupt service routines (ISR's)
- ISR ar platform specific
- Board support packages are provided on supported platforms
- ISER run outside of task, the best practice is finish as quickly as possible and post a message to queue

```
BaseType_t checkIfYieldRequired = xTaskResumeFromISR(buttonPressedTaskHandle);
portYIELD_FROM_ISR(checkIfYieldRequired);
```






## inter task communication

- direct-to-task-notifications
- queues
- stream buffers
- message buffers


### task notifications

Each task has a 32-bit notification value that is initialized to zero whe the task is created- A task notification is used to send and event directly to and potentially unblock an RTOS task, and optionally update the receiving task's notification value in one of the following way

- write a 32bit number to the notification value
- add one (increment) te notification value
- set one or more bits in the notification value
- leave the notification value unchanged

```
a more simple way using 

- xTaskNotifyGive(TaskHandle_t xTaskNotify); 
- xTaskNotifyGiveFromISR(TaskHandle_t xTaskToNotify, BaseType_t *pxHigherPriorityTaskWoken);


a more flexible way using 

- BaseType_t xTaskNotify(TaskHandle_t xTaskToNotify, uint32_t ulValue, eNofityAction eAction);
- BaseType_t xTaskNotifyFromISR(TaskHandle_t xTaskToNotify, uint32_t ulValue, eNofityAction eAction, BaseType_t *pxHigherPriorityTaskWoken);

```



NOT WORK {
	
to get TaskHandle_t you can use below but previously you should enable the function into FreeRTOSConfig.h 

```
//to get TaskHandle_t you can use
TaskHandle_t  taskToNotify;
taskToNotify = xTaskGetHandle("task_cstring_used_into_xTaskCreate_as_2nd_parameter")
// IT NOT WORK TRY USING A GLOBAL VAR of TaskHandle_t
```
}



IT WORK{

if save a global variable when you create the task

}








into the task which should be notificated

```
a more simple way using ulTaskNotifyTake()

BaseType_t ulTaskNotifyTake(
	BaseType_t xClearCountOnExit,
	TickType_t xTicksToWait)

a more flexible way using xTaskNotifyWait(), it waits with optional timeout until receive notification from other task or interrupt handler

BaseType_t xTaskNotifyWait(
	uint32_t ulBitsToClearOnEntry,
	uint32_t ulBitsToClearonExit,
	uint32_t pulNotificationValue,
	TickThype_t xTicksToWait);



pdTRUE is returned if a notification was received
pdFALSE is returned if the call to xTaskNotify timed out
```






```
#include "FreeRTOS.h"
#include "task.h"

BaseType_t xTaskNotify(TaskHandle_t xTaskToNotifiy, uint32_t ulValude, eNotifyAction eAction);
BaseType_t xTaskNotifyAndQuery(TaskHandle_t xTaskToNotify, uint32_t ulValue, eNotifyAction eAction, uint32_t *pulPrevioouesNotifyValue);
```



you can use to wait for definicion `portMAX_DELAY` to block undefinitelly 




IMPORTANTE la funcion xTaskGetHandle("task_name") no está disponible si no se modifica en el fichero FReeRTOSConfig.h la linea y poniendola a 1

```
#define INCLUDE_xTaskGetHandle      1
```


### queues

- preferred form of inter-task communication
- typically implemented as FIFO buffers
- designed for operation in memory constrained environments
- can have multiple publishers and subscribers
- fixed in length
- messages can be of any type and are sent by copy

queue api

```
#include "FreeRTOS.h"
#include "queue.h"

void vQueueAddToRegistry(QueueHandle_t xQueueHandler, char* xQueueName)
```


```
QueueHandle_t xQueueCreate(UBaseType_t uxQueueLength, UBaseType_t uxItemSize)
vQueueDelete()
xQueueSend()       | xQueueSendFromISR()
xQueueSendToFront() | xQueueSendToBack() | xQueueSendToBackFromISR()

xQueueReceive()    | xQUeueReceiveFromISR()
xQueuePeek()       | xQueuePeekFromISR()
xQUeueReset()
```


```
QueueHandle_t q = xQueueCreate(item_size,bytes_every_item);
char buf[10];
xQueueSend(q,buff,0); // 0 send now
xQueueReceive(q,(void*)buff,0); 
```




### direct-to-task notitication

- every FreeRTOS task has a 32 bit notification value
- it is an evente sent directly to the task
- the receiving task waits on the notification
- efficient opton to queues, semaphores and event group
- intended for 1:1 communication
- can be used as a light weight binary semaphore


```
xTaskNotifyGive()  | xTaskNotifyGiveFromISR()
ulTaskNotifyTake()
xTaskNotify()      | xTaskNotifyFromISR()
xTaskNotifyWait()
xTaskNotifyStateClear()
```

```
int val = ulTaskNotifyTake(pdFALSE,(TickType_t)portMAX_DELAY);
if(val>0){
	// took it
} else {
	// didn't get it
}



xTaskNOtifyGive(takeTaskHandle);
xTaskNotifyGive(takeTaskHandle);
```


### stream buffers


### message buffers



