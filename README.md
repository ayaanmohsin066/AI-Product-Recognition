# AI Product Recognition V2

This version learns your own 13 physical products from webcam photos. The previous YOLO-World version tried generic text-based detection, which can be slow and unreliable for specific products.

## Important
For accurate recognition of your exact items, collect example photos first. Aim for 30-50 varied photos per product (different angles, distances, and backgrounds). Training is a one-time step and can take several minutes on CPU. Training and live recognition both use a small classifier at 160px on the same centred square crop. Speed depends on your laptop.

## Setup (VS Code PowerShell)
Double-click `setup.bat`. It creates `.venv` and installs `requirements.txt`. If you already have a `.venv`, you can instead run:
```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

## Run order
`setup.bat` -> `src\collect_data.py` -> `src\train_model.py` -> `run.bat`

## 1. Collect photos
```powershell
.\.venv\Scripts\python.exe src\collect_data.py
```
Press the product letter shown on screen to select it, then SPACE to save a photo. Press Q to quit. Repeat until each product has 30-50 varied photos.

## 2. Train once
```powershell
.\.venv\Scripts\python.exe src\train_model.py
```
Every product needs at least 10 photos. If any are short, training lists them all and stops without touching `dataset/`.

## 3. Run live recognition
Double-click `run.bat`, or:
```powershell
.\.venv\Scripts\python.exe src\recognize.py
```
Show one product at a time inside the green square; only that square is classified, just like the collected photos. If the top confidence is below `CONF_THRESHOLD` (60% by default) the label shows "Unknown". Press Q to quit. If no model has been trained yet, the app tells you which commands to run.

## Settings
`src/config.py` holds `CAMERA_INDEX` (try 1 if the wrong camera opens), `CONF_THRESHOLD`, and the crop and image size, which must match between collection, training and recognition.

## Tips
Use bright light, keep the item centred and reasonably large, and capture different angles/backgrounds. If two products are confused, collect more varied examples of those two and retrain. Confidence is an estimate, not a guarantee.

## Legacy V1
`src/product_detector.py` is the older YOLO-World version. It is kept for reference and reads its classes from `src/labels.py`; `run.bat` starts V2.

## Tests
```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
.\.venv\Scripts\python.exe -m pytest
```
The tests cover the pure helpers and labels; they need no camera or model.

## GitHub
`.gitignore` excludes raw photos, datasets, model weights, and virtual environments. Upload the code and README; avoid uploading private photos.
