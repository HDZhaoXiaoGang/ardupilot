# STM32F405FC Flight Controller

基于STM32F405RGT6微控制器的自定义飞控板配置，专为无人机和固定翼飞机设计。

## 硬件规格

### MCU
- **型号**: STM32F405RGT6
- **架构**: ARM Cortex-M4 
- **主频**: 168MHz
- **Flash**: 1MB
- **RAM**: 192KB
- **封装**: LQFP64

### 传感器
- **IMU**: MPU6500 (SPI1)
- **气压计**: SPL06 (I2C1)
- **磁力计**: QMC5883L (I2C1)
- **OSD**: AT7456E (SPI2)

## 引脚分配

### PWM输出 (7路)
| 端口 | 引脚 | 定时器 | 功能 |
|------|------|--------|------|
| S1   | PB3  | TIM2_CH2 | PWM输出1 |
| S2   | PB4  | TIM3_CH1 | PWM输出2 |
| S3   | PB5  | TIM3_CH2 | PWM输出3 |
| S4   | PB8  | TIM4_CH3 | PWM输出4 |
| S5   | PB9  | TIM4_CH4 | PWM输出5 |
| S6   | PA0  | TIM2_CH1 | PWM输出6 |
| S7   | PA1  | TIM2_CH2 | PWM输出7 (已禁用) |

### 备用电机控制端口
| 端口 | 引脚 | 定时器 | 功能 |
|------|------|--------|------|
| MS1  | PB0  | TIM3_CH3 | PWM输出8 |
| MS2  | PB1  | TIM3_CH4 | PWM输出9 |
| MS3  | PC9  | TIM8_CH4 | PWM输出10 |
| MS4  | PA8  | TIM1_CH1 | PWM输出11 |

### 串口配置
| 串口 | TX引脚 | RX引脚 | 默认协议 | 波特率 |
|------|--------|--------|----------|--------|
| USART1 | PA9  | PA10 | MAVLink | 57600 |
| USART2 | PA2  | PA3  | GPS     | 38400 |
| USART3 | PB10 | PB11 | 用户配置 | 57600 |
| UART4  | PC10 | PC11 | 用户配置 | 57600 |
| UART5  | PC12 | PD2  | RC输入   | 420000 |
| USART6 | PC6  | PC7  | 用户配置 | 57600 |

### SPI接口
| SPI | SCK | MISO | MOSI | CS引脚 | 设备 |
|-----|-----|------|------|--------|------|
| SPI1 | PA5 | PA6  | PA7  | PA4    | MPU6500 |
| SPI2 | PB13| PB14 | PB15 | PB12   | AT7456E |

### I2C接口
| I2C | SCL | SDA | 设备 |
|-----|-----|-----|------|
| I2C1 | PB6 | PB7 | SPL06, QMC5883L |

### 模拟输入
| 功能 | 引脚 | ADC通道 |
|------|------|---------|
| 电池电压 | PC4 | ADC1_CH14 |
| 电池电流 | PC5 | ADC1_CH15 |

### 指示灯
| LED | 引脚 | 功能 |
|-----|------|------|
| LED_FC | PC13 | 飞控状态指示 |
| LED_LXB | PC14 | 用户自定义 |

### 其他引脚
| 功能 | 引脚 | 说明 |
|------|------|------|
| MPU6500_EXTL | PC3 | 陀螺仪外部中断 |
| USB_DM | PA11 | USB数据- |
| USB_DP | PA12 | USB数据+ |
| SWDIO | PA13 | SWD调试数据 |
| SWCLK | PA14 | SWD调试时钟 |

## 编译说明

使用以下命令编译固件：

```bash
cd ardupilot
./waf configure --board STM32F405FC
./waf plane
```

生成的固件文件位于：`build/STM32F405FC/bin/arduplane.hex`

## 功能特性

- ✅ 6路PWM输出（标准伺服/电调控制，S7已禁用）
- ✅ 4路备用PWM输出（MS1-MS4）
- ✅ 6路UART（含USB）
- ✅ MPU6500陀螺仪/加速度计
- ✅ SPL06气压计
- ✅ QMC5883L磁力计
- ✅ AT7456E OSD芯片
- ✅ 电池电压/电流监测
- ✅ LED状态指示
- ✅ USB连接支持
- ✅ SWD调试接口

## 适用场景

- 固定翼飞机
- 多旋翼无人机
- VTOL飞行器
- 遥控飞机
- 实验性飞行平台

## 注意事项

1. **电源供电**: 确保为飞控板提供稳定的5V/3.3V电源
2. **传感器连接**: I2C设备需要正确的上拉电阻
3. **PWM频率**: 默认支持50Hz-400Hz PWM输出
4. **调试接口**: 可通过SWD接口进行固件调试
5. **备用端口**: MS1-MS4可用于额外的控制功能

## 版本信息

- ArduPilot版本: 4.6.2+
- 硬件版本: v1.0
- 创建日期: 2024