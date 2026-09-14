# 易语言目录工程

本目录由 [e-packager](https://github.com/aiqinxuancai/e-packager) 从 `Aurora.Console.e` 解包生成，可使用 Git 管理版本、查看代码 Diff，并通过外部编辑器或 AI 辅助编辑后回包。

## 目录结构

| 路径 | 说明 |
| --- | --- |
| `src/` | 源码目录。普通程序集、类、窗口程序集使用 `.txt` 保存；窗口界面定义使用同名 `.xml` 保存。 |
| `src/.数据类型.txt` | 数据类型定义。 |
| `src/.DLL声明.txt` | DLL 声明。 |
| `src/.常量.txt` | 常量定义。 |
| `src/.全局变量.txt` | 全局变量定义。 |
| `project/` | 封包所需元数据与原生快照，请勿随意删除。 |
| `ecom/` | 当前工程引用的易模块工作区副本，仅供查阅、检索与辅助编辑。 |
| `elib/` | 当前工程依赖支持库的公开接口导出文本，仅供查阅与 AI 理解，不参与回包。 |
| `image/` | 图片资源 / 二进制资源及 `list.json`。 |
| `audio/` | 音频资源 / 二进制资源及 `list.json`。 |
| `tool/` | 当前目录自带的 `e-packager.exe`。 |
| `pack/` | 默认回包输出目录，首次回包时生成。 |
| `README.md` | 项目结构与回包入门说明。 |
| `AGENTS.md` | 供 AI Agent 使用的源码编辑规则与操作说明。 |
| `info.json` | 记录本目录来源 `.e` 的文件名、路径、类型、修改时间、尺寸、MD5。 |

依赖辅助目录按工程类型和解包选项生成，部分目录可能不存在。

## 编辑项目

直接修改 `src/` 中的 `.txt` 源码和 `.xml` 窗口定义；新增程序集或类可在 `src/` 下新增 `.txt`，回包时自动扫描。数据类型、DLL 声明、常量和全局变量应保留在各自固定文件中。

保留 `project/` 元数据与原生快照。完整的易语言语法、声明格式及新增程序集、类、窗口规则见 [AGENTS.md](AGENTS.md)。

## 回包方法

在本目录打开 PowerShell，使用随目录附带的工具：

```powershell
# 检查编辑后的源码
.\tool\e-packager.exe validate .

# 默认回包到 pack/，文件名由 info.json 决定
.\tool\e-packager.exe

# 显式指定输出文件
.\tool\e-packager.exe pack . ".\pack\Aurora.Console.e"
```

也可以直接运行 `tool/e-packager.exe` 无参回包。`pack` 会自动执行源码预检；回包得到的是易语言工程或模块文件，不是可执行程序。预检通过不等于 IDE 编译成功，生成的 `.e` 仍需在易语言 IDE 中打开并编译。

## 更新依赖与资源

以下命令在本目录执行，路径请替换为实际文件：

```powershell
.\tool\e-packager.exe update . --add-ecom "D:\modules\示例.ec"
.\tool\e-packager.exe update . --add-image "启动画面=D:\res\logo.png"
.\tool\e-packager.exe update . --add-audio "提示音=D:\res\notify.wav"
```

图片、音频及其它二进制资源都是常量资源，代码中以 `#资源名` 引用。`image/list.json` 与 `audio/list.json` 记录资源名称及文件路径；不要只把文件放进目录而不更新索引。`update` 完成后仍需执行回包。
