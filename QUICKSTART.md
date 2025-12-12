# Quick Start Guide

Think of this as a **choose-your-own-launchpad**. Follow the default runway or hop into the fast lanes that match your workflow.

## Launch Checklist (10 minutes)

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
2. **Verify the cockpit**
   ```bash
   python main.py --help
   ```
   You should see commands for `train`, `predict`, and `export`.
3. **Organize your dataset** (folder-per-class)
   ```
   data/
   ├── train/
   │   ├── class1/
   │   ├── class2/
   │   └── class3/
   └── val/
       ├── class1/
       ├── class2/
       └── class3/
   ```
4. **Train a model**
   ```bash
   python main.py train --data ./data --epochs 50 --batch 16
   ```
5. **Test inference**
   ```bash
   python main.py predict --model runs/classify/run/weights/best.pt --source path/to/image.jpg --save
   ```
6. **Export (optional)**
   ```bash
   python main.py export --model runs/classify/run/weights/best.pt --format onnx --output model.onnx --simplify
   ```

## Speed Lanes

- **GPU available?** Install CUDA-enabled PyTorch from [pytorch.org](https://pytorch.org/) before step 1.
- **Already have a dataset?** Jump straight to step 4 and point `--data` at it.
- **Want to sanity-check the pipeline?** Use a pretrained model: `python main.py predict --model yolov8n-cls.pt --source image.jpg`.

## Command Cheat Sheet

**Training (customizable)**
```bash
python main.py train \
    --data ./data \
    --model yolov8n-cls.pt \
    --epochs 100 \
    --batch 16 \
    --imgsz 224 \
    --device cuda \
    --project my_classification_project \
    --name experiment_1
```

**Inference (folder)**
```bash
python main.py predict \
    --model runs/classify/run/weights/best.pt \
    --source ./test_images \
    --save \
    --output ./predictions
```

**Video/Webcam**
```bash
python main.py predict --model best.pt --source video.mp4 --output output.mp4 --show
python main.py predict --model best.pt --source 0 --show              # webcam
```

## Troubleshooting Radar

- **CUDA out of memory** → Lower batch size: `--batch 8`.
- **Dataset not found** → Confirm the `--data` path and folder layout.
- **Model file missing** → Ensure training finished and `runs/classify/.../weights/best.pt` exists.

## Next Moves

- Experiment with model sizes (`yolov8n-cls.pt` → `yolov8x-cls.pt`).
- Tune hyperparameters in `configs/config.yaml` (CLI flags still win).
- Try different image sizes with `--imgsz 224` (common) or alternatives.
