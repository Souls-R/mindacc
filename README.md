# MindAcc

MindAcc 是一个用于对比 MindSpore Lite 与 ONNX 模型推理结果的工具，支持模型转换、随机输入生成、推理运行、对比分析等功能。

onnx 模型中间输出的 dump 能力亦开源并发布在PyPI作为本项目依赖，项目仓库 [onnxdumper](https://gitee.com/noiatrio/onnxdumper)，PyPI地址 [onnxdumper](https://pypi.org/project/onnxdumper/)。

## 演示视频、设计文档、PPT

[README.assets/vedio.mp4](https://gitee.com/noiatrio/mindacc/blob/master/README.assets/vedio.mp4)

[README.assets/mindacc.doc](https://gitee.com/noiatrio/mindacc/blob/master/README.assets/mindacc%E5%BC%80%E5%8F%91%E8%AE%BE%E8%AE%A1%E6%96%87%E6%A1%A3.docx)

[README.assets/mindacc.pptx](https://gitee.com/noiatrio/mindacc/blob/master/README.assets/mindacc.pptx)

## 安装

1. 克隆仓库：
    ```sh
    git clone https://gitee.com/noiatrio/mindacc
    cd mindacc
    ```

2. 安装 python 依赖：

    使用 `python venv`：
    ```sh
    python -m venv mindacc
    source mindacc/bin/activate
    pip install -r requirements.txt
    ```

    使用 `conda`：
    ```sh
    conda env create -f environment.yml
    conda activate mindacc
    ```

3. 获取 `mslite` 运行环境：

    - 下载 [MindSpore Lite 端侧运行环境](https://www.mindspore.cn/lite/docs/zh-CN/master/use/downloads.html)（包含convert与带导出功能的benchmark工具），将 `mindspore-lite-2.3.1-linux-x64` 置于当前目录下即可。
    - 相关环境变量将只在 `main.ipynb` 中自动设置，并在 `mindacc` 运行的python环境中生效，无需手动设置。
    - 环境变量设置详细信息请参考 [convert](https://www.mindspore.cn/lite/docs/zh-CN/master/train/converter_train.html)， [benchmark](https://www.mindspore.cn/lite/docs/zh-CN/master/tools/benchmark_tool.html#dump功能)。

## 使用方法
运行 `main.ipynb`：
    - 使用 Jupyter Notebook 或 Jupyter Lab 打开 `main.ipynb` 文件。
    - 点击“运行所有”按钮运行所有代码单元格。
    - 在浏览器中打开 Gradio 界面，即可使用 MindAcc 工具。

## 主要功能

- **模型转换**：支持将 ONNX 模型转换为 MindSpore Lite 模型。
- **随机输入生成**：自动生成随机输入数据。
- **推理运行**：运行 MindSpore Lite 和 ONNX 模型推理。
- **对比分析**：对比推理结果，支持多种分析指标，支持可视化对比结果。
- **自定义映射**：支持自定义算子映射。

## 示例
![img1](README.assets/image1.png)
![img2](README.assets/image2.png)
![img3](README.assets/image3.png)
![img4](README.assets/image4.png)

## 目录结构

```
mindacc
├─ .gitignore
├─ LICENSE
├─ mindspore-lite-2.3.1-linux-x64   // MindSpore Lite 端侧运行环境
├─ input                            // 模型输入数据
├─ output                           // 模型输出数据
├─ model                            // 模型文件
├─ README.assets                    // README.md 图片等资源
├─ README.md                        // 项目说明文档
├─ environment.yml                  // conda 环境配置文件
├─ main.ipynb                       // 主程序
└─ requirements.txt                 // python 依赖
```

```
main.ipynb 
├─ Import & Config                      // 导入模块与配置
│  ├─ import            // 导入模块            
│  ├─ logger            // 日志配置
│  └─ mslite_config     // MindSpore Lite 环境配置
├─ Class MindAcc Model                  // 模型管理
│  ├─ load              // 加载模型
│  ├─ run_ms_converter  // 运行模型转换
│  ├─ input_generate    // 生成随机输入
│  ├─ input_load        // 加载输入数据
│  ├─ run_ms_dump       // 运行 MindSpore Lite 推理
│  └─ run_onnx_dump     // 运行 ONNX 推理
├─ Class MindAcc Mapper                 // 映射器
│  ├─ get_ms_bin_info   // 获取 mslite 输出文件信息
│  ├─ read_ms_output    // 读取 mslite 输出文件夹
│  ├─ simple_map        // 简单映射
│  └─ get_map_result    // 获取映射结果
├─ Class MindAcc Analyzer               // 分析器
│  ├─ cosine_similarity // 余弦相似度
│  ├─ relative_euclidean_distance   // 相对欧氏距离
│  ├─ max_absolute_error    // 最大绝对误差
│  ├─ mean_absolute_error   // 平均绝对误差
│  ├─ root_mean_square_error    // 均方根误差
│  ├─ max_relative_error    // 最大相对误差
│  ├─ mean_relative_error   // 平均相对误差
│  ├─ accumulated_relative_error    // 累积相对误差
│  ├─ standard_deviation    // 标准差
│  └─ kullback_leibler_divergence   // KL散度
└─ Gradio Interface                     // Gradio 界面
   ├─ process_model         // 函数绑定
   ├─ process_input
   ├─ random_input
   ├─ run_infer
   ├─ run_map
   ├─ run_compare
   ├─ gr.Blocks             // Gradio 布局组件
   └─ launch                // Gradio 启动
```
## 许可证

本项目基于 MIT 许可证，详情请参阅 [LICENSE](LICENSE) 文件。

## 贡献

欢迎贡献代码！请提交 Pull Request 或报告 Issue。
