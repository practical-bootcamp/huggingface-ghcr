# 🤗 Hugging Face packaging using GitHub Container Registry

This repo shows a minimalist template to create a container and package it with GitHub Actions. It contains a Dockerfile, GitHub Actions workflow, and Python code.

The web application uses FastAPI with Hugging Face and exposes a single endpoint that you can interact with. 

Fork this repository and run the GitHub Actions as-is so that you can register your own containerized application with no modifications needed.

## Steps

1. Create a virtual env with `requirements.txt` to verify the app run 
    * ensure python 3.8 is specified for the virtual env, you can do this with tools such as `pipenv` and `anaconda`. 
    * activate the virtual env and run `where uvicorn` to check for uvicorn installation
    * run `uvicorn --host 0.0.0.0 main:app` to start the app
    * the app will be available on `localhost:8000`
    * go to `localhost:8000/docs` to play with the app
    * if desired, install `huggingface-cli` in dev environment for helpful functions such as `scan-cashe` and `delete-cache` to clear up cache after the test. 
2. Build the Docker container
    * download and install `docker` from [docker.com](www.docker.com)
    * verify installation with `where docker`
    * In the repo root where `Dockerfile` resides, run `docker build -t huggingface-local .`, where `-t` stands for `tag`
    * run the app in the container with `docker run -i -p 8000:8000 huggingface-local` where `-i` stands for `interactive` and `-p` stands for `port`. 
    * play with the app published from the container 
    * clean up the cache if desired, e.g., `docker system prune --all --force --volumes`
3. Automate CI/CD packaging with Github Actions
    * check out `.github\workflows` in the repo. Note that there is no hard-coded variables in `main.yml` so it is applicable to other repos we want to automate. 
    * We don't need to write these workflows from scratch. Click on `Actions` in github and choose `New workflow` and then search for the suitable template (e.g., Publish Docker Containers)
    * Go to `Actions` and click on `CI` workflow, we can trigger its run from there. 
    * When the above run finishes, check in the github repo, you will find a package named `huggingface-ghcr` published. Click on it shows that it can be pulled from `ghcr` (github container registry) and get that FastAPI working with huggingface from anywhere. 
    * Authenticaion is needed to interact with this package, [details here](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages#authenticating-to-github-packages). 

## Userful links

This repo was part of a [course on MLOps Tools offered by Duke Univ on Coursera](https://www.coursera.org/learn/mlops-mlflow-huggingface-duke/home)

The [original repo is available on github](https://github.com/practical-bootcamp/huggingface-ghcr), I forked it and added steps above based on my testing of the repo.  