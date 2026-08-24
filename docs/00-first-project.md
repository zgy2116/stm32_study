# 第一个工程：GPIO 控制 LED

这份清单用于完成第一个可复现的 STM32F103C8T6 实验。不要直接复制别人的 LED 引脚：先查看你的开发板原理图、丝印或商品说明。

## 1. 先确认工具链

在 VSCode 的终端执行：

```bash
arm-none-eabi-gcc --version
```

如果提示找不到命令，先把 Arm GNU Toolchain 的 `bin` 目录加入系统 `PATH`，再重启 VSCode。

## 2. 用 CubeMX 创建工程

1. 新建工程，选择 `STM32F103C8Tx`。
2. 在 `SYS > Debug` 选择 `Serial Wire`，否则下载后可能无法继续调试。
3. 根据板卡原理图把 LED 所在引脚设置为 `GPIO_Output`。若暂时没有板载 LED，可接一个限流电阻和 LED 到任意 GPIO。
4. 在 `Clock Configuration` 中配置系统时钟。常见 Blue Pill 使用 8 MHz 外部晶振，系统时钟为 72 MHz；没有外部晶振时应按实际硬件选择。
5. 在 `Project Manager` 中填写工程名和路径，工具链选择与你本机一致的 Makefile 或 CMake，然后点击 `Generate Code`。
6. 将生成的工程放到 `examples/01_gpio_led/`，保留 `.ioc`、`Core/`、`Drivers/` 和构建配置文件。

## 3. 编写最小功能

在 `main.c` 的主循环中调用 HAL GPIO 翻转函数，并加入延时。CubeMX 生成的用户代码区域通常位于 `/* USER CODE BEGIN */` 和 `/* USER CODE END */` 之间，代码应只写在这些区域内，这样重新生成代码时不容易丢失。

LED 的有效电平取决于接法：有些板卡 `GPIO_PIN_RESET` 点亮，有些板卡 `GPIO_PIN_SET` 点亮。若现象相反，先确认接线和有效电平，再修改逻辑。

## 4. 编译、下载、验证

在工程目录执行 CubeMX 生成的构建命令（例如 `make`），确认没有错误后，用 VSCode 的调试配置或 STM32CubeProgrammer 通过 ST-Link 下载。验证 LED 是否按固定周期闪烁，并记录实际引脚、时钟和工具链版本。

## 5. 记录并提交

在同目录新增 `README.md`，至少记录：

- 实验目的和日期
- 开发板型号、LED 引脚和有效电平
- CubeMX 关键配置和系统时钟
- 编译/下载方式
- 实际现象和遇到的问题

确认源码和 `.ioc` 可以重新生成后提交：

```bash
git add examples/01_gpio_led
git commit -m "feat: add GPIO LED example"
git push origin main
```

不要提交 `build/`、`Debug/`、`.elf`、`.hex` 等构建产物；仓库根目录的 `.gitignore` 已经覆盖常见情况。
