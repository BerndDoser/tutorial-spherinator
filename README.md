# Tutorial Spherinator

An end-to-end walkthrough of [Spherinator](https://github.com/HITS-AIN/Spherinator)
and [HiPSter](https://github.com/HITS-AIN/HiPSter) in a single notebook,
[`jupyter/illustris.ipynb`](jupyter/illustris.ipynb):

1. Load the [IllustrisTNG SKIRT SDSS](https://huggingface.co/datasets/HITS-AIN/IllustrisTNG_SKIRT_SDSS)
   galaxy images with a Spherinator `DataModule`.
2. Train a variational autoencoder whose latent space is the unit sphere $S^2$,
   using a small convolutional encoder (~2.1 M parameters).
3. Export the encoder and decoder to ONNX.
4. Generate a [HiPS](https://www.ivoa.net/documents/HiPS/) tiling with HiPSter by
   decoding every HEALPix cell centre.
5. Explore the result in [Aladin Lite](https://aladin.cds.unistra.fr/AladinLite/)
   via the `ipyaladin` widget, with the real galaxies overlaid as a catalogue.

## Jupyter with Docker Compose

```bash
docker compose up --build
```

Open <http://localhost:8888/lab?token=spherinator>

## Jupyter with uv

```bash
uv run --with jupyterlab jupyter lab jupyter/illustris.ipynb
```

The notebook starts an HTTP server on port 8083 to serve the generated HiPS tiles
to Aladin Lite, which runs in the browser and therefore cannot read them from the
filesystem. That port is published in `compose.yml` for the container case.
