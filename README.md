# AI Product Recognition V2

This version learns your own 13 physical products from webcam photos. The previous YOLO-World version tried generic text-based detection, which can be slow and unreliable for specific products.

## Important
For accurate recognition of your exact items, collect example photos first. Aim for 30-50 varied photos per product (different angles, distances, and backgrounds). Training is a one-time step and can take several minutes on CPU. Live recognition then uses a small classifier at 160px. Speed depends on your laptop.

## Setup (VS Code PowerShell)
Use your existing `.venv` if it already has Ultralytics and OpenCV installed. Otherwise:
```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install ultralytics opencv-python
```

## 1. Collect photos
```powershell
.\.venv\Scripts\python.exe src\collect_data.py
```
Press the product letter shown on screen to select it, then SPACE to save a photo. Press Q to quit. Repeat until each product has 30-50 varied photos.

## 2. Train once
```powershell
.\.venv\Scripts\python.exe src\train_model.py
```

## 3. Run live recognition
```powershell
.\.venv\Scripts\python.exe src\recognize.py
```
Show one product at a time inside the green square. Press Q to quit.

## Tips
Use bright light, keep the item centred and reasonably large, and capture different angles/backgrounds. If two products are confused, collect more varied examples of those two and retrain. Confidence is an estimate, not a guarantee.

## GitHub
`.gitignore` excludes raw photos, datasets, model weights, and virtual environments. Upload the code and README; avoid uploading private photos.
