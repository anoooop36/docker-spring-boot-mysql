To create image of Spring Boot Application run (update application.properties to change mysql connection details):
    ./gradlew bootBuildImage

To run Mysql image and Spring Boot application use command (using docker):
    docker compose up


Run kubernets mysql service
    kubectl apply -f mysql-deployment.yaml

Run kubernetes demo app service
    kubectl apply -f deployment.yaml

Access demo service apis using port-forwarding (need for local testing)
    kubectl port-forward svc/demo 8080:8080

