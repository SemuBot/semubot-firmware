PROJECT  = wheelbase
LIB      = micro_ros_stm32cubemx_utils/microros_static_library_ide/libmicroros
BUILD    = build
CC       = arm-none-eabi-gcc
SIZE     = arm-none-eabi-size

INC = Core/Inc \
      Drivers/CMSIS/Device/ST/STM32F3xx/Include \
      Drivers/CMSIS/Include \
      Drivers/STM32F3xx_HAL_Driver/Inc \
      Drivers/STM32F3xx_HAL_Driver/Inc/Legacy \
      Middlewares/ST/STM32_USB_Device_Library/Class/CDC/Inc \
      Middlewares/ST/STM32_USB_Device_Library/Core/Inc \
      Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS \
      Middlewares/Third_Party/FreeRTOS/Source/include \
      Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F \
      USB_DEVICE/App \
      USB_DEVICE/Target

SRC = $(wildcard Core/Src/*.c) \
      $(wildcard Drivers/STM32F3xx_HAL_Driver/Src/*.c) \
      $(wildcard Middlewares/ST/STM32_USB_Device_Library/Core/Src/*.c) \
      $(wildcard Middlewares/ST/STM32_USB_Device_Library/Class/CDC/Src/*.c) \
      $(wildcard Middlewares/Third_Party/FreeRTOS/Source/*.c) \
      Middlewares/Third_Party/FreeRTOS/Source/CMSIS_RTOS/cmsis_os.c \
      Middlewares/Third_Party/FreeRTOS/Source/portable/GCC/ARM_CM4F/port.c \
      Middlewares/Third_Party/FreeRTOS/Source/portable/MemMang/heap_4.c \
      $(wildcard USB_DEVICE/*/*.c) \
      Core/Startup/startup_stm32f303retx.s

CFLAGS  = -mcpu=cortex-m4 -mthumb -mfpu=fpv4-sp-d16 -mfloat-abi=hard -Os -std=gnu11 \
          -ffunction-sections -fdata-sections --specs=nano.specs \
          -DUSE_HAL_DRIVER -DSTM32F303xE $(addprefix -I,$(INC)) -I$(LIB)/include
LDFLAGS = -TSTM32F303RETX_FLASH.ld --specs=nosys.specs \
          -Wl,--gc-sections -u _printf_float -u _scanf_float -L$(LIB) -lmicroros -lc -lm

all: $(BUILD)/$(PROJECT).elf

$(BUILD)/$(PROJECT).elf: $(SRC) $(LIB)/libmicroros.a
	mkdir -p $(BUILD)
	$(CC) $(CFLAGS) $(SRC) $(LDFLAGS) -o $@
	$(SIZE) $@

clean:
	rm -rf $(BUILD)

.PHONY: all clean
