# Not pushing this file down to libraries in order to keep source tree as is (not populating with extra files, such as CMakeList.txt)
#
# Below each section represents a library with its own settings


###################
# SD card library
###################

SET(SDFAT_SRC
	SdFat/BlockDriver.h
	SdFat/FreeStack.h
#	SdFat/MinimumSerial.cpp
#	SdFat/MinimumSerial.h
	SdFat/SdFat.h
	SdFat/SdFatConfig.h
	SdFat/SysCall.h

	SdFat/FatLib/ArduinoFiles.h
	SdFat/FatLib/ArduinoStream.h
	SdFat/FatLib/BaseBlockDriver.h
	SdFat/FatLib/bufstream.h
	SdFat/FatLib/FatApiConstants.h
	SdFat/FatLib/FatFile.cpp
	SdFat/FatLib/FatFile.h
	SdFat/FatLib/FatFileLFN.cpp
	SdFat/FatLib/FatFilePrint.cpp
	SdFat/FatLib/FatFileSFN.cpp
	SdFat/FatLib/FatFileSystem.h
	SdFat/FatLib/FatLib.h
	SdFat/FatLib/FatLibConfig.h
	SdFat/FatLib/FatStructs.h
	SdFat/FatLib/FatVolume.cpp
	SdFat/FatLib/FatVolume.h
	SdFat/FatLib/FmtNumber.cpp
	SdFat/FatLib/FmtNumber.h
#	SdFat/FatLib/fstream.cpp
#	SdFat/FatLib/fstream.h
#	SdFat/FatLib/ios.h
#	SdFat/FatLib/iostream.h
#	SdFat/FatLib/istream.cpp
#	SdFat/FatLib/istream.h
#	SdFat/FatLib/ostream.cpp
#	SdFat/FatLib/ostream.h
#	SdFat/FatLib/StdioStream.cpp
#	SdFat/FatLib/StdioStream.h

	SdFat/SdCard/SdInfo.h
#	SdFat/SdCard/SdioCard.h
#	SdFat/SdCard/SdioCardEX.cpp
#	SdFat/SdCard/SdioTeensy.cpp
	SdFat/SdCard/SdSpiCard.cpp
	SdFat/SdCard/SdSpiCard.h
#	SdFat/SdCard/SdSpiCardEX.cpp

	SdFat/SpiDriver/DigitalPin.h
	SdFat/SpiDriver/SdSpiBaseDriver.h
        SdFat/SpiDriver/SdSpiDriver.h
#	SdFat/SpiDriver/SdSpiESP8266.cpp
#	SdFat/SpiDriver/SdSpiSAM3X.cpp
#	SdFat/SpiDriver/SdSpiSTM32F1.cpp
#       SdFat/SpiDriver/SdSpiSTM32x1.cpp
#	SdFat/SpiDriver/SdSpiTeensy3.cpp
#	SdFat/SpiDriver/SoftSPI.h
)
ADD_LIBRARY(SDFAT STATIC ${SDFAT_SRC})

TARGET_INCLUDE_DIRECTORIES(SDFAT PRIVATE
        SdFat
        STM32generic/libraries/SPI/src   # just for SPISettings
)

TARGET_COMPILE_DEFINITIONS(SDFAT PRIVATE
        -DENABLE_ARDUINO_FEATURES=0
)


###################
# FreeRTOS
###################

SET(FREERTOS_SRC
	FreeRTOS/Arduino_FreeRTOS.c
	FreeRTOS/Arduino_FreeRTOS.h
	FreeRTOS/FreeRTOS.h
	FreeRTOS/FreeRTOSConfig.h
        #FreeRTOS/heap_1.c
        FreeRTOS/heap_4.c
	FreeRTOS/list.c
	FreeRTOS/list.h
	FreeRTOS/mpu_prototypes.h
	FreeRTOS/mpu_wrappers.h
	FreeRTOS/port.c
	FreeRTOS/portable.h
	FreeRTOS/portmacro.h
	FreeRTOS/projdefs.h
	FreeRTOS/queue.c
	FreeRTOS/queue.h
	FreeRTOS/semphr.h
	FreeRTOS/StackMacros.h
	FreeRTOS/task.h
	FreeRTOS/tasks.c
	FreeRTOS/timers.c
	FreeRTOS/timers.h
)
ADD_LIBRARY(FreeRTOS STATIC ${FREERTOS_SRC})



###################
# Adafruit GFX library
###################

ADD_LIBRARY(AdafruitGFX STATIC
    AdafruitGFX/Adafruit_GFX.cpp
)

###################
# Pin
###################

ADD_LIBRARY(Pin STATIC
    Pin/Pin.cpp
    Pin/Pin.h
)

TARGET_INCLUDE_DIRECTORIES(Pin PRIVATE
    STM32generic/system/${STM32_FAMILY_LONG}/stm32_chip
)

###################
# SEPS525 driver
###################

ADD_LIBRARY(SEPS525_GFX STATIC
    SEPS525-OLED-Library/SEPS525_OLED.cpp
    SEPS525-OLED-Library/SEPS525_OLED.h
)

