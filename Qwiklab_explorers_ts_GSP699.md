# Migrating a Monolithic Website to Microservices on Google Kubernetes Engine || [GSP699](https://www.cloudskillsboost.google/course_templates/638/labs/480368) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

* ### Run the following Commands in CloudShell
```
cd ~
git clone https://github.com/googlecodelabs/monolith-to-microservices.git
cd ~/monolith-to-microservices
./setup.sh

gcloud services enable container.googleapis.com

gcloud container clusters create fancy-cluster --num-nodes 3 --machine-type=e2-standard-4
```
```
cd ~/monolith-to-microservices
./deploy-monolith.sh

kubectl get service monolith

cd ~/monolith-to-microservices/microservices/src/orders
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0 .

kubectl create deployment orders --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/orders:1.0.0

kubectl expose deployment orders --type=LoadBalancer --port 80 --target-port 8081
```
```
kubectl get service orders
```
* ### Run that command again & again, until get the `external IP address`
```
cd ~/monolith-to-microservices/react-app
nano .env.monolith
```
```
REACT_APP_ORDERS_URL=http://<ORDERS_IP_ADDRESS>/api/orders
REACT_APP_PRODUCTS_URL=/service/products
```
* ### Replace `<ORDERS_IP_ADDRESS>` with the `external IP adress`
* ### Then follow next steps from video
* ### Now, press `Ctrl+C` then `shift+y` and then hit `enter` key
```
npm run build:monolith

cd ~/monolith-to-microservices/monolith
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:2.0.0 .

kubectl set image deployment/monolith monolith=gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:2.0.0
```
```
cd ~/monolith-to-microservices/microservices/src/products
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0 .

kubectl create deployment products --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/products:1.0.0

kubectl expose deployment products --type=LoadBalancer --port 80 --target-port 8082
```
```
kubectl get service products
```
* ### Run that command again & again, until get the `external IP address`
```
cd ~/monolith-to-microservices/react-app
nano .env.monolith
```
```
REACT_APP_ORDERS_URL=http://<ORDERS_IP_ADDRESS>/api/orders
REACT_APP_PRODUCTS_URL=http://<PRODUCTS_IP_ADDRESS>/api/products
```
* ### Replace `<ORDERS_IP_ADDRESS>` with the previous got `external IP address` and `<PRODUCTS_IP_ADDRESS>` with recent got `external IP address`
* ### Then follow next steps from video
* ### Now, press `Ctrl+C` then `shift+y` and then hit `enter` key
```
npm run build:monolith

cd ~/monolith-to-microservices/monolith
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:3.0.0 .

kubectl set image deployment/monolith monolith=gcr.io/${GOOGLE_CLOUD_PROJECT}/monolith:3.0.0
cd ~/monolith-to-microservices/react-app
cp .env.monolith .env
npm run build

cd ~/monolith-to-microservices/microservices/src/frontend
gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0 .

kubectl create deployment frontend --image=gcr.io/${GOOGLE_CLOUD_PROJECT}/frontend:1.0.0

kubectl expose deployment frontend --type=LoadBalancer --port 80 --target-port 8080
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)


