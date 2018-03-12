# Model Training and Serving using WML

## Preequisite

Install [Bluemix CLI](https://console.bluemix.net/docs/cli/reference/bluemix_cli/get_started.html#getting-started) and [Machine Learning Plugin]()

``` shell
bx plugin install ml_cli_plugin_osx
bx target -o ORG -s SPACE
``` 

## 1. Provision your WML instance


### 1.1 Create an instance of WML service and associated key using BX command line

``` shell
bx cf create-service pm-20 lite Animesh-WML
bx cf create-service-key Animesh-WML Animesh-WML-Key
``` 

### 1.2 Get your service credentials
``` shell
bx cf service-key Animesh-WML Animesh-WML-Key
```

### 1.3 Set the Machine Learning plugin it up with your creds obtained in step 2

``` shell
export ML_INSTANCE=11111111-aaaa-2222-bbbb-333333333333
export ML_USERNAME=44444444-cccc-5555-dddd-666666666666
export ML_PASSWORD=77777777-eeee-8888-ffff-999999999999
export ML_ENV=<url from credentials>
 ```
### 1.4 Test your WML instance

``` shell
AnimeshMacBook:~ animeshsingh$ bx ml list training-runs
Fetching the list of training runs ...
SI No   Name   guid   status   framework   version   submitted-at   

0 records found.
OK
List all training-runs successful
 ```
 
## Provision an Object Storage Instance, and upload training data

Provision an [Object Storage instance](https://console.bluemix.net/catalog/services/cloud-object-storage), and then setup your AWS S3 command line. You then need to upload data in your Object storage. Here we are getting the data sets from [THE MNIST DATABASE
of handwritten digits](http://yann.lecun.com/exdb/mnist/)

``` shell
export AWS_ACCESS_KEY_ID=test
export AWS_SECRET_ACCESS_KEY=test

# Create your training data and result buckets
aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 mb <trainingDataBucket>
aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 mb <trainingResultBucket>

aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 cp t10k-labels-idx1-ubyte.gz s3://test-data-animesh/
aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 cp train-labels-idx1-ubyte.gz s3://test-data-animesh/
aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 cp t10k-images-idx3-ubyte.gz s3://test-data-animesh/
aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 cp train-images-idx3-ubyte.gz s3://test-data-animesh/

aws --endpoint-url=http://s3-api.us-geo.objectstorage.softlayer.net s3 ls s3://test-data-animesh
2018-03-10 00:14:49    1648877 t10k-images-idx3-ubyte.gz
2018-03-10 00:13:12       4542 t10k-labels-idx1-ubyte.gz
2018-03-10 00:15:22    9912422 train-images-idx3-ubyte.gz
2018-03-10 00:14:31      28881 train-labels-idx1-ubyte.gz
``` 

## Create Model graphs Zip

``` shell
Like before, we prepackage it and keep it in object store, and ask users to download it to their machine
``` 

## Create a Training Run Manifest File

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

