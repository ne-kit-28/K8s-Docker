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
5.1) minikube docker-env
minikube docker-env | Invoke-Expression установка окружения
minikube docker-env --unset | Invoke-Expression возврат в исходное состояние
6) cinema.yaml: (Для локального репозитория используя )
______________________________________________________
apiVersion: v1
kind: Pod
metadata:
  name: cinema
spec:
  containers:
    - image: 172.29.224.1:5000/cinema:latest //мой ip (?)
      name: cinema
      ports:
        - containerPort: 80
_______________________________________________________
# cinema-deployment.yaml
apiVersion: apps/v1 //apps так как это Deployment
kind: Deployment
metadata:
  name: cinema-deployment
spec:
  replicas: 2
  template:
    metadata:
      labels:
        app: cinema-app
    spec:
      containers:
        - name: cinema-container
          image: nekit28/cinema:first
          imagePullPolicy: Never // IfNotPresent
          ports:
            - containerPort: 40001
  selector:
    matchLabels:
      app: cinema-app
______________________________________________________
bot.yaml:
apiVersion: v1
kind: Pod
metadata:
  name: bot
spec:
  containers:
    - image: nekit28/bot:first
      name: bot
      securityContext:
          runAsUser: 0
      ports:
        - containerPort: 80
7) kubectl create -f bot.yaml
8) kubectl apply -f cinema-deployment.yaml
9) kubectl logs deployment/cinema-deployment для логов
