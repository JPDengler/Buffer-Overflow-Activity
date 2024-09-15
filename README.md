# CS 405 Module Two: Buffer Overflow Activity

## Overview

This project is part of the CS 405 course, focusing on securing C++ code against buffer overflow attacks. The objective of the assignment was to detect and prevent a buffer overflow when collecting user input, preventing it from overwriting sensitive information, such as an account number.

## Project Files

### C++ Source Code

- `BufferOverflow.cpp`: The main source code that demonstrates a buffer overflow vulnerability and implements a solution to prevent it.

### Python Files

- `PythonWithExploit.py`: A Python script that demonstrates the buffer overflow exploit.
- `PythonWithoutExploit.py`: A Python script that shows secure input handling without an overflow exploit.

### Documentation

- `Module 2 Buffer Overflow Activity - Joseph Dengler.docx`: Contains a summary of the process, screenshots of the outputs before and after fixing the buffer overflow, and an explanation of how the code was corrected.

## Problem Description

The initial problem involved code that allows users to input data, which could potentially overwrite the account number due to a buffer overflow vulnerability. This could lead to unpredictable behavior in the program, especially in applications dealing with sensitive data, such as a banking system.

## Solution

The solution involved modifying the user input logic to prevent any overflow while keeping the original variable (`account_number`) unchanged. Specifically:
1. Used `std::cin.get()` to limit input length to 19 characters (to prevent the buffer overflow).
2. Checked for buffer truncation and warned the user if too many characters were entered.
3. Ensured that input larger than the buffer was safely ignored to avoid any further overflow issues.

### Key Code Changes

```cpp
// Use std::cin.get to limit input to the size of the buffer minus 1 (for null terminator)
std::cin.get(user_input, sizeof(user_input));

// Check if the input was truncated by the buffer size limit
if (std::cin.gcount() == sizeof(user_input) - 1 && std::cin.peek() != '\n')
{
    std::cout << "Warning: You entered too many characters, input has been truncated." << std::endl;
    // Clear remaining input to avoid unexpected behavior
    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}
