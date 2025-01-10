# VHDL Counter Race Condition
This repository demonstrates a race condition in a simple VHDL counter and provides a corrected version.  The original counter suffers from potential issues with its reset handling, leading to inconsistent behavior after reset.

The `buggy_counter.vhdl` file contains the flawed code, and `fixed_counter.vhdl` provides the solution.

## Bug Description
The primary issue lies in the `if rst = '1'` condition within the process.  If the reset signal is asserted while the clock is also transitioning, it might not properly reset the `internal_count`.   The existing implementation only sets `internal_count` to 0 if the reset is high at the *same time* as the clock edge, and in this scenario this is not a reliable condition to depend on. This is a classic race condition between two events.

## Solution
The corrected code in `fixed_counter.vhdl` uses a more robust approach to handle the reset signal.  By explicitly checking and setting the count to 0 at the start of each clock cycle in the process, the race condition is avoided.