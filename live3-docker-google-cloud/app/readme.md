# Docker com Cloud na Prática

## Passos

- Download app.zip: https://www.dropbox.com/s/tu5asei37iqp6ya/app-pt.zip?dl=0
- Crie o arquivo Dockerfile

```
    FROM python:3

    COPY ./requirements.txt /app/requirements.txt

    WORKDIR /app

    RUN pip install --no-cache-dir -r requirements.txt

    COPY . /app

    ENTRYPOINT [ "python" ]

    CMD [ "app.py" ]
```

- Zip e Upload app.zip para o Cloud Shell
- Unzip app.zip
- Crie (Build) a Docker image

```
    docker build -t app:1.0 .
    docker image ls
```

- Teste a imagem localmente no Cloud Shell

```
    docker container run --name app -p 5000:5000 app:1.0
    docker container ls 
    docker container ls --all
    docker container start app
    docker container stop app
```

- Adicione tag a imagem

```
    docker tag app:1.0 us.gcr.io/<ID_PROJETO>/app
```

- Suba (Push) a imagem para Container Registry na Google Cloud

```
    docker push us.gcr.io/<ID_PROJETO>/app
```

- Faça o deploy da aplicação em container no Google Cloud Run usando a imagem criada