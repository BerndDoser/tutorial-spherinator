# Tutorial Spherinator & HiPSter

End-to-end walkthroughs of [Spherinator](https://github.com/HITS-AIN/Spherinator)
and [HiPSter](https://github.com/HITS-AIN/HiPSter) on the
[Emoji Dataset](https://huggingface.co/datasets/valhalla/emoji-dataset):

1. **Load** 2,749 emoji images with a Spherinator `DataModule`.
2. **Train** a variational autoencoder whose latent space is the unit sphere
   $S^2$, using a small convolutional encoder.
3. **Export** the encoder and decoder to ONNX.
4. **Generate** a [HiPS](https://www.ivoa.net/documents/HiPS/) tiling with
   HiPSter by decoding every HEALPix cell centre, plus a nearest-neighbour
   projection of the real dataset onto the same tiling.
5. **Explore** the result in [Aladin Lite](https://aladin.cds.unistra.fr/AladinLite/)
   via the `ipyaladin` widget, with the real emoji overlaid as a catalogue and
   the model/dataset tilings blended into each other.


## Notebooks

- [`emojis_training.ipynb`](jupyter/emojis_training.ipynb)  
  [![Open In
  Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BerndDoser/Tutorial-Spherinator/blob/master/jupyter/emojis_training.ipynb)  
  Trains a quick demo model (under two minutes on a laptop GPU) and exports it to ONNX.
- [`emojis_inference.ipynb`](jupyter/emojis_inference.ipynb)  
  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/BerndDoser/Tutorial-Spherinator/blob/master/jupyter/emojis_inference.ipynb)  
  Downloads a more thoroughly trained production model from Hugging Face ([`bernddoser/emoji`](https://huggingface.co/bernddoser/emoji)) instead of reading the output of the training notebook, then generates and serves the tiling.

The two notebooks are independent: run either on its own, or run the training
notebook first and point the inference notebook at its ONNX output instead of
the Hugging Face download.


## Jupyter with Docker Compose

```bash
docker compose up --build
```

Open <http://localhost:8888/lab?token=spherinator> and pick a notebook.


## Jupyter with uv

```bash
uv run --with jupyterlab jupyter lab
```

The inference notebook starts an HTTP server on port 8083 to serve the
generated HiPS tiles to Aladin Lite, which runs in the browser and therefore
cannot read them from the filesystem. That port is published in `compose.yml`
for the container case.
