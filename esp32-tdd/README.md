# esp23-tdd

## to run the docker image from Todd's public docker registry (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm toddflanders/esp-idf-tdd bash
```

## to build the docker file locally
```
docker build . -t esp-idf-tdd:latest
```

## to run the locally built docker image (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm esp-idf-tdd bash
```

## to publish your locally built docker image:
```
docker tag esp-idf-tdd toddflanders/esp-idf-tdd:1.3.0
docker push toddflanders/esp-idf-tdd:1.3.0
docker push toddflanders/esp-idf-tdd:latest
```
