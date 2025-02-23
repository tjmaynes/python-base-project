install:
	chmod +x ./scripts/install.sh
	./scripts/install.sh

lint:
	. .venv/bin/activate; python -m mypy --strict {{ cookiecutter.project_slug }}/
	. .venv/bin/activate; python -m ruff check {{ cookiecutter.project_slug }}/

format:
	. .venv/bin/activate; python -m ruff format {{ cookiecutter.project_slug }}/

test:
	. .venv/bin/activate; python -m pytest {{ cookiecutter.project_slug }} \
		--doctest-modules \
		--junitxml=reports/test-results-$(shell cat .python-version).xml

.PHONY: build
build: clean lint test
	python -m build

deploy: install build

ship_it: build
	git push

start:
	python -m {{ cookiecutter.project_slug }}.main

clean:
	rm -rf dist/ build/ reports/ *.egg-info/ *cache