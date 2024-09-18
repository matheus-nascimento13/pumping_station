# Pump Control System with Rotation Logic

This project is a Structured Text (ST) program for a **Pump Control System** using three pumps. The program manages the operation of the pumps based on water levels, with an additional feature of **pump rotation** after each pump operation to ensure even usage. The system handles alarms for both high and low water levels, and switches pump sequences after they have completed a cycle.

## Features

- **Three Pump Control**: Operates three pumps based on different water level conditions.
- **Water Level Management**: 
  - **High level (>= 80)**: All pumps turn on, and a high-level alarm is triggered.
  - **Medium level (60 <= level < 80)**: Two pumps are activated, and high-level alarm is cleared.
  - **Normal level (40 <= level < 60)**: Only one pump is activated.
  - **Low level (20 <= level < 40)**: All pumps are turned off.
  - **Very low level (< 20)**: Low-level alarm is triggered, and all pumps remain off.
- **Pump Rotation**: After each pump completes its cycle, the next pump in the sequence starts. The order of pumps changes after each cycle to balance wear and tear on the pumps.
- **Rising Edge Detection**: The program detects the rising edge when a pump is switched off, triggering the pump rotation logic.
  
## Variables

- `level` : The current water level in the tank (REAL).
- `mode_operation`: Enables or disables the automatic pump operation (BOOL).
- `working_state`: Describes the current working state of the pumps (WSTRING).
- `pump1`, `pump2`, `pump3`: Status of each pump (BOOL).
- `pump1_was_on`, `pump2_was_on`, `pump3_was_on`: Used for detecting the rising edge when each pump is turned off (BOOL).
- `counter_pump`: A counter to rotate the pump order (INT).
- `high_level_alarm`, `low_level_alarm`: Alarms for high and low water levels (BOOL).
- `rising_edge1`, `rising_edge2`, `rising_edge3`: Variables to detect the rising edge for each pump (BOOL).

## Logic Flow

### Pump Control Based on Water Level

The pumps are controlled based on the following water levels:

1. **High Water Level (>= 80)**
   - All pumps are turned on.
   - High-level alarm is triggered.

2. **Medium Water Level (60 <= level < 80)**
   - Two pumps are turned on, and the high-level alarm is cleared.

3. **Normal Water Level (40 <= level < 60)**
   - One pump is turned on, and alarms are cleared.

4. **Low Water Level (20 <= level < 40)**
   - All pumps are turned off, and alarms are cleared.

5. **Very Low Water Level (< 20)**
   - All pumps remain off, and a low-level alarm is triggered.

### Pump Rotation

- Each pump operates based on the `counter_pump` value (1, 2, or 3).
- After a pump completes its cycle (i.e., when a pump turns off), the program detects the rising edge and rotates to the next pump in sequence.
- The sequence of pumps is rotated after each pump is switched off to balance usage.

## How to Use

1. Set the `level` variable to simulate different water levels.
2. Set the `mode_operation` to `TRUE` to enable the automatic control of the pumps.
3. The system will automatically adjust the number of active pumps based on the current water level and will rotate the pumps after each cycle.

## Future Improvements

- Add manual pump control mode.
- Introduce maintenance logs to track pump usage.
- Optimize pump sequence rotation based on actual pump runtime.
- Add flow accumulator
