# gefyra-devcontainer

Local image + devcontainer build:

- https://code.visualstudio.com/docs/remote/devcontainer-cli

```bash
docker build ./app -t fastapi:lastest
devcontainer build --no-cache --image-name "fastapi:devcontainer" --workspace-folder "."
```

Deck setup + Gefyra bridge

```bash
deck get .
gefyra up
gefyra run -i fastapi:devcontainer -N fastapi -v $(pwd):/workspace -c "/bin/sh -c 'while sleep 1000; do :; done'"
```

Attach to container via VSCode (Using Docker extension -> right click on container -> "Attach Visual Studio Code").
Open Folder in "/workspace"

Optional:

```bash
gefyra bridge -N fastapi --deployment fastapi --port 8080:8000 --container-name fastapi-app -I myfastapi
```

Within the devcontainer try to install poetry -> Timeout error/problems

```bash
pip install poetry
```

Finish up

```bash
gefyra unbridge -A
gefyra down
deck remove --cluster .
```
