# 命令行工具使用说明

## 查看帮助信息
要查看 MinerU 命令行工具的帮助信息，可以使用 `--help` 参数。以下是各个命令行工具的帮助信息示例：
```bash
mineru --help
Usage: mineru [OPTIONS]

Options:
  -v, --version                   显示版本并退出
  -p, --path PATH                 输入文件路径或目录（必填）
  -o, --output PATH               输出目录（必填）
  -m, --method [auto|txt|ocr]     解析方法：auto（默认）、txt、ocr（仅用于 pipeline 后端）
  -b, --backend [pipeline|vlm-transformers|vlm-sglang-engine|vlm-sglang-client]
                                  解析后端（默认为 pipeline）
  -l, --lang [ch|ch_server|ch_lite|en|korean|japan|chinese_cht|ta|te|ka|th|el|latin|arabic|east_slavic|cyrillic|devanagari]
                                  指定文档语言（可提升 OCR 准确率，仅用于 pipeline 后端）
  -u, --url TEXT                  当使用 sglang-client 时，需指定服务地址
  -s, --start INTEGER             开始解析的页码（从 0 开始）
  -e, --end INTEGER               结束解析的页码（从 0 开始）
  -f, --formula BOOLEAN           是否启用公式解析（默认开启）
  -t, --table BOOLEAN             是否启用表格解析（默认开启）
  -d, --device TEXT               推理设备（如 cpu/cuda/cuda:0/npu/mps，仅 pipeline 后端）
  --vram INTEGER                  单进程最大 GPU 显存占用(GB)（仅 pipeline 后端）
  --source [huggingface|modelscope|local]
                                  模型来源，默认 huggingface
  --help                          显示帮助信息
```
```bash
mineru-api --help
Usage: mineru-api [OPTIONS]

Options:
  --host TEXT     服务器主机地址（默认：127.0.0.1）
  --port INTEGER  服务器端口（默认：8000）
  --reload        启用自动重载（开发模式）
  --help          显示此帮助信息并退出
```
```bash
mineru-gradio --help
Usage: mineru-gradio [OPTIONS]

Options:
  --enable-example BOOLEAN        启用示例文件输入(需要将示例文件放置在当前
                                  执行命令目录下的 `example` 文件夹中)
  --enable-sglang-engine BOOLEAN  启用 SgLang 引擎后端以提高处理速度
  --enable-api BOOLEAN            启用 Gradio API 以提供应用程序服务
  --max-convert-pages INTEGER     设置从 PDF 转换为 Markdown 的最大页数
  --server-name TEXT              设置 Gradio 应用程序的服务器主机名
  --server-port INTEGER           设置 Gradio 应用程序的服务器端口
  --latex-delimiters-type [a|b|all]
                                  设置在 Markdown 渲染中使用的 LaTeX 分隔符类型
                                  ('a' 表示 '$' 类型，'b' 表示 '()[]' 类型，
                                  'all' 表示两种类型都使用)
  --help                          显示此帮助信息并退出
```

## 环境变量说明

MinerU命令行工具的某些参数存在相同功能的环境变量配置，通常环境变量配置的优先级高于命令行参数，且在所有命令行工具中都生效。
以下是常用的环境变量及其说明： 

- `MINERU_DEVICE_MODE`：用于指定推理设备，支持`cpu/cuda/cuda:0/npu/mps`等设备类型，仅对`pipeline`后端生效。
- `MINERU_VIRTUAL_VRAM_SIZE`：用于指定单进程最大 GPU 显存占用(GB)，仅对`pipeline`后端生效。
- `MINERU_MODEL_SOURCE`：用于指定模型来源，支持`huggingface/modelscope/local`，默认为`huggingface`，可通过环境变量切换为`modelscope`或使用本地模型。
- `MINERU_TOOLS_CONFIG_JSON`：用于指定配置文件路径，默认为用户目录下的`mineru.json`，可通过环境变量指定其他配置文件路径。
- `MINERU_FORMULA_ENABLE`：用于启用公式解析，默认为`true`，可通过环境变量设置为`false`来禁用公式解析。
- `MINERU_TABLE_ENABLE`：用于启用表格解析，默认为`true`，可通过环境变量设置为`false`来禁用表格解析。

