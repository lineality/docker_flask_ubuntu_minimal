# docker_flask_ubuntu_minimal
# Overview
Here is sample minimal code for running keras-ocr in a flask docker image.

Follow each step and run each command in your terminal. Instructions that start with "$" are likely terminal commands. Other instructions will be text to copy into files.


## New Project Folder
It is recommended that you create a project-folder and then do your work in that folder("directory"). Run this line of code to create a project folder and then make that folder the "current working directory" where your terminal opera"my_project_folder" is arbitrary, you can name your project anything you like.
```
$ mkdir my_project_folder; cd my_project_folder
```


## Check Docker Memory Use 
Check if docker is still using memory in any area:
```
sudo docker system df
```

## Remove Old Files (optional)
```
$ sudo docker system prune; sudo docker image prune; sudo docker volume prune; sudo docker container prune
```

## First Setup Bash Script
```
$ touch Dockerfile; touch requirements.txt; touch readme.txt; mkdir app; cd app; touch app.py; cd ..
```

## readme.md / readme.txt 
Having a readme or instructions file is helpful for documentation and clear communication. You can put the contents of this guide into that readme file. 
```
# Instructions and Guide
```



## requirements.txt
Add this text to your file. This specific minimal project has no required text, no required packages, but some docker applications require a 'requirements.txt' file even if that file is blank. (e.g. AWS-lambda-function docker-containers)
```
Flask
```

# Dockerfile
Add this text to your file. 
```
# Get docker base image
FROM ubuntu:18.04

# Update ubuntu linux software and packages
RUN apt-get update -y

# Install and update pip and python-dev 
RUN apt-get install -y python3-pip python3-dev

# Import requirements.txt into docker
COPY ./requirements.txt /requirements.txt

# Set working directory
WORKDIR /

# Install python requirements
RUN pip3 install -r requirements.txt

# Copy all files in project directory into docker
COPY . /

# Specify the executable to run
ENTRYPOINT [ "python3" ]

CMD [ "app/app.py" ]
```







# app.py
Add this text to your file. 
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
Add this text to your file. 

"project_abc" is an arbitrary project name, you can use any name you like.

The final period "." is not a typo:
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

## See you results in a browser
Now the application can be accessed at 

http://localhost:5000 or  http://0.0.0.0:5000/

#### Successful run should print a display to a browser.
```
Hello, World... etc.
```


## Remove Old Files 
```
$ sudo docker system prune; sudo docker image prune; sudo docker volume prune; sudo docker container prune
```


## Remove Old Files  (optional)
Check if docker is still using memory in any area:
```
sudo docker system df
```



## Sources and Resources
- use ubuntu, install docker
- https://docs.docker.com/engine/install/ubuntu/
- https://www.educba.com/docker-entrypoint/
- https://linuxhint.com/docker-entrypoint-beginner-guide/ 
- https://duckduckgo.com/?t=ffsb&q=%3Ch1%3EPython+Flask+App+via+Docker%3C%2Fh1%3E&ia=web 
