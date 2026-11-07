# led

LibXR / STM32F407 的 LED 示例工程，`User/app_main.cpp` 由 CodeGenerator（`libxr`）生成。

## 首次 clone 后

1. 用 VS Code 打开仓库根目录的 `XROBOT_demo.code-workspace`，或直接打开 `led/` 文件夹。
   不要打开仓库根目录后直接 F5：`launch.json` 里的 `build/Debug/led.elf` 是相对 `led/` 的。
2. 安装 STM32CubeCLT / STM32 VS Code 扩展（本工程默认使用 `cube-cmake` 和 `cube`），并确认 `arm-none-eabi-gcc`、`cmake`、`ninja` 可用。
3. 配置并构建 Debug preset：
   - 推荐：VS Code 命令面板执行 `CMake: Configure`（选择 `Debug`），再执行 `CMake: Build`；
   - 命令行（`cmake` 在 PATH 时）：`cmake --preset Debug`，然后 `cmake --build --preset Debug`。
4. 按 F5 启动 `Debug led (OpenOCD)`。

`build/` 被 `.gitignore` 忽略，clone 后不会自带 `led.elf`，必须先构建。

## 调试工具路径

`launch.json` 不写死 OpenOCD / GDB 路径。每台机器在 VS Code **用户设置**（不是工作区设置）里配置一次：

```jsonc
{
  "cortex-debug.openocdPath": "C:/path/to/openocd.exe",
  "cortex-debug.armToolchainPath": "C:/path/to/arm-none-eabi/bin"
}
```

也可以把 `openocd.exe` 和 `arm-none-eabi-gdb.exe` 加入 PATH，然后不配置这两项。

如果 OpenOCD 找不到 `interface/cmsis-dap.cfg` / `target/stm32f4x.cfg`，在 `launch.json` 的配置里临时加：

```jsonc
"searchDir": ["C:/path/to/openocd/openocd/scripts"]
```

`interface/cmsis-dap.cfg` 对应 CMSIS-DAP 调试器；如果使用 ST-Link，改成 `interface/stlink.cfg`。
