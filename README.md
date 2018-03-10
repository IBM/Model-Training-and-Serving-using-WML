# Model Training and Serving using WML

## Preequisite

Install Bluemix CLI and Machine Learning Plugin

## Provision your WML instance, and setup CLIs

### 1. Create an instance of WML service and associated key using BX command line

``` shell
bx cf create-service pm-20 lite Animesh-WML
bx cf create-service-key Animesh-WML Animesh-WML-Key
``` 

### 2. Get your service credentials
``` shell
bx cf service-key Animesh-WML Animesh-WML-Key
```

### 3. Install the Blumix bx cli and Machine learning plugin, and set it up with your creds obtained in step 2.

``` shell
    bx plugin install ml_cli_plugin_osx
    export ML_INSTANCE=11111111-aaaa-2222-bbbb-333333333333
    export ML_USERNAME=44444444-cccc-5555-dddd-666666666666
    export ML_PASSWORD=77777777-eeee-8888-ffff-999999999999
    export ML_ENV=<url from credentials>
 ```
 
## Provision an Object Storage Instance, and upload training data

``` shell
We pre upload training data  in our own object storage here, so users dont need to do this
``` 

## Package the Model graphs in zip

``` shell
Like before, we prepackage it and keep it in object store, and ask users to download it to their machine
``` 

## Create a Training Manifest File

``` shell
Like before, we pre create it and keep it in object store, and ask users to download it to their machine
``` 

## Submit, Monitor and Store a Training RUN (Note: need to download the BX deep learning add-ons)
``` shell
bx ml train tf-model.zip tf-train.yaml
bx ml list training-runs
bx ml show training-runs training-DOl4q2LkR
bx ml monitor training-runs training-DOl4q2LkR
``` 
## Deploy and Serve Models

