深度学习YOLOV8模型如何训练智慧化煤矿井下矿井开采异常检测数据集 检测识别煤矿工作人员检测 大煤块检测 采煤机拖揽检测 矿工不安全行为检测，安全帽佩戴检测
@[toc]
6大类别：
1煤矿工作人员检测
2.液压支撑防护板检测（液压支撑防护板所有角度如防护板0到30度，30度到60…等多角度检测，防护板异常等）
3.大煤块检测
4.采煤机拖揽检测
5.矿工不安全行为检测（行走，站立，坐下，操作，弯腰，依靠，摔倒，爬行）
6.安全帽佩戴检测
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7822167f971a40f2a2bcb30513168168.png)

### ⛏️ **煤矿井下开采异常检测数据集（Smart Mine Intelligent Analysis Dataset）**

| **项目** | **详细信息** |
|----------|--------------|
| **数据集名称** | 煤矿井下智能分析多目标检测数据集 |
| **应用场景** | 智慧矿井、AI安全监管、自动化巡检、事故预防 |
| **图像总数** | **130,000 张**（真实煤矿井下拍摄） |
| **图像来源** | 国内多个大型煤矿井下固定摄像头、移动巡检机器人、头戴设备等 |
| **光照条件** | 低照度、高粉尘、复杂反光环境（贴近真实工况） |
| **标注质量** | 高精度人工标注，边界框紧密贴合目标 |
| **标注格式** | ✅ 提供两种标准格式：<br>• YOLO 格式（`.txt`，归一化坐标）<br>• COCO 格式（`instances.json`，含 segmentation） |
| **适用模型** | YOLOv8 / YOLOv10 / YOLOv11 及其变体（如 YOLOv8-seg、YOLO-NAS） |
| **用途说明** | 可直接用于目标检测、行为识别、安全隐患预警系统开发与学术研究 |
| **引用建议** | 论文撰写可直接引用（建议注明数据来源与采集单位） |

---![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/27c26ab31a9d46479ae8c51ae4f0d7fa.png)


### 📊 **类别定义与目标说明**

| 类别 ID | 类别名称（英文） | 类别名称（中文） | 目标描述与检测重点 |
|--------|------------------|------------------|----------------------|
| 0 | `mining_worker` | 煤矿工作人员检测 | 检测井下所有作业人员位置，支持人数统计与区域管控 |
| 1 | `hydraulic_shield` | 液压支撑防护板检测 | 多角度识别液压支架状态：<br>• 0°~30°、30°~60°、60°~90°等角度分类<br>• 支架未完全展开、倾斜、漏液等异常状态识别 |
| 2 | `large_coal_chunk` | 大煤块检测 | 检测采落后的大型煤块（>50cm），防止堵塞运输系统或引发卡滞故障 |
| 3 | `shearer_cable` | 采煤机拖缆检测 | 检测拖拽电缆是否脱轨、缠绕、断裂，预防供电中断 |
| 4 | `unsafe_behavior` | 矿工不安全行为检测 | 包括以下子类行为：<br>• 行走中操作设备<br>• 在危险区站立/停留<br>• 坐卧轨道<br>• 弯腰穿越机械间隙<br>• 依靠支架休息<br>• 摔倒/晕厥<br>• 爬行通过非通行区<br>（可通过动作分类模型进一步细分） |
| 5 | `safety_helmet` | 安全帽佩戴检测 | 检测人员是否佩戴安全帽，区分“佩戴”、“未佩戴”、“佩戴不规范” |

> ✅ 所有类别均支持在低光照、烟尘干扰环境下进行鲁棒检测

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/13c44cedc9c444d5afb66f06751295c8.png)


### 📁 作者建议数据组织结构示例
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e8ba4770d600479d90cdf7264bf059e0.jpeg)


```bash
coal_mine_dataset/
├── images/
│   ├── train/          # 图像训练集（约 104,000 张）
│   ├── val/            # 图像验证集（约 19,500 张）
│   └── test/           # 图像测试集（约 6,500 张）
├── labels/
│   ├── yolo/
│   │   ├── train/      # YOLO 格式 .txt 文件
│   │   ├── val/
│   │   └── test/
│   └── coco/
│       └── annotations/
│           ├── instances_train.json
│           ├── instances_val.json
│           └── instances_test.json
├── data.yaml             # YOLO 配置文件
└── README.md
```
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/f6eef4e5ecd448058adbe2c3d011a92a.jpeg)

