# VB_196
Speech overlap detection in stereo audio using Silero VAD.
# Stereo Audio Speech Overlap Detection using Silero VAD

## Overview

This project analyzes **stereo audio recordings** and detects **speech overlap (crosstalk)** between left and right channels using **Silero Voice Activity Detection (VAD)**.

The system processes both audio channels independently, identifies speech segments, and classifies them as:

- **ISOLATED** → Clean speech with no overlap (usable)
- **OVERLAP** → Speech overlapping with the other channel (rejected)

The goal is to estimate the **quality and usability of speech segments** for applications such as:

- Voice Biometrics
- Speaker Verification
- Audio Sampling Services
- Call Center Audio Analysis
- Crosstalk Detection
- Speech Quality Assessment

---

## Features

✅ Stereo audio loading and processing  
✅ Automatic resampling to **16kHz**  
✅ Speech detection using **Silero VAD**  
✅ Speech overlap (crosstalk) detection between channels  
✅ Classification of speech segments:
- Isolated (usable)
- Overlapping (rejected)

✅ Speech statistics generation:
- Total speech duration
- Isolated speech percentage
- Overlap percentage
- Usable/rejected segment count

✅ Feasibility analysis:
- **HIGH** → Plenty of isolated speech
- **MEDIUM** → Some overlap present
- **LOW** → Heavy overlap

✅ JSON result export

---

## How It Works

### Step 1: Load Stereo Audio
The system loads a stereo `.wav` file and separates:

- **Left Channel (L)**
- **Right Channel (R)**

If the audio sample rate is different, it automatically converts it to:

**16,000 Hz (16kHz)**

---

### Step 2: Speech Detection (VAD)

The project uses **Silero VAD** to detect speech timestamps from both channels.

Example:

```python
[
    {"start": 0.5, "end": 3.2},
    {"start": 4.1, "end": 6.0}
]
```

---

### Step 3: Overlap Detection

Each speech segment from the processed channel is compared with the reference channel.

#### Classification Logic

| Condition | Status |
|------------|---------|
| No overlap found | ISOLATED |
| Overlap found | OVERLAP |

---

### Step 4: Speech Quality Analysis

The script calculates:

- Total speech duration
- Isolated speech duration
- Overlapping speech duration
- Usable percentage
- Rejected percentage

---

## Project Structure

```bash
project/
│── main.py
│── experiment_results.json
│── README.md
```

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/your-username/your-repository-name.git
cd your-repository-name
```

### Install Dependencies

```bash
pip install torch torchaudio silero-vad
```

---

## Usage

### Set Audio Path

Inside the script, update:

```python
input = "/content/1.wav"
```

with your audio file path.

Example:

```python
input = "audio/test.wav"
```

---

### Run the Script

```bash
python main.py
```

---

## Output Example

Example terminal output:

```bash
--- Processed: L | Reference: R ---

L channel speech segments: 12
R channel speech segments: 9

Total speech       : 40.25s
Isolated (usable)  : 29.50s (73.2%)
Overlap (rejected) : 10.75s (26.8%)

Feasibility: HIGH - plenty of isolated speech
```

---

## JSON Output

Results are saved as:

```bash
experiment_results.json
```

Example:

```json
[
  {
    "processed_channel": "L",
    "usable_pct": 73.2,
    "rejected_pct": 26.8,
    "feasibility": "HIGH - plenty of isolated speech"
  }
]
```

---

## Technologies Used

- Python
- PyTorch
- TorchAudio
- Silero VAD
- JSON

---

## Use Cases

This project can be used for:

### Voice Biometrics
Selecting clean speaker segments before voiceprint generation.

### Call Center Audio Processing
Removing overlapping conversations.

### Speaker Verification
Improving speaker embedding quality.

### Crosstalk Detection
Identifying overlapping speech in stereo calls.

### Speech Quality Filtering
Selecting high-quality isolated speech.

---

## Future Improvements

- Audio waveform visualization
- Segment timeline plotting
- CSV report generation
- GUI/interactive dashboard
- Multi-speaker overlap analysis

---



