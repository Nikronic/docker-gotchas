## Persist the DB
| <div style="width:290px"></div> | Named volumes | Bind mounts |
| :---: | :---: | :---: |
| Host location | Docker chooses | You decide |
| Mount example (using `--mount`) | `type=volume,src=my-volume,target=/usr/local/data` | `type=bind,src=/path/to/data,target=/usr/local/data` |
| Populates new volume with container contents | Yes | No |
| Supports Volume Drivers | Yes | No |

## Multi container apps
>*"Install it in the same container or run it separately?"*

In general, **each container should do one thing and do it well**. The following are a few reasons to run the container separately:
- There’s a good chance you’d have to *scale APIs and front-ends differently* than databases.
- Separate containers let you version and *update versions in isolation*.
- While you may use a container for the database locally, you may want to *use a managed service
  for the database in production*. You don’t want to ship your database engine with your app then.
- *Running multiple processes will require a process manager* (the container only starts one process), which adds complexity to container startup/shutdown. (For a real world example in our projects see [[Deployment#Process Management]])

### Container Networking
Containers, by default, run in isolation and don’t know anything about other processes or containers on the same machine. But, **containers on the same network, they can talk** to each other.

There are two ways to put a container on a network:
- Assign the network *when starting* the container.
- Connect an *already running* container to a network.

You can use similar commands to creating a `volume` for creating new network, i.e.
```bash
docker network create network-name # create network
docker run -d --network network-name --network-alias network-name-alias ...  # connect networ to a container
```
