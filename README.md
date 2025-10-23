# STM32F411RE ADC with Multiple Channels and DMA Circular Mode

This project demonstrates how to use the ADC on an STM32F411RE microcontroller to read multiple channels using DMA in circular mode.

## Project Overview

This project is configured to read three ADC channels (ADC_CHANNEL_0, ADC_CHANNEL_1, and ADC_CHANNEL_2) continuously using DMA. The DMA is set up in circular mode to continuously transfer the ADC conversion results to a memory buffer without CPU intervention.

## Features

-   **Microcontroller:** STM32F411RE
-   **ADC:** ADC1 is used to read 3 channels.
-   **DMA:** DMA2 Stream 0 is configured in circular mode to handle the ADC data transfer.
-   **Development Environment:** STM32CubeIDE

## How it Works

1.  **ADC Configuration:**
    -   ADC1 is configured to run in continuous conversion mode.
    -   Scan conversion mode is enabled to convert a sequence of channels.
    -   Three channels (0, 1, and 2) are configured in the sequence.

2.  **DMA Configuration:**
    -   DMA2 Stream 0 is connected to ADC1.
    -   The DMA is configured in circular mode. This means that once it finishes transferring the data for all ADC channels, it will automatically restart from the beginning of the buffer.
    -   The ADC values are stored in a `uint16_t` array called `ADC_VAL`.

3.  **Main Application:**
    -   The `main` function initializes the MCU, GPIO, DMA, and ADC.
    -   `HAL_ADC_Start_DMA()` is called to start the ADC conversion with DMA.
    -   The main loop is kept simple with a counter and a delay, as the ADC conversions are handled in the background by the DMA.
    -   The `HAL_ADC_ConvCpltCallback()` function is provided as a weak function. You can implement this function in your user code to process the ADC data after each complete sequence conversion.

## Getting Started

### Prerequisites

-   [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)
-   A NUCLEO-F411RE board or a custom board with an STM32F411RE microcontroller.

### Building and Running

1.  Clone this repository or import it into your STM32CubeIDE workspace.
2.  Open the project in STM32CubeIDE.
3.  Build the project by clicking on the hammer icon or by pressing `Ctrl+B`.
4.  Run the project by clicking on the green play button or by pressing `F11`.
5.  You can use the debugger to inspect the values in the `ADC_VAL` array to see the live ADC conversion results.

## Code Structure

-   `Core/Src/main.c`: The main application file containing the initialization and the main loop.
-   `Core/Inc/main.h`: The main header file.
-   `ADC_Multiple_Channel_with_DMA_Circular_Mode_STM32F411RE.ioc`: The STM32CubeMX configuration file. You can open this file to see the graphical configuration of the peripherals.
