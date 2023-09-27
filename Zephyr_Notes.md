## Overview

These are the notes for ZephyrRTOS architecture. These notes are for reference on constructing Zephyr software development.

## Topics:

### 1. Basic GPIO

**Defining Input Output**

For example, defining basic GPIO LED. `red_led` is from DeviceTree aliases.
```
const struct gpio_dt_spec red_led_spec = GPIO_DT_SPEC_GET(DT_NODELABEL(red_led), gpios);
```

**Turn ON/OFF the basic GPIO**
```
gpio_pin_set(red_led_spec.port, red_led_spec.pin, 1); // 1 == HIGH
gpio_pin_set(red_led_spec.port, red_led_spec.pin, 0); // 0 == LOW
```

**Alternative Way:**

`uart_a` & `uart_b` are from DeviceTree aliases which are from `uart-a` & `uart-b`

```
#define UART_NODE1 DT_ALIAS(uart_a)
#define UART_NODE2 DT_ALIAS(uart_b)

const struct device *const uart_cha = DEVICE_DT_GET(UART_NODE1);
const struct device *const uart_chb = DEVICE_DT_GET(UART_NODE2);
```

### 2. PWM GPIO

**Defining Input Output**

For example, defining PWM GPIO LED:

```
#define MOTOR1_PWM_NODE DT_ALIAS(motor_pwm_1) // PB6
const struct pwm_dt_spec motor_pwm_1 = PWM_DT_SPEC_GET(DT_ALIAS(motor_pwm_1));
const struct device *pwm_dev = motor_pwm_1.dev;
```

**Turn ON/OFF the PWM GPIO**

There are many functions to set the PWM pins. Here is the basic one:

Insert the pwm value and convert it into pulse width value:

```
uint32_t pulse_width = (uint32_t)value * MAX_PERIOD / 65535U;
```

Setting the pwm pin with the pulse width value:

```
// Set the PWM pulse width in cycles
pwm_set(pwm_dev, motor_pwm_1.channel, MAX_PERIOD, pulse_width, 0);
```

The `pwm_set` needs:

- `motor_pwm_1.dev` = device

- `motor_pwm_1.channel` = channel

- `MAX_PERIOD` = maximum period

- `pulse_width` = pulse width value

- `flags` = normally `0`