TARGET_INCLUDE_DIRECTORIES(SEPS525_GFX PRIVATE
    AdafruitGFX
    Pin
    SEPS525-OLED-Library
    STM32generic/libraries/SPI/src
)

###################
# STM32 generic - HAL based Arduino API implementation
###################

SET(STM32GENERIC_SRC
        STM32generic/libraries/SPI/src/SPI.cpp
        STM32generic/libraries/stm32_dma/src/stm32_dma.c

	STM32generic/cores/arduino/abi.cpp
#	STM32generic/cores/arduino/Arduino.h
##	STM32generic/cores/arduino/hooks.c
##	STM32generic/cores/arduino/itoa.c
##	STM32generic/cores/arduino/itoa.h
#	STM32generic/cores/arduino/main.cpp
##	STM32generic/cores/arduino/new.cpp
##	STM32generic/cores/arduino/new.h
#	STM32generic/cores/arduino/pins_arduino.h
	STM32generic/cores/arduino/Print.cpp
	STM32generic/cores/arduino/Print.h
	STM32generic/cores/arduino/Printable.h
	STM32generic/cores/arduino/Stream.cpp
	STM32generic/cores/arduino/Stream.h
#	STM32generic/cores/arduino/syscalls.c
#	STM32generic/cores/arduino/syscalls.h
##	STM32generic/cores/arduino/wiring_private.h
##	STM32generic/cores/arduino/WMath.cpp
##	STM32generic/cores/arduino/WString.cpp
##	STM32generic/cores/arduino/WString.h

#	STM32generic/cores/arduino/stm32/SerialUART.cpp
#	STM32generic/cores/arduino/stm32/SerialUART.h
#	STM32generic/cores/arduino/stm32/SerialUSB.cpp
#	STM32generic/cores/arduino/stm32/SerialUSB.h
##	STM32generic/cores/arduino/stm32/stm32_ADC.c
##	STM32generic/cores/arduino/stm32/stm32_build_defines.h
#	STM32generic/cores/arduino/stm32/stm32_clock.h
##	STM32generic/cores/arduino/stm32/stm32_def.h
        STM32generic/cores/arduino/stm32/stm32_gpio.c
        STM32generic/cores/arduino/stm32/stm32_gpio.h
        STM32generic/cores/arduino/stm32/stm32_gpio_af.c
        STM32generic/cores/arduino/stm32/stm32_gpio_af.h
        STM32generic/cores/arduino/stm32/stm32_gpio_af_F0F2F3F4F7L0L1L4.c
        STM32generic/cores/arduino/stm32/stm32_gpio_af_F1.c
#	STM32generic/cores/arduino/stm32/stm32_gpio_exti.c
        STM32generic/cores/arduino/stm32/stm32_init.c # SysTick_Handler THERE!
        STM32generic/cores/arduino/stm32/stm32_pin_list.c
        STM32generic/cores/arduino/stm32/stm32_PWM.c
#	STM32generic/cores/arduino/stm32/USBDevice.cpp
#	STM32generic/cores/arduino/stm32/USBDevice.h
 
##	STM32generic/cores/arduino/usb/usb_device.c
##	STM32generic/cores/arduino/usb/usb_device.h
#	STM32generic/cores/arduino/usb/usbd_conf.h
#	STM32generic/cores/arduino/usb/usbd_conf_F1.c
##	STM32generic/cores/arduino/usb/usbd_conf_F4.c
##	STM32generic/cores/arduino/usb/usbd_conf_F7.c
##	STM32generic/cores/arduino/usb/usbd_conf_L0.c
##	STM32generic/cores/arduino/usb/usbd_conf_L4.c
#	STM32generic/cores/arduino/usb/usbd_core.c
#	STM32generic/cores/arduino/usb/usbd_core.h
#	STM32generic/cores/arduino/usb/usbd_ctlreq.c
#	STM32generic/cores/arduino/usb/usbd_ctlreq.h
#	STM32generic/cores/arduino/usb/usbd_def.h
#	STM32generic/cores/arduino/usb/usbd_desc.c
#	STM32generic/cores/arduino/usb/usbd_desc.h
#	STM32generic/cores/arduino/usb/usbd_ioreq.c
#	STM32generic/cores/arduino/usb/usbd_ioreq.h
 
#	STM32generic/cores/arduino/usb/cdc/usbd_cdc.c
#	STM32generic/cores/arduino/usb/cdc/usbd_cdc.h
#	STM32generic/cores/arduino/usb/cdc/usbd_cdc_if.c
#	STM32generic/cores/arduino/usb/cdc/usbd_cdc_if.h


#	STM32generic/variants/BLUEPILL/systemclock_config.c
	STM32generic/variants/BLUEPILL/variant.h
)

ADD_LIBRARY(STM32generic STATIC ${STM32GENERIC_SRC})

TARGET_INCLUDE_DIRECTORIES(STM32generic PRIVATE
        STM32generic/system/${STM32_FAMILY_LONG}/stm32_chip
        STM32generic/libraries/stm32_dma/src
)

