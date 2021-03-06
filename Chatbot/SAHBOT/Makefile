.PHONY: clean train-nlu train-core cmdline server

TEST_PATH=./

help:
	@echo "    clean"
	@echo "        Remove python artifacts and build artifacts."
	@echo "    train-nlu"
	@echo "        Trains a new nlu model using the projects Rasa NLU config"
	@echo "    train-core"
	@echo "        Trains a new dialogue model using the story training data"
	@echo "    action-server"
	@echo "        Starts the server for custom action."
	@echo "    cmdline"
	@echo "       This will load the assistant in your terminal for you to chat."
	@echo "    visual-graph"
	@echo "       This will give the visual graph."


clean:
	find . -name '*.pyc' -exec rm -f {} +
	find . -name '*.pyo' -exec rm -f {} +
	find . -name '*~' -exec rm -f  {} +
	rm -rf build/
	rm -rf dist/
	rm -rf *.egg-info
	rm -rf docs/_build

train-nlu:
	python3.5 -m rasa_nlu.train -c nlu_config.yml --data data/nlu.md -o models --fixed_model_name nlu --project current --verbose

train-core:
	python3.5 -m rasa_core.train -d domain.yml -s data/stories.md -o models/current/dialogue -c policy.yml

cmdline:
	python3.5 -m rasa_core.run -d models/current/dialogue -u models/current/nlu --endpoints endpoints.yml
	
action-server:
	python3.5 -m rasa_core_sdk.endpoint --actions actions

visual-graph:
	python3.5 -m rasa_core.visualize -d domain.yml -s data/stories.md -o graph.html