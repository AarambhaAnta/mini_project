# EMO-DB Audio Emotion Dataset Processing

Processing and feature extraction pipeline for the Berlin Database of Emotional Speech (EMO-DB).

**Original Dataset:** [Berlin Database of Emotional Speech on Kaggle](https://www.kaggle.com/datasets/piyushagni5/berlin-database-of-emotional-speech-emodb?resource=download)

## Project Overview

This project processes emotional speech audio files, splits them into uniform segments, and generates structured metadata for machine learning applications. The pipeline handles 535 audio recordings from 10 speakers across 7 emotion categories.

## Folder Structure

```bash
mini_project/
├── emodb_dataset/              # Original EMO-DB audio files
├── emodb_dataset_partitioned/  # Partitioned audio segments
├── features/                   # Extracted features and metadata
│   ├── durations.csv          # Audio segment durations
│   ├── labels.csv             # Labeled dataset with metadata
│   └── test/                  # Per-speaker test feature files
│       ├── S03.csv
│       ├── S08.csv
│       └── ...
├── test/                      # Test audio samples
├── main.ipynb                 # Main processing pipeline
├── build_test.ipynb           # Testing utilities
├── rename_wav.ipynb           # File renaming utilities
└── README.md                  # Project documentation
```

## Directory Details

### `emodb_dataset/`

Original EMO-DB audio files (535 recordings) with emotion labels encoded in filenames.

**Filename Format:** `SSPPPEV.wav`

- `SS`: Speaker ID (03, 08, 09, 10, 11, 12, 13, 14, 15, 16)
- `PPP`: Text code (a01-a07, b01-b10)
- `E`: Emotion code
  - `W` = Anger (Wut)
  - `L` = Boredom (Langeweile)
  - `E` = Disgust (Ekel)
  - `A` = Anxiety/Fear (Angst)
  - `F` = Happiness (Freude)
  - `T` = Sadness (Traurigkeit)
  - `N` = Neutral
- `V`: Version (a, b, c, d, e, f)

**Example:** `03a01Fa.wav` → Speaker 03, text a01, Happiness, version a

### `emodb_dataset_partitioned/`

Processed audio files split into uniform segments for consistent ML training.

**Filename Format:** `SXX_SSPPPEV_N.wav`

- `SXX`: Speaker prefix (S03, S08, etc.)
- `SSPPPEV`: Original filename
- `N`: Segment number (1, 2, 3...)

**Example:** `S03_03a01Fa_1.wav` → First segment of speaker 03's recording

**Total Segments:** 873 audio files

### `features/`

Generated metadata and feature files for model training.

#### Files

- **`durations.csv`** (873 entries)
  - `filename`: Segment filename
  - `duration(sec)`: Duration in seconds

- **`labels.csv`** (873 entries)
  - `ID`: Unique segment identifier
  - `duration`: Audio duration (seconds)
  - `wav`: Full path to audio file
  - `start`: Start frame (0-based)
  - `stop`: End frame (samples at 16kHz)
  - `spk_id`: Speaker ID (S03-S16)
  - `label`: Emotion number (0-6)

#### Emotion Label Mapping

| Label | Emotion  | Count (approx) |
|-------|----------|----------------|
| 0     | Happiness| ~127           |
| 1     | Neutral  | ~79            |
| 2     | Anger    | ~127           |
| 3     | Anxiety  | ~69            |
| 4     | Boredom  | ~81            |
| 5     | Disgust  | ~46            |
| 6     | Sadness  | ~62            |

#### `test/` subdirectory

Per-speaker CSV files containing extracted features for testing/validation (S03.csv through S16.csv).

### `test/`

Sample test audio files for pipeline validation.

## Notebooks

### `main.ipynb`

Primary processing pipeline with the following workflow:

1. **Audio Splitting**: Splits long recordings into 2-part segments
2. **Duration Extraction**: Calculates duration for each segment
3. **Label Generation**: Creates structured dataset with:
   - File metadata
   - Speaker identification
   - Emotion labeling
   - Sample rate conversion (16kHz standard)

**Key Functions:**

- `split_wav()`: Splits audio files into equal parts
- `create_audio_duration_csv()`: Generates duration metadata
- `parse_filename()`: Extracts speaker/emotion from filenames
- `create_label_csv()`: Builds labeled dataset

### `build_test.ipynb`

Testing and validation utilities for the processing pipeline.

### `rename_wav.ipynb`

File renaming utilities for dataset organization.

## Dataset Statistics

- **Total Original Files:** 535 recordings
- **Total Segments:** 873 audio files
- **Speakers:** 10 (5 male, 5 female)
- **Emotions:** 7 categories
- **Sample Rate:** 16 kHz (after processing)
- **Segment Duration:** ~1-2 seconds (variable)

## Usage

### Complete Pipeline

Run [main.ipynb](main.ipynb) cells sequentially:

1. Load libraries (wave, os, csv, pandas)
2. Configure paths for input/output directories
3. Execute audio splitting on EMO-DB files
4. Generate duration CSV
5. Create labeled dataset CSV

### Quick Start

```python
# Process audio files
output_path = "/path/to/mini_project/emodb_dataset_partitioned"
features_path = "/path/to/mini_project/features"

# Run processing functions in main.ipynb
# - Audio splitting
# - Duration extraction  
# - Label generation
```

## Dependencies

- `wave`: Audio file processing
- `pandas`: Data manipulation
- `numpy`: Numerical operations
- `librosa`: Audio analysis (optional)
- `scikit-learn`: ML utilities (optional)
- `tensorflow`: Deep learning (optional)

Install dependencies:

```bash
pip install librosa numpy pandas scikit-learn tensorflow matplotlib
```

## Dataset Citation

If using this dataset, please cite:

> Burkhardt, F., Paeschke, A., Rolfes, M., Sendlmeier, W.F., & Weiss, B. (2005).  
> A database of German emotional speech.  
> Proc. Interspeech 2005, 1517-1520.

## License

EMO-DB is available for research purposes. Please refer to the original dataset license terms on Kaggle.
