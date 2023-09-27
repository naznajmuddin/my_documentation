## Overview

These are embedded software notes on developing and designing RTOS software architecture.

## Topics:

### 1. Pulse Width Modulation (PWM): 

STM32F411CEU6 Blackpill has a 16-bit PWM pin, which means:

The maximum counter value will be `2^16 - 1 = 65535`

**Calculating the Pulse Width:**

For example the value you want to set is 33000, the calculation is:

`Pulse Width (cycles) = (<your-value>/65535) * MAX_PERIOD`

`MAX_PERIOD == Maximum counter value == 65536`

`Pulse Width (cycles) = (33000/65535) * 65536 ≈ 33000`

**Calculating the Duty Cycle:**

`Duty Cycle (%) = (Pulse Width / Period) * 100%`

For example:

`Duty Cycle (%) = (33000 / 65536) * 100% ≈ 50.35%`