# docker_flask_ubuntu_minimal


## Remove Old Files 
```
$ sudo docker system prune
```

## First Setup Bash Script
```
$ touch Dockerfile; touch requirements.txt; touch readme.txt; mkdir app; cd app; touch app.py; cd ..
```

## Requirements.txt
```
Flask
```

# Dockerfile
```
FROM ubuntu:18.04

RUN apt-get update -y && \
    apt-get install -y python3-pip python3-dev

RUN touch requirements.txt

COPY ./requirements.txt /requirements.txt

WORKDIR /

RUN pip3 install -r requirements.txt

COPY . /

ENTRYPOINT [ "python3" ]

CMD [ "app/app.py" ]
```







# app.py
```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
  return """
  <h1>Hello World!</h1>
  <h6>Python Flask App via Docker</h6>
  <p> |O...O| </p>
  """

if __name__ == "__main__":
    app.run(debug=True, host='0.0.0.0')
```

## Build your Docker image
The period "." is not a typo:
```
sudo docker build -t flast_test .
```

Successful builds outputs these lines at end:
```
Successfully built ############
Successfully tagged ###:latest
```

## Run your Docker container
```
$ sudo docker run --name flaskapp -v$PWD/app:/app -p5000:5000 flast_test:latest
```

Now the application can be accessed at 
http://localhost:5000 
or 
http://0.0.0.0:5000/




# Resources

https://docs.docker.com/engine/install/ubuntu/

https://duckduckgo.com/?t=ffsb&q=%3Ch1%3EPython+Flask+App+via+Docker%3C%2Fh1%3E&ia=web 
