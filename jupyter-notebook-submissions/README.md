```
docker build -t xyz .
```

```
tira-run --image xyz --input-directory example-ir-dataset --command './run-pyterrier-notebook.py --input ${TIRA_INPUT_DIRECTORY} --output ${TIRA_OUTPUT_DIRECTORY} --notebook /workspace/pyterrier-notebook.ipynb'
```
