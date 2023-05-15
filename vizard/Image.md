### Using `cache` in Docker
![[Pasted image 20230514132451.png]]

### Using `dvc` and Docker
Well, DVC has different way of tracking a data corresponding to a repo. Usually we set it to track the git repo and all files inside that repo handled by DVC. In this case we would have:
```python
# data versioning config
PATH = 'raw-dataset/all-dev.pkl'  # path to some files tracked via DVC
REPO = 'home/nik/visaland-visa-form-utility'  ### IMPORTANT ###
VERSION = 'v1.2.5-dev' # tag used inside git for versioning

# get url data from DVC data storage
data_url = dvc.api.get_url(path=PATH, repo=REPO, rev=VERSION)
```

Now, since I have used absolute path (or any other path that is *inconsiderate of docker `WORKDIR`*), `dvc` will complain that the **`WORKDIR` is not a git repo** (it was in original repo, but it is now in `WORKDIR` that is not a git repo). To fix this, the `REPO` path should point to `WORKDIR`, i.e., `REPO = "Docker.WORKDIR"`. In other words:

First, we need to set the working directory in the `Dockerfile` to whatever original repo was (which DVC used it too; i.e., the root directory where `Dockerfile` is in it):
```Dockerfile
WORKDIR /visaland-visa-form-utility
```
Then, now I point to the exact same path, in my code where DVC wants it:
```python
# data versioning config
PATH = 'raw-dataset/all-dev.pkl'  # path to some files tracked via DVC
REPO = '/visaland-visa-form-utility'  ### IMPORTANT ###
VERSION = 'v1.2.5-dev' # tag used inside git for versioning

# get url data from DVC data storage
data_url = dvc.api.get_url(path=PATH, repo=REPO, rev=VERSION)
```

>[!Warning] Take care of Paths
>Make sure you are broadcasting the path, i.e., `REPO`, `WORKDIR` should get their value from a **system-wide** value rather than geting hardcoded.

