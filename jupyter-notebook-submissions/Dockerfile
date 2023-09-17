FROM webis/tira-ir-starter-pyterrier:0.0.3-base

ADD *.ipynb /workspace

ADD example-ir-dataset /tmp-delete-ir-dataset

RUN export TIRA_INPUT_DIRECTORY=/tmp-delete-ir-dataset \
	&& export TIRA_OUTPUT_DIRECTORY=/tmp \
	&& ./run-pyterrier-notebook.py --input ${TIRA_INPUT_DIRECTORY} --output ${TIRA_OUTPUT_DIRECTORY} --notebook /workspace/pyterrier-notebook.ipynb \
	&& rm -R /tmp-delete-ir-dataset \
	&& head -3 /tmp/run.txt \
	&& rm /tmp/run.txt \
	&& rm -R /root/.ir_datasets
