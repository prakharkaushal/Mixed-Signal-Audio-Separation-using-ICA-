
# Mixed-Signal Audio Separation with ICA

An end-to-end Independent Component Analysis (ICA) experiment that learns to recover five audio sources from their mixtures. The notebook is designed as a compact, visual walkthrough: load the mixtures, learn an unmixing matrix, inspect the signals, and listen to the recovered tracks.

## Results at a glance

The generated audio is already included in [`output/`](output/). Use the players below to compare the input mixtures with the recovered sources.

### Mixed signals

| Track | Audio |
| --- | --- |
| Mixed 0 | <audio controls preload="metadata"><source src="output/mixed_0.wav" type="audio/wav">[Download mixed_0.wav](output/mixed_0.wav)</audio> |
| Mixed 1 | <audio controls preload="metadata"><source src="output/mixed_1.wav" type="audio/wav">[Download mixed_1.wav](output/mixed_1.wav)</audio> |
| Mixed 2 | <audio controls preload="metadata"><source src="output/mixed_2.wav" type="audio/wav">[Download mixed_2.wav](output/mixed_2.wav)</audio> |
| Mixed 3 | <audio controls preload="metadata"><source src="output/mixed_3.wav" type="audio/wav">[Download mixed_3.wav](output/mixed_3.wav)</audio> |
| Mixed 4 | <audio controls preload="metadata"><source src="output/mixed_4.wav" type="audio/wav">[Download mixed_4.wav](output/mixed_4.wav)</audio> |

### Separated sources

| Source | Audio |
| --- | --- |
| Source 0 | <audio controls preload="metadata"><source src="output/split_0.wav" type="audio/wav">[Download split_0.wav](output/split_0.wav)</audio> |
| Source 1 | <audio controls preload="metadata"><source src="output/split_1.wav" type="audio/wav">[Download split_1.wav](output/split_1.wav)</audio> |
| Source 2 | <audio controls preload="metadata"><source src="output/split_2.wav" type="audio/wav">[Download split_2.wav](output/split_2.wav)</audio> |
| Source 3 | <audio controls preload="metadata"><source src="output/split_3.wav" type="audio/wav">[Download split_3.wav](output/split_3.wav)</audio> |
| Source 4 | <audio controls preload="metadata"><source src="output/split_4.wav" type="audio/wav">[Download split_4.wav](output/split_4.wav)</audio> |

For a reference comparison, the supplied target is [`data/correct_split_0.wav`](data/correct_split_0.wav). The learned matrix is saved as [`output/W.txt`](output/W.txt).

## Run the notebook

1. Open [`p04_ica.ipynb`](p04_ica.ipynb) in VS Code or Jupyter.
2. Select a Python kernel with NumPy, SciPy, Matplotlib, and IPython installed.
3. Run the cells from top to bottom.

The notebook reads `data/mix.dat`, writes WAV files and `W.txt` into `output/`, and uses a fixed random seed so the result is repeatable.

## Method

The mixtures are normalized and processed with a Laplace-model ICA update. The algorithm starts with an identity matrix and performs stochastic gradient ascent over an annealed learning-rate schedule. Once the unmixing matrix $W$ is learned, the recovered signals are computed as:

$$S = XW^T$$

where $X$ is the matrix of observed mixtures and $S$ contains the estimated independent sources.

## Repository layout

```text
.
├── data/
│   ├── mix.dat
│   └── correct_split_0.wav
├── output/
│   ├── mixed_*.wav
│   ├── split_*.wav
│   └── W.txt
├── p04_ica.ipynb
└── README.md
```

