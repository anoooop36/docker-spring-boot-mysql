## Reference Doc:
    https://spring.io/guides/gs/accessing-data-mysql

## To create image of Spring Boot Application run (update application.properties to change mysql connection details):
    ./gradlew bootBuildImage

## To run Mysql image and Spring Boot application use command (using docker):
    docker compose up


## Run kubernets mysql service
    kubectl apply -f mysql-deployment.yaml

## Run kubernetes demo app service
    kubectl apply -f deployment.yaml

## Access demo service apis using port-forwarding (need for local testing)
    kubectl port-forward svc/demo 8080:8080


## api end point to get all users
    http://localhost:8080/demo/all


# Load Balancing trafic to demo service pods
## Reference doc: 
> https://kubernetes.github.io/ingress-nginx/deploy/
## Create nginx ingress controller
> kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.0-beta.0/deploy/static/provider/cloud/deploy.yaml
## Create ingress rule to route traffic to demo service
> kubectl create ingress demo-localhost --class=nginx --rule="demo.localdev.me/*=demo:8080"
## port-forward to test it in local
> kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 8084:80
## use local dns resolution to hit demo service apis
> curl --resolve demo.localdev.me:8084:127.0.0.1 http://demo.localdev.me:8084/demo/all
## access demo serivce apis in browser
> http://demo.localdev.me:8084/demo/all
