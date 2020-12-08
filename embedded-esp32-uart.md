# uart into esp32

The ESP32 chip has three UART controllers (UART0, UART1, and UART2) that feature an identical set of registers for ease of programming and flexibility.

1.    Setting Communication Parameters - Setting baud rate, data bits, stop bits, etc.

2.    Setting Communication Pins - Assigning pins for connection to a device.

3.    Driver Installation - Allocating ESP32’s resources for the UART driver.

4.    Running UART Communication - Sending / receiving data

5.    (Optional) Using Interrupts - Triggering interrupts on specific communication events

6.    (Optional) Deleting a Driver - Freeing allocated resources if a UART communication is no longer required



## 1. setting configuration

```
const int uart_num = UART2;
uart_config_t uart_config = {
    .baud_rate = 115200,
    .data_bits = UART_DATA_8_BITS,
    .parity = UART_PARITY_DISABLE,
    .stop_bits = UART_STOP_BITS_1,
    .flow_ctrl = UART_HW_FLOWCTRL_CTS_RTS,
    .rx_flow_ctrl_thresh = 122,
};
// Configure UART parameters
ESP_ERROR_CHECK(uart_param_config(uart_num, &uart_config));

```

## 2. setting communication pins

```
// Set UART pins(TX: IO16 (UART2 default), RX: IO17 (UART2 default), RTS: IO18, CTS: IO19)
ESP_ERROR_CHECK(
	uart_set_pin(UART_NUM_2, UART_PIN_NO_CHANGE, UART_PIN_NO_CHANGE, 18, 19)
	);
```



## 3. driver installation

```
// Setup UART buffered IO with event queue
const int uart_buffer_size = (1024 * 2);
QueueHandle_t uart_queue;
// Install UART driver using an event queue here
ESP_ERROR_CHECK(
	uart_driver_install(UART2, uart_buffer_size, uart_buffer_size, 10, &uart_queue, 0)
	);
```

## 4.1 Running UART Communication - Sending / receiving data


### transmitting

- blocking

```
// Write data to UART.
char* test_str = "This is a test string.\n";
uart_write_bytes(uart_num, (const char*)test_str, strlen(test_str));


// Write data to UART, end with a break signal.
uart_write_bytes_with_break(uart_num, "test break\n",strlen("test break\n"), 100);
```


- non-blocking while there are available space and return the number of bytes that were written.

```
// uart_tx_chars()

// uart_wait_tx_done()
const int uart_num = UART_NUM_2;
ESP_ERROR_CHECK(uart_wait_tx_done(uart_num, 100));  // wait timeout is 100 RTOS ticks (TickType_t)
```

### receiving



```
// Read data from UART.
const int uart_num = UART2;
uint8_t data[128];
int length = 0;

ESP_ERROR_CHECK(
	uart_get_buffered_data_len(uart_num, (size_t*)&length)
	);
length = uart_read_bytes(uart_num, data, length, 100);
```


```
uart_flush() // can clear buffer
```

### mode selection

```
// Setup UART in rs485 half duplex mode
ESP_ERROR_CHECK(uart_set_mode(uart_num, UART_MODE_RS485_HALF_DUPLEX));
```


## 4.2 Software Flow Control


```
uart_set_rts()
uart_set_dtr()
```



## 5. (Optional) Using Interrupts 

```
uart_enable_intr_mask() 
uart_disable_intr_mask() 
```



## 6. (Optional) Deleting a Driver

If the communication established with uart_driver_install() is no longer required, the driver can be removed to free allocated resources by

```
calling uart_driver_delete()
```