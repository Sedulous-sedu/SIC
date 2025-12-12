# GUI Application Guide

Welcome to the **Flight Deck** — a PyQt6 cockpit that keeps training, inference, and export within reach. Glide through the tabs below or jump via the quick links.

> **Jump Links**: [Launch](#launch-options) · [Training Tab](#training-tab) · [Inference Tab](#inference-tab) · [Export Tab](#export-tab) · [Shortcuts](#keyboard-shortcuts) · [HiDPI Tips](#high-dpi--8k-support)

## Launch Options

- Direct: `python gui_app.py`
- Shell launcher: `./launch_gui.sh`
- Embedded: 
  ```python
  from gui_app import main
  main()
  ```

## Training Tab

**What you configure**
- **Model**: yolov8n-cls.pt → yolov8x-cls.pt
- **Dataset**: Browse to your folder-per-class dataset
- **Device**: auto / CPU / specific CUDA device
- **Pretrained**: Toggle ImageNet initialization
- **Hyperparameters**: epochs · batch size · image size · workers · learning rate · patience
- **Project labels**: project + run names to keep outputs organized

**What you see**
- Live progress bar + metrics per epoch
- Streamed training logs
- Start/Stop controls for quick aborts
- Outputs saved under `runs/classify/<project>/<run>/`

## Inference Tab

**Sources**
- Single image
- Folder (batch)
- Video file
- Webcam or RTSP stream

**Controls**
- Confidence threshold slider
- Save predictions toggle

**Readouts**
- Preview panel with overlays
- Top-1 and Top-5 predictions with confidences
- Folder summary with counts and distributions

## Export Tab

**Formats**: ONNX · TorchScript · CoreML

**Knobs**
- Output path suggestion per format
- Image size for exported graph
- FP16 quantization toggle
- ONNX simplification toggle

**Feedback**
- Progress + completion status
- File size hints when done

## Keyboard Shortcuts

- **Ctrl+Q** — Quit
- **Ctrl+O** — Open file dialogs (context aware)
- **Tab** — Move between fields
- **Enter** — Trigger the primary action in the current tab

## High DPI / 8K Support

- Auto high-DPI scaling for crisp widgets and pixmaps
- Font scaling that tracks your display settings
- Manual override if needed:
  ```bash
  export QT_SCALE_FACTOR=1.5
  python gui_app.py
  ```

## Tips & Best Practices

- Start with **yolov8n-cls.pt** for rapid iteration; scale up after baseline accuracy looks good.
- Keep an eye on the **learning rate** and **batch size** if you hit stability or memory issues.
- Use the **folder** inference mode to sanity-check class balance after training.
- Prefer **ONNX + simplify** for widest deployment compatibility; add **FP16** for leaner artifacts.
