## Building the Image
Here, first imagine you have the appropriate `Dockerfile` (which is a challenge itself!), then you can build it:
```shell
docker build --progress=plain -t your-container-name -f Dockerfile .
```

### Best Practices
#### Cache
Building images could be time consuming ([[vizard/Intro|Vizard]] project takes around 25min and it is around 10GB; it has tone of dependencies, e.g., PyTorch, DVC, MLflow, etc). So, it is highly important to use s **caching** as much as possible, particularly:
- **Writing `Dockerfile` for the first time**
- **Editting source code** but not dependencies

>[!NOTE] Docker Layering
>If you change a layer, all layers on top of it need to be built again!

So put all the changing layers at the topest possible layer! E.g.:
| Bad | Good |
| ---- | ------ |
| ![[Pasted image 20230514131331.png]] | ![[Pasted image 20230514131447.png]] |

*caption: in this example, step `yarn intall --production` won't be triggered every time we change the source code, since the dependencies are not changing, there is no need!*

## Conda to Docker
Well, everything is fine with the `conda` for multi platform cases until what it exports is useless! So, methods such as below does not work:
```shell
conda env export > environment.yml
# then import
```

>[!Warning] Activating a conda env in a docker image is different!

Steps:
1. Use a base `conda`, `mamba`, `miniconda`, etc image:
```
FROM continuumio/miniconda3
```
2. \[OPTIONAL\] In case you did not install `mamba` but want it:
```
RUN conda install -y mamba -c conda-forge
```
3. Create the environment:
```shell
COPY environment.yml .
RUN conda env create -f environment.yml
```
4. Make `RUN` commands use the new environment:
```shell
SHELL ["conda", "run", "-n", "YOUR_ENV_NAME", "/bin/bash", "-c"]
```
5. \[For starting container\] The code to run when container is started:
```shell
COPY some_py_file.py .
ENTRYPOINT ["conda", "run", "--no-capture-output", "-n", "YOUR_ENV_NAME", "python", "some_py_file.py"]
```

>[!NOTE] All thanks to this blog post [Activating a Conda environment in your Dockerfile (pythonspeed.com)](https://pythonspeed.com/articles/activate-conda-dockerfile/))
