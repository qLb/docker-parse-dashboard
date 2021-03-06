
[![](https://images.microbadger.com/badges/image/ball6847/parse-dashboard.svg)](https://microbadger.com/images/ball6847/parse-dashboard "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/version/ball6847/parse-dashboard.svg)](https://microbadger.com/images/ball6847/parse-dashboard "Get your own version badge on microbadger.com")
[![Docker Automated buil](https://img.shields.io/docker/automated/jrottenberg/ffmpeg.svg)](https://hub.docker.com/r/ball6847/parse-dashboard/)

# Docker Image for parse-dashboard

Dashboard for parse-server

## Running using Docker Compose

```yml
version: '2'

services:
  parse-server:
    image: ball6847/parse-server:2.3.2
    depends_on:
      - mongo
    environment:
      - PARSE_SERVER_APPLICATION_ID=myAppId
      - PARSE_SERVER_MASTER_KEY=masterKey
      - PARSE_SERVER_DATABASE_URI=mongodb://mongo:27017/db
    ports:
      - 1337:1337
  parse-dashboard:
    image: ball6847/parse-dashboard:1.0.25
    depends_on:
      - parse-server
    environment:
      - PARSE_DASHBOARD_SERVER_URL=http://localhost:1337/parse
      - PARSE_DASHBOARD_ALLOW_INSECURE_HTTP=true
      - PARSE_DASHBOARD_MASTER_KEY=masterKey
      - PARSE_DASHBOARD_APP_ID=myAppId
      - PARSE_DASHBOARD_APP_NAME=myApp
      - PARSE_DASHBOARD_USER_ID=admin
      - PARSE_DASHBOARD_USER_PASSWORD=admin
    ports:
      - 4040:4040
  mongo:
    image: mongo:3.4.1
```
