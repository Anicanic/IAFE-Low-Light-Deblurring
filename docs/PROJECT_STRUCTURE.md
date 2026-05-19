# IAFE GitHub 项目结构建议

本文档用于说明当前仓库中每个文件夹应该包含什么内容，方便后续逐步补充代码、模型、结果和项目主页。

## 根目录

- `README.md`
  - 项目首页说明。
  - 应包含论文题目、作者、摘要、方法亮点、主要结果、使用方法、数据集说明、引用信息和更新计划。
- `2026165663.pdf`
  - 当前论文 PDF。
  - 建议后续重命名为 `paper/IAFE.pdf` 或在根目录保留 `IAFE.pdf`，使文件名更直观。
- `requirements.txt`
  - 后续添加 Python 依赖，例如 PyTorch、OpenCV、NumPy、tqdm、scikit-image、lpips 等。
- `.gitignore`
  - 排除数据集、权重、缓存、实验输出等大文件。
- `LICENSE`
  - 明确代码开源协议。常用选择为 MIT、Apache-2.0 或仅研究用途许可证。

## `configs/`

用于存放训练和测试配置文件。

建议内容：

- `iafe_lolblur.yaml`
  - LOL-Blur 训练配置。
  - 包含数据路径、batch size、crop size、学习率、优化器、训练迭代数、loss 权重等。
- `iafe_eval.yaml`
  - 通用测试配置。
- `ablation/`
  - 消融实验配置，例如去掉光照建模、去掉频率模块、去掉边缘约束等。

## `data/`

本地数据集目录，不建议提交到 GitHub。

建议结构：

```text
data/
  LOL-Blur/
    train/
      input/
      target/
    test/
      input/
      target/
  LOL-v1/
  LOL-v2/
  RealBlur/
```

应提交的内容：

- `data/README.md`
  - 数据集下载链接、放置路径和预处理说明。
- `.gitkeep`
  - 保留空目录。

不应提交的内容：

- 原始图片数据。
- 大规模中间缓存。
- 数据集压缩包。

## `docs/`

用于存放项目文档。

建议内容：

- `PROJECT_STRUCTURE.md`
  - 当前文件，解释仓库结构。
- `DATASETS.md`
  - 数据集下载、目录组织、训练/测试划分说明。
- `REPRODUCTION.md`
  - 复现实验步骤，包括环境、训练、测试和指标计算。
- `TODO.md`
  - 项目发布任务清单。
- `CHANGELOG.md`
  - 后续记录每次公开更新。

## `figures/`

用于放置论文图和 GitHub 展示图。

建议内容：

- `architecture.png`
  - IAFE 网络结构图，对应论文 Fig. 1。
- `visual_comparison.png`
  - 低光运动模糊可视化对比，对应论文 Fig. 2。
- `training_curves.png`
  - 长期训练曲线，对应论文 Fig. 3。
- `teaser.png`
  - GitHub README 顶部展示图，可由输入、结果、GT 拼接而成。

注意：

- 图片建议压缩后上传。
- 如果论文图来自 PDF，应确保拥有展示权限。

## `models/`

用于存放神经网络模型定义。

建议内容：

- `iafe.py`
  - IAFE 主网络。
- `illumination.py`
  - 光照分解分支与光照调制模块。
- `frequency.py`
  - 频率感知高频增强模块。
- `edge.py`
  - 结构边缘相关模块。
- `backbone.py`
  - 主干网络或基线网络封装。

## `src/`

用于存放项目核心工具代码。

建议内容：

- `datasets/`
  - LOL-Blur、LOL-V1、LOL-V2、RealBlur 的数据加载器。
- `losses/`
  - 像素损失、感知损失、光照平滑损失、重建一致性损失、边缘一致性损失。
- `metrics/`
  - PSNR、SSIM、LPIPS 计算。
- `utils/`
  - 日志、随机种子、模型保存、图像读写、配置解析等工具。
- `engine/`
  - 训练循环、验证循环、测试循环。

## `scripts/`

用于存放命令行入口脚本。

建议内容：

- `train.py`
  - 训练入口。
- `evaluate.py`
  - 测试并输出 PSNR/SSIM/LPIPS。
- `infer.py`
  - 对单张图片或文件夹进行推理。
- `prepare_data.py`
  - 可选的数据预处理脚本。
- `export_results.py`
  - 可选的可视化结果导出脚本。

## `tests/`

用于存放最小测试。

建议内容：

- `test_model_forward.py`
  - 检查模型能否前向传播。
- `test_losses.py`
  - 检查损失函数输出是否正常。
- `test_metrics.py`
  - 检查指标计算。
- `test_dataloader.py`
  - 检查数据加载维度和配对关系。

## `results/`

用于存放本地实验输出，不建议提交大文件。

建议内容：

- `demo/`
  - 少量演示结果。
- `lolblur/`
  - LOL-Blur 测试输出。
- `tables/`
  - 指标表格，例如 CSV 或 Markdown。

不建议提交：

- 大规模推理图片。
- 重复实验日志。
- TensorBoard 大文件。

## `checkpoints/`，后续可创建

用于存放模型权重。

建议内容：

- `iafe_lolblur.pth`
  - LOL-Blur 训练权重。
- `README.md`
  - 权重下载链接和校验信息。

注意：

- 权重通常不要直接提交到 GitHub。
- 建议用 GitHub Release、Google Drive、Hugging Face 或学校服务器发布。

