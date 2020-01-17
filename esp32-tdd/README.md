docker build . -t esp-idf-tdd:latest

docker container run -it -v$(pwd):/workdir --rm toddflanders/esp-idf-tdd bash

