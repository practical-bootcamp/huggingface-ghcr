# 🤗 Hugging Face packaging using GitHub Container Registry

This repo shows a minimalist template to create a container and package it with GitHub Actions. It contains a Dockerfile, GitHub Actions workflow, and Python code.

The web application uses FastAPI with Hugging Face and exposes a single endpoint that you can interact with it. 

Fork this repository and run the GitHub Actions as-is so that you can register your own containerized application with no modifications needed.

## Steps

1. Create a virtual env with `requirements.txt` to verify the app run 
    * run `where uvicorn` to check for uvicorn installation
    * run `uvicorn --host 0.0.0.0 main:app`
    * the app will be available on `localhost:8000`
    * go to `localhost:8000/docs` to play with the app
    * if desired, install `huggingface-cli` in dev environment for helpful functions such as `scan-cashe` and `delete-cache`. 
2. Build the Docker container
    * download and install `docker` 
    * verify installation with `where docker`
    * In the repo root where `Dockerfile` resides, run `docker build -t huggingface-local .`, where `-t` stands for `tag`
    * run the app in the container with `docker run -i -p 8000:8000 huggingface-local` where `-i` stands for `interactive` and `-p` stands for `port`. 
    * play with the app published from the container 
    * clean the cache if desired, e.g., `docker system prune --all --force --volumes`
