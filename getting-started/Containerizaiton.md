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

>[!INFO] Docker Layering
>If you change a layer, all layers on top of it need to be built again!

So put all the changing layers at the topest possible layer! E.g.:
| Bad | Good |
| ---- | ------ |
| ![[Pasted image 20230514131331.png]] | ![[Pasted image 20230514131447.png]] |

*caption: in this example, step `yarn intall --production` won't be triggered every time we change the source code, since the dependencies are not changing, there is no need!*

