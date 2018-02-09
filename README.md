# istio-intro
getting to know istio meetup content

## Setup
- DEMO.md
- Follow all instructions for dev accounts in the [flight-status README](https://github.com/estesp/flightassist/blob/master/README.md#external-service-pre-requisites)
- Download or clone [flightstatus code](https://github.com/estesp/flightassist)
- Build flightassist local image and tag to your desired repository
```bash
cd flightassist
make localimage
docker tag $SHA mydockerrepo/flightassist:0.0.1
docker push mydockerrepo/flightassist:0.0.1
```
- Fill in [secrets.yaml](https://github.com/estesp/flightassist/blob/master/secret.yaml)
- Download or clone [flightassist-weather](https://github.com/estesp/flightassist-weather)

- Build fi local image and tag to your desired repository
```bash
cd flightassist-weather
make localimage
docker tag weather-service:v1 mydockerrepo/weather-service:0.0.1
docker push mydockerrepo/weather-service:0.0.1
```

