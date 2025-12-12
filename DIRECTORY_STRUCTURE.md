# Directory Structure (Choose Your Tour)

Use this map like a museum guide: jump to the room you care about or skim the highlights.

## Quick Postcard

```
SIC/
├── README.md                  # Interactive overview
├── QUICKSTART.md              # 10-minute takeoff
├── GUI_GUIDE.md               # Screens + tips for the GUI
├── main.py                    # CLI entry point
├── gui_app.py                 # GUI entry point
├── launch_gui.sh              # GUI launcher
├── configs/
│   └── config.yaml            # Default knobs
└── src/
    ├── trainer.py             # Training logic
    ├── predictor.py           # Inference logic
    └── exporter.py            # Export logic
```

## Room-by-Room

- **Root Deck**
  - `README.md` — orientation map with pick-your-path navigation.
  - `QUICKSTART.md` — condensed setup and runnable snippets.
  - `GUI_GUIDE.md` — how to fly the PyQt6 interface.
  - `requirements.txt` — everything you need to install.
  - `main.py` — CLI portal for train/predict/export.
  - `gui_app.py` + `launch_gui.sh` — graphical portal and shell launcher.

- **configs/**
  - `config.yaml` — baseline defaults for model, dataset, training, and export. CLI flags override these.

- **src/**
  - `trainer.py` — `ClassificationTrainer` orchestrates YOLOv8 classification training (callbacks, checkpoints, metrics).
  - `predictor.py` — `ClassificationPredictor` handles images, folders, videos, and live streams.
  - `exporter.py` — `ModelExporter` targets ONNX, TorchScript, CoreML, and more.

## What Appears After You Run Things

```
runs/classify/
└── <project>/<run>/
    ├── weights/
    │   ├── best.pt
    │   └── last.pt
    ├── results.png
    ├── confusion_matrix.png
    └── ...
predictions/                # if you saved outputs during inference
```

## Navigation Shortcuts

- Want commands you can paste? → [CLI Action Cards](README.md#cli-action-cards)
- Need dataset layout? → [Dataset Blueprint](README.md#dataset-blueprint)
- Looking for GUI instructions? → [GUI Flight Deck](README.md#gui-flight-deck)