---

### 🧾 **data.yaml 配置文件模板（YOLO 使用）**

```yaml
# data.yaml
train: ./coal_mine_dataset/images/train
val: ./coal_mine_dataset/images/val
test: ./coal_mine_dataset/images/test

# 类别数量
nc: 6

# 类别名称（按ID顺序）
names:
  - mining_worker
  - hydraulic_shield
  - large_coal_chunk
  - shearer_cable
  - unsafe_behavior
  - safety_helmet
```

---

### 🔍 **主要应用领域**

| 应用方向 | 具体功能 |
|----------|-----------|
| **智慧矿山建设** | 构建“AI+视频”智能监控平台，实现无人化值守 |
| **安全生产监管** | 实时识别不安全行为与设备异常，自动报警 |
| **事故预防系统** | 提前发现支架失稳、电缆脱落、大块煤卡堵等风险 |
| **人员定位与行为分析** | 结合轨迹跟踪，分析作业流程合规性 |
| **自动化报告生成** | 自动生成每日安全隐患统计报表 |
| **应急响应辅助** | 检测摔倒、晕厥等突发情况，及时启动救援 |

---



以下是针对您提供的 **煤矿井下开采异常检测数据集**（6类目标，13万张图像，YOLO格式）的完整 **YOLOv8 多类别训练脚本**，支持直接训练、验证、推理和模型导出，适用于本地或服务器环境。

---

## ✅ 一、环境准备

```bash
# 安装 YOLOv8（Ultralytics 官方库）
pip install ultralytics

# 其他依赖
pip install opencv-python torch torchvision matplotlib tqdm
```

> 📌 推荐使用 Python 3.8+ 和 PyTorch 1.13+，GPU 环境（CUDA 11.7/12.1）

---

## ✅ 二、数据集结构确认

请确保您的数据集按如下结构组织：

```bash
coal_mine_dataset/
├── images/
│   ├── train/          # 约 104,000 张
│   ├── val/            # 约 19,500 张
│   └── test/           # 约 6,500 张
├── labels/
│   └── yolo/
│       ├── train/      # 对应的 .txt 标签
│       ├── val/
│       └── test/
├── data.yaml           # 配置文件（见下文）
└── README.md
```

---

## ✅ 三、创建 `data.yaml` 文件

在 `coal_mine_dataset/` 目录下创建 `data.yaml`：

```yaml
# data.yaml
train: ./coal_mine_dataset/images/train
val: ./coal_mine_dataset/images/val
test: ./coal_mine_dataset/images/test

# 类别数量
nc: 6

# 类别名称（按ID顺序）
names:
  - mining_worker         # 煤矿工作人员
  - hydraulic_shield      # 液压支撑防护板
  - large_coal_chunk      # 大煤块
  - shearer_cable         # 采煤机拖缆
  - unsafe_behavior       # 不安全行为
  - safety_helmet         # 安全帽佩戴
```

---

## ✅ 四、YOLOv8 多类别训练脚本（Python 版）

### `train_coal_mine.py`

```python
from ultralytics import YOLO
import os

# 设置训练参数
MODEL_NAME = "yolov8l.pt"        # 可选: yolov8n/s/m/l/x，根据硬件选择
PROJECT_NAME = "coal_mine_detection"
EXPERIMENT_NAME = "v1_train_full"
EPOCHS = 100
IMG_SIZE = 640
BATCH_SIZE = 32                  # 根据GPU显存调整（16/32/64）
DEVICE = "0,1"                   # 使用 GPU 0 和 1；单卡用 "0"；CPU 用 "cpu"

# 创建模型
model = YOLO(MODEL_NAME)

# 开始训练
print("🚀 开始训练煤矿井下多目标检测模型...")
results = model.train(
    data="coal_mine_dataset/data.yaml",
    epochs=EPOCHS,
    imgsz=IMG_SIZE,
    batch=BATCH_SIZE,
    device=DEVICE,
    project=PROJECT_NAME,
    name=EXPERIMENT_NAME,
    exist_ok=False,              # 防止覆盖已有实验
    optimizer="AdamW",           # 推荐用于复杂场景
    lr0=0.001,                   # 初始学习率
    lrf=0.1,                     # 最终学习率 = lr0 * lrf
    momentum=0.937,
    weight_decay=5e-4,
    warmup_epochs=3,
    warmup_momentum=0.8,
    box=7.5,                     # 检测框损失权重
    cls=0.5,                     # 分类损失权重
    dfl=1.5,
    label_smoothing=0.1,         # 标签平滑，提升泛化
    patience=15,                 # 早停：15轮无提升则停止
    save_period=10,              # 每10轮保存一次
    seed=42,
    # 数据增强
    hsv_h=0.015,     # 色调增强
    hsv_s=0.7,       # 饱和度增强
    hsv_v=0.4,       # 明度增强
    degrees=10.0,    # 随机旋转
    translate=0.2,   # 平移
    scale=0.5,       # 缩放
    shear=2.0,       # 剪切
    flipud=0.0,      # 上下翻转（井下对称少，可关闭）
    fliplr=0.5,      # 左右翻转
    mosaic=1.0,      # Mosaic增强，提升小目标检测
    mixup=0.1,       # MixUp增强
    copy_paste=0.3,  # Copy-Paste增强（对小目标如安全帽有效）
)

print("✅ 训练完成！")
```

