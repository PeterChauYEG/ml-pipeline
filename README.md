# ml-pipeline


## mlflow

### setup

1. make conda env `conda create -n ml-pipeline python=3.7`
2. activate env `conda activate ml-pipeline`
3. install mlflow `pip install mlflow`


### Train

1. train with defaults `python src/sklearn_elasticnet_wine/train.py`
2. train with hypers `python src/sklearn_elasticnet_wine/train.py 0.6 0.6`
3. as a mlflow project `mlflow run src/sklearn_elasticnet_wine -P alpha=0.42`

### Monitoring

1. open the ui `mlflow ui`


### Serve model

1. serve: `mlflow models serve -m /Users/peterchau/ml-pipeline/mlruns/0/8916148ebcb44b92a0611639700ff073/artifacts/model -p 1234`
2. test: `curl -X POST -H "Content-Type:application/json; format=pandas-split" --data '{"columns":["alcohol", "chlorides", "citric acid", "density", "fixed acidity", "free sulfur dioxide", "pH", "residual sugar", "sulphates", "total sulfur dioxide", "volatile acidity"],"data":[[12.8, 0.029, 0.48, 0.98, 6.2, 29, 3.33, 1.2, 0.39, 75, 0.66]]}' http://127.0.0.1:1234/invocations`


### Deploy model 

1. build: `mlflow models build-docker -m /Users/peterchau/ml-pipeline/mlruns/0/8916148ebcb44b92a0611639700ff073/artifacts/model -n my-docker-image --enable-mlserver`
2. apply to k8s: `kubectl apply -f my-manifest.yaml`

### operations

1. local run: `docker run -p 8080:8080 my-docker-image`
2. local test: `curl -X POST -H "Content-Type:application/json; format=pandas-split" --data '{"columns":["alcohol", "chlorides", "citric acid", "density", "fixed acidity", "free sulfur dioxide", "pH", "residual sugar", "sulphates", "total sulfur dioxide", "volatile acidity"],"data":[[12.8, 0.029, 0.48, 0.98, 6.2, 29, 3.33, 1.2, 0.39, 75, 0.66]]}' http://127.0.0.1:8080/invocations`
3. 
301-2255
