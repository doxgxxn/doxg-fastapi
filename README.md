# doxg-api 
   
preparation 

    https://pdm.fming.dev/latest/#installation
    
    $ source .venv/bin/activate
    $ pdm add fastapi
    $ pdm add "uvicorn[standard]"
    $ pdm add -dG test pytest pytest-cov
  
RUN SERVER

    http://localhost:8000
    $ uvicorn app.main:app --reload                 ### --reload 옵션: 코드 변경 감지, 개발 시 자동 재시작
    INFO:     Will watch for changes in these directories: ['/home/doxg/code/doxg-api']
    INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)          
    INFO:     Started reloader process [20346] using WatchFiles
    INFO:     Started server process [20348]
    INFO:     Waiting for application startup.
    INFO:     Application startup complete.
    INFO:     127.0.0.1:45600 - "GET /weather HTTP/1.1" 200 OK
    
API

    http://localhost:8000/docs
    $ curl -X 'GET' 'http://localhost:8000/weather' -H 'accept: application/json'
    {"location":"동작구 신대방2동","weather_condition":"맑음","temperature":"18.4"}
    
    $ curl http://localhost:8000/weather
    {"location":"동작구 신대방2동","weather_condition":"맑음","temperature":"18.4"}
    
Docker

    http://localhost:9040/docs
    $ docker build -t doxg-api:0.4.0 .
    $ docker run -dit --name doxg-api040 -p 9040:80 doxg-api:0.4.0

Deploy fly.io
    
    $ flyctl launch
    Visit your newly deployed app at https://doxg-api.fly.dev/
    
Reg Docker Hub

    https://hub.docker.com/r/doxgxxn/doxg-api/tags
    $ docker build -t doxgxxn/doxg-api:0.6.0 .
    $ docker push doxgxxn/doxg-api:0.6.0
    $ docker tag doxgxxn/doxg-api:0.6.0  doxgxxn/doxg-api:latest
    $ docker images
    REPOSITORY           TAG       IMAGE ID       CREATED          SIZE
    pysatellite/dj-api   0.6.1     29d4162e7fb5   32 minutes ago   1.04GB
    pysatellite/dj-api   latest    29d4162e7fb5   32 minutes ago   1.04GB

    $ docker push doxgxxn/doxg-api
    Using default tag: latest
    The push refers to repository [docker.io/doxgxxn/doxg-api]
    85ef78d095d2: Layer already exists
    5b83e684ed37: Layer already exists
    e78fcb2a5a29: Layer already exists
    aeb76cec1d43: Layer already exists
    b343d97c2c3c: Layer already exists
    70981c1da3c1: Layer already exists
    6a4ba3269682: Layer already exists
    d3de4ba9f72c: Layer already exists
    0c2d6fc19d6a: Layer already exists
    2ef3351afa6d: Layer already exists
    5cc3a4df1251: Layer already exists
    2fa37f2ee66e: Layer already exists
    latest: digest: sha256:44f4741c8340c8e2a742f739a3a0d1e1b44da5787511c842761be894e7329104 size: 2840

ref

    https://fastapi.tiangolo.com/ko/#_4
    https://fastapi.tiangolo.com/ko/deployment/docker/?h=docker
