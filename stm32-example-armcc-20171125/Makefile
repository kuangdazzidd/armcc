# powered by ralfak 20140410
# this is just a makefile for keil armcc
#first you should set enviroment variable ,then you can use armcc arm asm and armlink
#if you want get hen taget.hex ,you should use fromelf 

RM := rm -rf
Target = gpio

# All Target
all: $(Target).axf $(Target).elf $(Target).hex

CC =armcc

CFLAGS = -c --cpu Cortex-M3 -g -O0 --apcs=interwork --asm --interleave --asm_dir="List" \
-ISource/FWLib/inc \
-ISource \
--output_dir="Obj" --depend_dir="Obj" --md --list_dir "List" --list \
-DSTM32F10X_HD 

#asm options
AS = armasm
ASFLAGS = --cpu Cortex-M3 -g --apcs=interwork \
--xref \
--md --list=

#linker options
LD = armlink
LDFLAGS = --cpu Cortex-M3  \
--strict --scatter ".\Source\GPIO.sct" \
--summary_stderr --info summarysizes --map --xref --callgraph --symbols \
--info sizes --info totals --info unused --info veneers \
--list $(Target).map 

#dump options
DUMP = fromelf
DUMPFLAGS = --cpu Cortex-M3 --i32combined --info=sizes,totals
#fromelf --cpu cortex-m3 --i32 --info=sizes,totals gpio.elf  --output=gpio.hex 

#source
C_SRCS += \
Source/main.c \
Source/stm32f10x_it.c 

OBJS += \
OBJ/main.o \
OBJ/stm32f10x_it.o 

 
C_DEPS += \
OBJ/main.d \
OBJ/stm32f10x_it.d 

LST += \
List/main.lst \
List/stm32f10x_it.lst

TXT += \
List/main.txt \
List/stm32f10x_it.txt


C_SRCS += \
Source/FWLib/src/stm32f10x_flash.c \
Source/FWLib/src/stm32f10x_gpio.c \
Source/FWLib/src/stm32f10x_nvic.c \
Source/FWLib/src/stm32f10x_rcc.c 

OBJS += \
OBJ/stm32f10x_flash.o \
OBJ/stm32f10x_gpio.o \
OBJ/stm32f10x_nvic.o \
OBJ/stm32f10x_rcc.o 


C_DEPS += \
OBJ/stm32f10x_flash.d \
OBJ/stm32f10x_gpio.d \
OBJ/stm32f10x_nvic.d \
OBJ/stm32f10x_rcc.d 

LST += \
List/stm32f10x_flash.lst \
List/stm32f10x_gpio.lst \
List/stm32f10x_nvic.lst \
List/stm32f10x_rcc.lst 

TXT += \
List/stm32f10x_flash.txt \
List/stm32f10x_gpio.txt \
List/stm32f10x_nvic.txt \
List/stm32f10x_rcc.txt 

ASM_SRCS += \
Source/Startup/cortexm3_macro.s \
Source/Startup/stm32f10x_vector.s

ASM_OBJ = \
OBJ/cortexm3_macro.o \
OBJ/stm32f10x_vector.o 

OBJS += \
OBJ/cortexm3_macro.o \
OBJ/stm32f10x_vector.o 

ASM_DEPS += \
cortexm3_macro.d \
stm32f10x_vector.d 

LST += \
cortexm3_macro.lst \
stm32f10x_vector.lst 




# Each subdirectory must supply rules for building sources it contributes
OBJ/%.o: Source/%.c
#OBJ/$(NEWOBJ).o : Source/$(NEWOBJ).c
	@echo 'Building file: $<'
	@echo 'Invoking: Cross ARM C Compiler'
	$(CC) $(CFLAGS)  "$<"
	@echo 'Finished building: $<'
	@echo ' '

# Each subdirectory must supply rules for building sources it contributes
OBJ/%.o: Source/FWLib/src/%.c
	@echo 'Building file: $<'
	@echo 'Invoking: Cross ARM C Compiler'
	$(CC) $(CFLAGS) "$<"
	@echo 'Finished building: $<'
	@echo ' '
#	$(CC) $(CFLAGS) --depend=.d  -o "$@" "$<"	
OBJ/%.o: Source/Startup/%.s
	@echo 'Building file: $<'
	@echo 'Invoking: Cross ARM C Compiler'
	$(AS) $(ASFLAGS)  -o "$@" "$<"
	@echo 'Finished building: $<'
	@echo ' '	

# Tool invocations
$(Target).axf: $(OBJS)
	@echo 'Building target: $@'
	@echo 'Invoking: Cross ARM C Linker'
	$(LD) $(LDFLAGS) -o "$@" $(OBJS) 
	@echo 'Finished building target: $@'
	@echo ' '
$(Target).elf: $(OBJS)
	@echo 'Building target: $@'
	@echo 'Invoking: Cross ARM C Linker'
	$(LD) $(LDFLAGS) -o "$@" $(OBJS) 
	@echo 'Finished building target: $@'
	@echo ' '

#make target.hex	
$(Target).hex : $(Target).axf
	@echo 'Building hex: $@'
	@echo 'Invoking: Cross ARM fromelf'
	$(DUMP) $(DUMPFLAGS) $(Target).axf --output=$(Target).hex
	@echo 'Finished building target: $@'
	@echo ' '

# Other Targets
clean:
	-$(RM) $(OBJS)$(C_DEPS)$(ASM_DEPS)$(LST)$(TXT) $(Target).axf $(Target).elf $(Target).hex $(Target).map
	-@echo ' '