# 命令行参数进阶

## SGLang 加速参数优化

### 显存优化参数
> [!TIP]
> sglang加速模式目前支持在最低8G显存的Turing架构显卡上运行，但在显存<24G的显卡上可能会遇到显存不足的问题, 可以通过使用以下参数来优化显存使用：
> 
> - 如果您使用单张显卡遇到显存不足的情况时，可能需要调低KV缓存大小，`--mem-fraction-static 0.5`，如仍出现显存不足问题，可尝试进一步降低到`0.4`或更低
> - 如您有两张以上显卡，可尝试通过张量并行（TP）模式简单扩充可用显存：`--tp-size 2`

### 性能优化参数
> [!TIP]
> 如果您已经可以正常使用sglang对vlm模型进行加速推理，但仍然希望进一步提升推理速度，可以尝试以下参数：
> 
> - 如果您有超过多张显卡，可以使用sglang的多卡并行模式来增加吞吐量：`--dp-size 2`
> - 同时您可以启用`torch.compile`来将推理速度加速约15%：`--enable-torch-compile`

### 参数传递说明
> [!TIP]
> - 所有sglang官方支持的参数都可用通过命令行参数传递给 MinerU，包括以下命令:`mineru`、`mineru-sglang-server`、`mineru-gradio`、`mineru-api`
> - 如果您想了解更多有关`sglang`的参数使用方法，请参考 [sglang官方文档](https://docs.sglang.ai/backend/server_arguments.html#common-launch-commands)

## GPU 设备选择与配置

### CUDA_VISIBLE_DEVICES 基本用法
> [!TIP]
> - 任何情况下，您都可以通过在命令行的开头添加`CUDA_VISIBLE_DEVICES` 环境变量来指定可见的 GPU 设备：
>   ```bash
>   CUDA_VISIBLE_DEVICES=1 mineru -p <input_path> -o <output_path>
>   ```
> - 这种指定方式对所有的命令行调用都有效，包括 `mineru`、`mineru-sglang-server`、`mineru-gradio` 和 `mineru-api`，且对`pipeline`、`vlm`后端均适用。

### 常见设备配置示例
> [!TIP]
> 以下是一些常见的 `CUDA_VISIBLE_DEVICES` 设置示例：
>   ```bash
>   CUDA_VISIBLE_DEVICES=1  # Only device 1 will be seen
>   CUDA_VISIBLE_DEVICES=0,1  # Devices 0 and 1 will be visible
>   CUDA_VISIBLE_DEVICES="0,1"  # Same as above, quotation marks are optional
>   CUDA_VISIBLE_DEVICES=0,2,3  # Devices 0, 2, 3 will be visible; device 1 is masked
>   CUDA_VISIBLE_DEVICES=""  # No GPU will be visible
>   ```

## 实际应用场景

> [!TIP]
> 以下是一些可能的使用场景：
> 
> - 如果您有多张显卡，需要指定卡0和卡1，并使用多卡并行来启动`sglang-server`，可以使用以下命令： 
>   ```bash
>   CUDA_VISIBLE_DEVICES=0,1 mineru-sglang-server --port 30000 --dp-size 2
>   ```
>   
> - 如果您有多张显卡，需要指定卡0-3，并使用多卡数据并行和张量并行来启动`sglang-server`，可以使用以下命令： 
>   ```bash
>   CUDA_VISIBLE_DEVICES=0,1,2,3 mineru-sglang-server --port 30000 --dp-size 2 --tp-size 2
>   ```
>   
> - 如果您有多张显卡，需要在卡0和卡1上启动两个`fastapi`服务，并分别监听不同的端口，可以使用以下命令： 
>   ```bash
>   # 在终端1中
>   CUDA_VISIBLE_DEVICES=0 mineru-api --host 127.0.0.1 --port 8000
>   # 在终端2中
>   CUDA_VISIBLE_DEVICES=1 mineru-api --host 127.0.0.1 --port 8001
>   ```