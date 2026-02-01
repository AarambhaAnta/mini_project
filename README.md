# Audio Emotion Dataset Processing

Berlin Database of Emotional Speech (EMO-DB) processing and labeling.

**Original Dataset:** [Berlin Database of Emotional Speech on Kaggle](https://www.kaggle.com/datasets/piyushagni5/berlin-database-of-emotional-speech-emodb?resource=download)

## Folder Structure

```bash
mini_project/
├── dataset/          # Original audio files
├── output/           # Processed/split audio files
├── info/             # Generated CSV metadata files
├── main.ipynb        # Main processing notebook
└── README.md         # Project documentation
```

## Folders

### `dataset/`

Contains original `.wav` audio files with emotion labels encoded in filenames.

**Filename Format:** `SSPPPEV.wav`

- `SS`: Speaker ID (e.g., 03, 08, 10)
- `PPP`: Text code (e.g., a01, b02)
- `E`: Emotion code (W=Anger, L=Boredom, E=Disgust, A=Anxiety, F=Happiness, T=Sadness, N=Neutral)
- `V`: Version (a, b, c, etc.)

### `output/`

Contains split audio files (e.g., `03a01Fa_1.wav`, `03a01Fa_2.wav`) generated from original files based on duration.

### `info/`

Contains generated CSV files with metadata:

- `audio_durations.csv`: Filename and duration for each output file
- `audio_labels.csv`: Complete dataset labels with columns:
  - `ID`: Speaker ID (format: S03, S08, etc.)
  - `duration`: Audio duration in seconds
  - `file_location`: Full path to audio file
  - `start`: Start time in original recording
  - `stop`: Stop time in original recording
  - `speaker_id`: Speaker number
  - `emotion_label`: Emotion name
  - `emotion_number`: Emotion numeric code (Happiness=0, Neutral=1, Anger=2, Anxiety=3, Boredom=4, Disgust=5, Sadness=6)

## Files

### `main.ipynb`

Jupyter notebook for processing audio files:

1. Splits long audio files into smaller segments
2. Generates duration metadata
3. Creates labeled dataset CSV with emotion annotations

## Usage

Run cells in `main.ipynb` sequentially to process audio files and generate labeled datasets.
