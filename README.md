# The-principle-of-vscode
讲解vscode的神奇文件launch.json和tasks.json

# 1. version: "0.2.0"
这是配置文件的版本号。每个版本都有其特定的格式和功能，VS Code 使用这个字段来确定如何解析和加载配置文件。
# 2. configurations:
这个数组包含了不同的调试配置。每个配置代表一种调试环境设置。你可以在这里添加多个配置项。
# 3. 配置项（name, type, request, 等）:
## name: "gcc.exe - 生成和调试活动文件"
该字段是你为调试配置指定的名称。在 VS Code 的调试面板中会显示这个名称，便于选择和启动调试会话。

type: "cppdbg"
该字段指定了调试器的类型。这里使用的是 cppdbg，表示 C++ 调试器（cppdbg 是 C++ 调试器的 VS Code 调试器类型，适用于 C++ 项目）。

request: "launch"
这个字段指定调试的请求类型。launch 表示启动调试会话，而 attach 表示附加到正在运行的进程。

program: "${fileDirname}\\${fileBasenameNoExtension}.exe"
这个字段指定了要调试的程序路径。${fileDirname} 是当前文件所在的目录，${fileBasenameNoExtension} 是文件名（不包括扩展名），这意味着它会调试与当前文件同名的 .exe 文件。对于 Windows 系统，这里使用了 \\ 作为路径分隔符。

args: []
该字段是一个空数组，表示没有额外的命令行参数传递给程序。如果需要传递参数，可以在此数组中指定。

stopAtEntry: false
该字段设置为 false 表示程序在启动时不会在 main() 函数处停下来。如果设置为 true，则调试器会在程序入口处暂停，便于开发者检查初始状态。

cwd: "${fileDirname}"
设置当前工作目录（cwd）为当前文件的目录。这样可以确保程序启动时在正确的目录下运行。

environment: []
这个字段是一个空数组，表示没有设置任何环境变量。如果需要在调试过程中设置环境变量，可以将其添加到数组中。

externalConsole: true
这个字段设置为 true 表示启动调试时使用外部控制台（终端）。这意味着输出将显示在一个独立的命令行窗口中，而不是在 VS Code 的内部终端中。

MIMode: "gdb"
该字段指定了调试器的模式，gdb 表示使用 GNU 调试器（GDB）进行调试。

miDebuggerPath: "E:\\soft\\mingw\\mingw64\\bin\\gdb.exe"
该字段指定 GDB 调试器的路径。这里使用的是 mingw64 中的 gdb.exe，并指定了它的完整路径。

# 4. setupCommands:
这部分定义了一些调试器的设置命令，在调试会话开始时会自动执行。

description: "为 gdb 启用整齐打印"
描述命令的作用，这里是启用 GDB 的整齐打印（pretty printing）功能，使得打印结构体等数据时更加易读。

text: "-enable-pretty-printing"
这是 GDB 命令，启用整齐打印。

ignoreFailures: true
如果这个命令失败，调试器不会中断执行。true 表示即使命令执行失败也不会影响调试流程。

description: "将反汇编风格设置为 Intel"
设置反汇编输出的风格为 Intel 风格，而不是默认的 AT&T 风格，Intel 风格的汇编指令更为常见和易于理解。

text: "-gdb-set disassembly-flavor intel"
这是 GDB 命令，设置反汇编风格为 Intel。

# 5. preLaunchTask: "C/C++: gcc.exe 生成活动文件"
这个字段指定在启动调试会话之前执行的任务。在这里，它指向一个名为 C/C++: gcc.exe 生成活动文件 的任务，通常是编译任务，用来编译当前的 C/C++ 文件并生成可执行文件。这个任务需要在 tasks.json 文件中定义。