TARGET_COMPILE_DEFINITIONS(STM32generic PRIVATE
        -DMENU_USB_SERIAL
)

###################
# USB Core and classes
###################

SET(USB_SRC
	USB/Core/usbd_conf.c
	USB/Core/usbd_conf.h
	USB/Core/usbd_core.c
	USB/Core/usbd_core.h
	USB/Core/usbd_ctlreq.c
	USB/Core/usbd_ctlreq.h
	USB/Core/usbd_def.h
	USB/Core/usbd_desc.c
	USB/Core/usbd_desc.h
	USB/Core/usbd_ioreq.c
	USB/Core/usbd_ioreq.h

	USB/CDC/usbd_cdc.c
	USB/CDC/usbd_cdc.h
	USB/CDC/usbd_cdc_if.c
	USB/CDC/usbd_cdc_if.h

	USB/MSC/usbd_msc.c
	USB/MSC/usbd_msc.h
	USB/MSC/usbd_msc_bot.c
	USB/MSC/usbd_msc_bot.h
	USB/MSC/usbd_msc_data.c
	USB/MSC/usbd_msc_data.h
	USB/MSC/usbd_msc_scsi.c
	USB/MSC/usbd_msc_scsi.h

	USB/MSC_CDC/usbd_msc_cdc.c
	USB/MSC_CDC/usbd_msc_cdc.h
)
ADD_LIBRARY(USB STATIC ${USB_SRC})

TARGET_INCLUDE_DIRECTORIES(USB PRIVATE
	USB/Core
	USB/CDC
	USB/MSC
	USB/MSC_CDC
)



###################
# CMSIS and HAL
# 
# Note: In order not to make yet another copy of CMSIS and HAL in the source tree I'll use
#       stm32generic's one for now. It seems it is pretty fresh and match the original
###################

SET(STM32_FAMILY_LONG_lx ${STM32_FAMILY_LONG_l}xx)
STRING(TOLOWER ${STM32_FAMILY_X} STM32_FAMILY_Xl)

SET(HAL_SRC
        STM32generic/system/${STM32_FAMILY_LONG}/CMSIS_Inc/${STM32_FAMILY_Xl}.h
        STM32generic/system/${STM32_FAMILY_LONG}/CMSIS_Inc/${STM32_FAMILY_LONG_lx}.h
        STM32generic/system/${STM32_FAMILY_LONG}/CMSIS_Inc/system_${STM32_FAMILY_LONG_lx}.h
        STM32generic/system/${STM32_FAMILY_LONG}/CMSIS_Src/startup_${STM32_FAMILY_Xl}.s

        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_adc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_adc_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_can.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_can_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_cec.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_conf.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_cortex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_crc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_dac.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_dac_ex.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_def.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_dma.h
        ##### FIXME: STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_dma_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_eth.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_flash.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_flash_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_gpio.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_gpio_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_hcd.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_i2c.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_i2s.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_irda.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_iwdg.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_mmc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_nand.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_nor.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_pccard.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_pcd.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_pcd_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_pwr.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_rcc.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_rcc_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_rtc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_rtc_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_sd.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_smartcard.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_spi.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_sram.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_tim.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_tim_ex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_uart.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_usart.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_hal_wwdg.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_adc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_bus.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_cortex.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_crc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_dac.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_dma.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_exti.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_fsmc.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_gpio.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_i2c.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_iwdg.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_pwr.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_rcc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_rtc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_sdmmc.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_spi.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_system.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_tim.h
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_usart.h
        #### FIXME: STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_usb.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_utils.h
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Inc/${STM32_FAMILY_LONG_lx}_ll_wwdg.h

        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_adc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_adc_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_can.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_cec.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_cortex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_crc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_dac.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_dac_ex.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_dma.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_eth.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_flash.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_flash_ex.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_gpio.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_gpio_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_hcd.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_i2c.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_i2s.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_irda.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_iwdg.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_mmc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_nand.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_nor.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_pccard.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_pcd.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_pcd_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_pwr.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_rcc.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_rcc_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_rtc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_rtc_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_sd.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_smartcard.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_spi.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_spi_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_sram.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_tim.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_tim_ex.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_uart.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_usart.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_hal_wwdg.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_adc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_crc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_dac.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_dma.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_exti.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_fsmc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_gpio.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_i2c.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_pwr.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_rcc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_rtc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_sdmmc.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_spi.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_tim.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_usart.c
        #### FIXME: STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_usb.c
        #STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/${STM32_FAMILY_LONG_lx}_ll_utils.c
        STM32generic/system/${STM32_FAMILY_LONG}/HAL_Src/system_${STM32_FAMILY_LONG_lx}.c
)

ADD_LIBRARY(HAL STATIC ${HAL_SRC})

TARGET_INCLUDE_DIRECTORIES(HAL PRIVATE

)

TARGET_COMPILE_DEFINITIONS(HAL PRIVATE
        -DVECT_TAB_OFFSET=${VECT_TAB_ADDR}
)

SET(LIBS_DIR            ${CMAKE_CURRENT_SOURCE_DIR}             PARENT_SCOPE)
