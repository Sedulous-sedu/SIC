# YOLOv8 Classification Suite

A production-grade, modular toolkit for image classification with YOLOv8 — now documented as an **interactive map** so you can jump straight to what you need.

> **Pick Your Path**
> - **I want the fastest setup** → Jump to the [Quick Launch Lane](#quick-launch-lane)
> - **I prefer the GUI experience** → Skip to the [GUI Flight Deck](#gui-flight-deck)
> - **I work in the terminal** → Head to the [CLI Action Cards](#cli-action-cards)
> - **I need the lay of the land** → Explore the [Repo Topography](#repo-topography)

## Why This Suite Stands Out

- **Professional GUI**: Modern PyQt6 interface with 8K/High DPI support.
- **Modular Architecture**: Clear separation for training, inference, and export.
- **Production Ready**: Logging, error handling, type hints, CLI + GUI entry points.
- **Flexible Training**: Configurable hyperparameters with checkpointing and early stopping.
- **Real-Time Monitoring**: Live metrics and previews while training or inferencing.
- **Device-Aware**: Automatic CUDA/CPU selection and export to ONNX/TorchScript/CoreML.

## Quick Launch Lane

Follow this abbreviated runway to get airborne fast. For a full play-by-play, see [QUICKSTART.md](QUICKSTART.md).

1. **Install**
   ```bash
   pip install -r requirements.txt
   ```
2. **Check the controls**
   ```bash
   python main.py --help
   ```
3. **Train immediately**
   ```bash
   python main.py train --data ./data --epochs 50 --batch 16
   ```
4. **Test a single image**
   ```bash
   python main.py predict --model runs/classify/run/weights/best.pt --source image.jpg --save
   ```
5. **Export for deployment**
   ```bash
   python main.py export --model runs/classify/run/weights/best.pt --format onnx --output model.onnx --simplify
   ```

## GUI Flight Deck

Prefer point-and-click? Launch the PyQt6 experience and fly through training, inference, and export from a single cockpit. Detailed screenshots and tips live in [GUI_GUIDE.md](GUI_GUIDE.md).

**Launch Options**
- `python gui_app.py`
- `./launch_gui.sh`
- In Python: `from gui_app import main; main()`

**Tabs at a Glance**
- **Training**: Model picker, dataset browser, hyperparameter sliders, live logs, start/stop controls.
- **Inference**: Load models, pick sources (image/folder/video/webcam), adjust confidence, see previews and ranked predictions.
- **Export**: Choose ONNX/TorchScript/CoreML, toggle FP16 or ONNX simplification, and track progress.

## CLI Action Cards

Mix and match these cards to build your own workflow.

<details>
<summary><strong>Train (baseline)</strong></summary>

```bash
python main.py train --data ./data --epochs 100 --batch 16
```

Key options: `--model yolov8n-cls.pt` · `--imgsz 224` · `--device cuda|cpu` · `--project my_project` · `--name experiment_1`
</details>

<details>
<summary><strong>Predict (single image)</strong></summary>

```bash
python main.py predict --model runs/classify/run/weights/best.pt --source image.jpg --save
```
</details>

<details>
<summary><strong>Predict (folder)</strong></summary>

```bash
python main.py predict --model best.pt --source ./test_images --save --output ./predictions
```
</details>

<details>
<summary><strong>Predict (video or stream)</strong></summary>

```bash
python main.py predict --model best.pt --source video.mp4 --output output.mp4 --show
python main.py predict --model best.pt --source 0 --show              # webcam
python main.py predict --model best.pt --source rtsp://... --show     # RTSP
```
</details>

<details>
<summary><strong>Export</strong></summary>

```bash
python main.py export --model best.pt --format onnx --output model.onnx --imgsz 224 --simplify
python main.py export --model best.pt --format torchscript --output model.pt
python main.py export --model best.pt --format coreml --output model.mlmodel
```
</details>

## Dataset Blueprint

YOLOv8 classification expects a folder-per-class layout. Point your `--data` flag at the directory containing `train/` and `val/` (and optionally `test/`).

```
data/
├── train/
│   ├── class1/
│   ├── class2/
│   └── class3/
├── val/
│   ├── class1/
│   ├── class2/
│   └── class3/
└── test/        # optional
```

**Tips**
- Folder names become class labels.
- Supported formats: JPG, JPEG, PNG, BMP, TIFF, WEBP.
- Keep images directly inside each class folder (no nested subfolders).

## Repo Topography

For a guided tour of every directory and generated artifact, check [DIRECTORY_STRUCTURE.md](DIRECTORY_STRUCTURE.md). Quick map:

```
SIC/
├── src/           # trainer.py, predictor.py, exporter.py
├── configs/       # config.yaml (defaults)
├── main.py        # CLI entry point
├── gui_app.py     # GUI entry point
└── launch_gui.sh  # shell launcher for the GUI
```

## Model Menu

Pick the YOLOv8 classification variant that matches your balance of speed and accuracy:
- `yolov8n-cls.pt` — Nano (fastest)
- `yolov8s-cls.pt` — Small
- `yolov8m-cls.pt` — Medium
- `yolov8l-cls.pt` — Large
- `yolov8x-cls.pt` — Extra Large (most accurate)

## Configuration Snapshot

Defaults live in `configs/config.yaml`; CLI flags always override. Example:

```yaml
model:
  name: "yolov8n-cls.pt"
  pretrained: true

dataset:
  root: "data"

training:
  epochs: 100
  batch_size: 16
  imgsz: 224
  device: "auto"
```

## Outputs at a Glance

Training writes into `runs/classify/` by project/run name:

```
runs/classify/
└── run/
    ├── weights/
    │   ├── best.pt
    │   └── last.pt
    ├── results.png
    ├── confusion_matrix.png
    └── ...
```

## Requirements

- Python 3.8+
- PyTorch 2.0+
- CUDA (optional for GPU acceleration)
- Full list in `requirements.txt`

## Licensing

Provided as-is for educational and production use.
