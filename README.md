# SovereignGuard — Member 1 (AI & Sensor Specialist)

This is YOUR entire part of the project. Your team's app is being built in
**Flutter**, but you don't need to touch Flutter or Dart at all — you stay
100% in Python. This package includes a small Dart file for Member 4 too,
so they know exactly how to connect to your work.

---

## What's inside this zip

```
sovereignguard-member1-final/
├── README.md                              <- this file
├── backend/                               <- YOUR work, in Python
│   ├── main.py
│   ├── models.py
│   ├── motion_detection.py
│   ├── ble_detection.py
│   └── requirements.txt
└── flutter-snippets-for-member4/          <- hand these 2 files to Member 4
    ├── sensor_sender.dart
    └── ble_sender.dart
```

---

## PART 1: Getting your Python backend running

### Step 1 — Install Python (skip if you already did this)

1. Open your browser, go to: **https://www.python.org/downloads/**
2. Click the yellow "Download Python" button.
3. Open the downloaded file.
4. On the FIRST screen of the installer, **check the box that says "Add python.exe to PATH"** at the bottom.
5. Click **"Install Now"**, wait, then click **"Close"**.

### Step 2 — Confirm Python installed

1. Press the **Windows key**, type `cmd`, press **Enter**. A black window opens (Command Prompt).
2. Type this and press Enter:
   ```
   python --version
   ```
3. You should see something like `Python 3.12.4`. If you see an error, tell me exactly what it says.

### Step 3 — Unzip this project

1. Find the file you downloaded: `sovereignguard-member1-final.zip`
2. Right-click it → **Extract All** → choose your **Desktop** as the location → click **Extract**.
3. You should now have a folder on your Desktop called `sovereignguard-member1-final`.

### Step 4 — Open Command Prompt inside the `backend` folder

1. Open File Explorer, go to: `Desktop` → `sovereignguard-member1-final` → `backend`
2. Click once on the empty address bar at the top of the File Explorer window (it currently shows the folder path).
3. Type `cmd` and press **Enter**. A black Command Prompt window opens, already inside the `backend` folder.

### Step 5 — Create a virtual environment

A virtual environment keeps this project's Python packages separate from everything else on your computer. In the Command Prompt window, type:

```
python -m venv venv
```

Wait a few seconds — this creates a new folder called `venv` inside `backend`.

### Step 6 — Activate the virtual environment

Type:

```
venv\Scripts\activate
```

You'll know it worked because the line now starts with `(venv)`, like:
```
(venv) C:\Users\YourName\Desktop\sovereignguard-member1-final\backend>
```

**Important:** every time you close and reopen Command Prompt to work on this project, you must repeat Steps 4 and 6 (navigate to the folder, then activate venv) before running anything.

### Step 7 — Install the required packages

Type:

```
pip install -r requirements.txt
```

This reads the `requirements.txt` file and installs exactly: `fastapi`, `uvicorn`, and `pydantic`. Wait for it to finish — you'll see a bunch of text, ending in something like `Successfully installed fastapi-0.115.0 ...`

### Step 8 — Run your server

Type:

```
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

You should see:
```
INFO:     Uvicorn running on http://0.0.0.0:8000
INFO:     Application startup complete.
```

**Leave this window open** — closing it stops your server. If you need to type more commands, open a NEW Command Prompt window (and remember to repeat Steps 4 and 6 in that new window).

### Step 9 — Test it in your browser

1. Open Chrome/Edge.
2. Go to: **http://127.0.0.1:8000/docs**
3. You'll see a page listing your API endpoints (`/analyze-motion`, `/analyze-ble`, `/demo/trigger-impact`, `/demo/seed-stalker`).
4. Click on **POST /demo/trigger-impact** → click **"Try it out"** → click the blue **"Execute"** button.
5. Scroll down — you should see a response like:
   ```json
   {
     "event": "IMPACT_DETECTED",
     "confidence": 0.95,
     "max_g_force": 4.2,
     "message": "[DEMO MODE] Fall signature detected..."
   }
   ```

**If you see that response, your backend is fully working.** Tell me it worked (or paste any error) before moving on.

---

## PART 2: What each file does (for your own understanding)

| File | What it does |
|---|---|
| `main.py` | Defines the actual web addresses (endpoints) your app can call, like `/analyze-motion` |
| `models.py` | Defines exactly what shape/fields the incoming and outgoing data must have |
| `motion_detection.py` | The actual "is this a fall?" logic — math on accelerometer numbers |
| `ble_detection.py` | The actual "is this device following me?" logic — tracks Bluetooth device history |
| `requirements.txt` | List of packages `pip` needs to install |

You are welcome to open these files in Notepad (or better, install **VS Code**: https://code.visualstudio.com/ — free code editor, just download and run the installer with default settings) to read through the comments — every function is explained in plain English inside the file.

---

## PART 3: Handing off to Member 4 (Flutter developer)

1. Send them the entire `flutter-snippets-for-member4` folder (2 files: `sensor_sender.dart` and `ble_sender.dart`).
2. Tell them: *"These connect to my Python backend. Replace `YOUR_BACKEND_IP` in both files with my computer's IP address before testing — I'll give you that IP separately once we're on the same WiFi."*
3. To find your IP address (do this when you're ready to test together, since IP can change):
   ```
   ipconfig
   ```
   Look for "IPv4 Address" — something like `192.168.1.5`. Give this number to Member 4.
4. Both your laptop (running the Python server) and their phone (running the Flutter app) must be connected to the **same WiFi network** for this to work.

---

## PART 4: For your live demo

Instead of relying on real sensors working perfectly on stage, use these two guaranteed-to-work triggers:

- **POST `/demo/trigger-impact`** — instantly returns a fake-but-realistic "fall detected" response.
- **POST `/demo/seed-stalker?user_id=demo_user_1`** — pre-loads fake Bluetooth history so the very next `/analyze-ble` call for that user shows `STALKER_DETECTED`.

Both can be tested right now in your browser at `http://127.0.0.1:8000/docs`, and Member 4 can wire a hidden button in the app to call these as a safety net.

---

## If something goes wrong

Copy the **exact error text** from Command Prompt and send it to me — I'll tell you exactly what to fix and which line to change.
