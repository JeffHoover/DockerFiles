# esp23-tdd

## to run the docker image from Todd's public docker registry (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm toddflanders/esp-idf3-tdd bash
```

## to build the docker file locally
```
docker build . -t esp-idf3-tdd:latest
```

## to run the locally built docker image (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm esp-idf3-tdd bash
```

## to publish your locally built docker image:
```
docker tag esp-idf3-tdd toddflanders/esp-idf3-tdd:<version tag>
docker push toddflanders/esp-idf-tdd:<version tag>
docker push toddflanders/esp-idf-tdd:latest
```
