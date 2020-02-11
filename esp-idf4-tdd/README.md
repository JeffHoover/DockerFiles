# esp23-tdd

## to run the docker image from Todd's public docker registry (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm toddflanders/esp-idf4-tdd bash
```

## to build the docker file locally
```
docker build . -t esp-idf4-tdd:latest
```

## to run the locally built docker image (mounting the current working directory as 'workdir'):
```
docker container run -it -v$(pwd):/workdir --rm esp-idf4-tdd bash
```

## to publish your locally built docker image:
```
docker tag esp-idf4-tdd toddflanders/esp-idf4-tdd:<version>
docker push toddflanders/esp-idf4-tdd:<version>
docker push toddflanders/esp-idf4-tdd:latest
```
