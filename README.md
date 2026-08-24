# STM32F103C8T6 学习记录

这是一个从零开始学习 STM32F103C8T6 的仓库，用来保存 CubeMX 配置、实验代码、学习笔记和问题排查记录。每完成一个可以复现的实验，就在 Git 中留下一个清晰的提交。

## 项目目标

- 整理 STM32 学习过程
- 保存实验代码
- 记录开发过程中遇到的问题
- 积累嵌入式开发经验
- 使用 GitHub 备份和分享代码

## 学习路线

建议按下面的顺序学习，每一项都先完成“能运行的最小实验”，再扩展功能：

1. GPIO：LED、按键、软件消抖
2. 外部中断：按键中断和中断服务函数
3. 定时器：定时中断、输入捕获
4. USART：串口打印和接收命令
5. PWM：呼吸灯、舵机
6. ADC：电位器采样和数据换算
7. I2C / SPI：连接传感器或 OLED
8. DMA：串口或 ADC 的高效数据传输
9. 看门狗、低功耗和错误处理
10. 综合项目：把多个外设组合起来

FreeRTOS 放在裸机外设和中断基础扎实之后学习。

## 目录说明

- `docs/`：学习笔记和问题记录
- `projects/`：完整的 STM32 项目工程
- `examples/`：独立的小实验
- `hardware/`：开发板、接线和硬件资料

## 开发环境

- 单片机：STM32F103C8T6
- 配置工具：STM32CubeMX
- 编辑器：Visual Studio Code
- 编译器：Arm GNU Toolchain（`arm-none-eabi-gcc`，请在本机确认版本）
- 构建方式：CubeMX 生成的 CMake
- 调试器：ST-Link（SWD）
- 开发板：STM32F103C8T6 开发板（板型待确认）
- 首个实验硬件：板载 LED 为 PC13，低电平点亮；PA0 配置为上拉输入

首次使用前，请确认 VSCode 终端能找到 `arm-none-eabi-gcc`，并能使用 ST-Link 或 OpenOCD 连接芯片。

## 当前项目状态

- [x] 创建基础目录结构
- [x] 完成 GPIO LED 实验
- [ ] 上传第一个 STM32 工程
- [x] 补充 LED 引脚和调试器信息
- [x] 开始记录学习笔记
- [ ] 创建第一个 Issue

## 后续计划

每学习一个新的 STM32 模块，就在 `examples/` 或 `projects/` 中创建对应目录，并记录实验目的、硬件连接、代码功能、运行结果和遇到的问题。第一次实验可直接参考 [`docs/00-first-project.md`](docs/00-first-project.md)。

## GitHub 记录方式

保留 `.ioc` 文件和源码，忽略 `build/`、`Debug/`、`.elf`、`.hex` 等可重新生成的文件。每完成一个小目标就提交一次，例如：

```bash
git add README.md docs/ examples/ projects/
git commit -m "feat: add GPIO LED example"
git push origin main
```

提交信息尽量描述结果，而不是描述过程，例如 `docs: record USART baud rate issue`。
