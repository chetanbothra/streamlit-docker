# Dockerize Streamlit App !  
#### _A step-by-step guide to Dockerize a streamlit app.The working way as the one available in first page of google search dont work anymore_

### prerequisite:
1. A working streamlit application
2. A linux machine with Docker installed 


Lets Begin the fun 

# Dockerizing the streamlit app

## **Step 1:**  Let’s create a Docker file.

In the working root directory, let’s create a file named ‘Dockerfile’ without any extensions.
Your file structure should be as shown.
```
root
   ├── Dockerfile
   ├── something.png
   ├── something.txt
   ├── model
   ├── nainvemodel.pkl
```
## **Step 2:**  Dockerfile's content
```
FROM python:3.7
RUN apt-get update && apt-get install -y python3-opencv
WORKDIR /app
COPY requirements.txt ./requirements.txt
RUN pip3 install opencv-python cython numpy
RUN pip3 install -r requirements.txt
EXPOSE 8501
COPY . /app
CMD streamlit run filename.py --server.enableCORS false --server.enableXsrfProtection false
```
NOTE: This is the most critical part. If you don't add ``` --server.enableCORS false --server.enableXsrfProtection false``` then the webpage would be stuck at loading screen

## **Step 3:**  Build the docker image

```
docker build -t streamlitapp:latest .
```

## **Step 4:** View docker images.
```
docker image ls`
```

## **Step 5:** Running as a container
```
docker run -p 8501:8501 streamlitapp:latest
```

# Output

It also starts our streamlit app in the following urls:

Network URL: http://172.17.0.2.8501

External URL: https://193.106.63.249:8501

With that, the Streamlit app is now deployed with docker.

hi