> 💡 **说明**：
> - `copy_paste=0.3`：特别适合“安全帽”、“大煤块”等小目标
> - `mosaic=1.0`：提升小目标和遮挡目标的检测能力
> - `label_smoothing`：防止过拟合，提升模型鲁棒性

---

## ✅ 五、启动训练（命令行方式）

您也可以使用命令行快速启动：

```bash
yolo train \
    model=yolov8l.pt \
    data=coal_mine_dataset/data.yaml \
    epochs=100 \
    imgsz=640 \
    batch=32 \
    device=0,1 \
    project=coal_mine_detection \
    name=v1_train_full \
    optimizer=AdamW \
    lr0=0.001 \
    label_smoothing=0.1 \
    mosaic=1.0 \
    copy_paste=0.3 \
    patience=15
```

---

## ✅ 六、验证与测试

### 1. 在验证集上评估模型

```bash
yolo val model=runs/coal_mine_detection/v1_train_full/weights/best.pt data=coal_mine_dataset/data.yaml
```

### 2. Python 脚本评估

```python
# val_model.py
from ultralytics import YOLO

model = YOLO("runs/coal_mine_detection/v1_train_full/weights/best.pt")
metrics = model.val()
print(f"mAP@0.5: {metrics.box.map:.4f}")
print(f"mAP@0.5:0.95: {metrics.box.map50:.4f}")
print(f"Recall: {metrics.box.recall:.4f}")
```

---

## ✅ 七、推理与预测

### 1. 单张图像预测

```python
# predict_single.py
from ultralytics import YOLO

model = YOLO("runs/coal_mine_detection/v1_train_full/weights/best.pt")
results = model("test_image.jpg", save=True, conf=0.25, show_labels=True)

for r in results:
    print(r.boxes)  # 输出检测框信息
```

### 2. 视频或摄像头实时检测

```python
# 实时检测（摄像头）
results = model.predict(source=0, show=True, save=True)

# 视频文件检测
results = model.predict(source="underground_video.mp4", save=True, conf=0.3)
```

---

## ✅ 八、模型导出（用于部署）

```python
# export_model.py
from ultralytics import YOLO

model = YOLO("runs/coal_mine_detection/v1_train_full/weights/best.pt")

# 导出为 ONNX（通用部署）
model.export(format="onnx", opset=13, dynamic=True)

# 导出为 TensorRT（NVIDIA 加速，推荐用于边缘设备）
model.export(format="engine", half=True, workspace=10)

# 导出为 TFLite（移动端）
model.export(format="tflite")

# 导出为 CoreML（iOS）
model.export(format="coreml")
```

---

## ✅ 九、训练结果输出

训练完成后，将在以下路径生成结果：

```bash
runs/coal_mine_detection/v1_train_full/
├── weights/
│   ├── best.pt        # 最佳模型（mAP最高）
│   └── last.pt        # 最终模型
├── results.png        # 损失曲线、mAP、精度等图表
├── confusion_matrix.png  # 混淆矩阵
├── labels_pred.jpg    # 预测可视化示例
└── args.yaml          # 训练参数记录
```

---

以上为作者提供的代码示例，仅供参考学习。
