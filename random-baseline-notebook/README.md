# Random Baseline for ValueEval'24 (Notebook)
Random baseline for the task on Human Value Detection, notebook version.

The baseline is intended for kickstarting your own approach. Load your models
etc. at `Setup` and then change `predict(text)`. If you keep everything else,
your approach can be directly dockerized, run within Docker on TIRA, and run as
a server that you can call via HTTP or deploy for everyone to use.

## Usage
You can open the [random_baseline.ipynb](random_baseline.ipynb) notebook in a notebook server as usual.

### Local usage
```bash
# install
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# run
tira-run-notebook --notebook random_baseline.ipynb --input ../toy-dataset --output output

# view result
cat output/predictions.tsv
```

### Docker usage
```bash
# build
docker build -t registry.webis.de/code-research/tira/tira-user-TIRA_USER_FOR_AUTOMATIC_REPLACEMENT/random-baseline-notebook:1.0.0 .

# run
docker run --rm \
  -v $PWD/../../toy-dataset:/dataset -v $PWD/output:/output \
  registry.webis.de/code-research/tira/tira-user-TIRA_USER_FOR_AUTOMATIC_REPLACEMENT/random-baseline-notebook:1.0.0

# view result
cat output/predictions.tsv
```

### Server usage
Start a server that provides the `predict`-function over HTTP:
```bash
# Either for local usage (after installation):
tira-run-inference-server --notebook random_baseline.ipynb --port 8787

# Or for docker usage (after building):
docker run --rm -it --publish 8787:8787 --entrypoint tira-run-inference-server valueeval24-random-baseline-notebook:1.0.0 \
  --notebook random_baseline.ipynb --port 8787
```
Then in another shell:
```bash
curl -X POST -H "application/json" \
  -d "[\"Our nature must be protected\", \"We do not always get what we want\"]" \
  localhost:8787
```

### TIRA usage
- Define actions in [.github/workflows](.github/workflows/)
- Use via [Actions](https://github.com/tira-io/valueeval-2024-human-value-detection-TIRA_USER_FOR_AUTOMATIC_REPLACEMENT/actions)


## Develop your own approach
- See the [random-baseline](../random-baseline/) if you prefer to work with plain Python scripts instead of notebooks
- Modify "Setup" and "Prediction"
- At the start of the [Dockerfile](Dockerfile) is an alternative `FROM` instruction to use PyTorch and GPUs (works with TIRA)
- You can integrate our [model_downloader](../model-downloader/) to download models from Hugging Face Hub

