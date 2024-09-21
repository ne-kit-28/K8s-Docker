# K8s-Docker
1) docker login -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
2)Tag your image build.
My image name here is bot and by default it has tag latest, My username is nekit28 as registered with docker cloud, and I created a public repository named bot.
So my personal repository becomes now nekit28/bot and I want to push my image with tag first.
I tagged as below :
docker tag bot:latest nekit28/bot:first
3) Pushed the image to my personal docker repository as below
docker push docker push nekit28/bot:first
4) minikube start
5) kubectl get nodes
6) cinema.yaml:
apiVersion: v1
kind: Pod
metadata:
  name: cinema
spec:
  containers:
    - image: 172.29.224.1:5000/cinema:latest
      name: cinema
      ports:
        - containerPort: 80

bot.yaml:
apiVersion: v1
kind: Pod
metadata:
  name: bot
spec:
  containers:
    - image: nekit28/bot:first
      name: bot
      ports:
        - containerPort: 80
7) kubectl create -f bot.yaml
