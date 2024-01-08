# weather-app-microservice

# Steps Using Helm Charts:

## MYSQL DB:

```t
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install mysql bitnami/mysql --version 9.16.1 --set auth.rootPassword=dbpassword
```
## Auth:

```t
helm upgrade --install weather-app-auth weather-app-helm-charts/weather-app-auth/weather-app-auth-0.1.0.tgz
```
## Weather:

```t
helm upgrade --install weather-app-weather --set apikey=ecbc396f46mshb65cbb1f82cf334p1fcc87jsna5e962a3c542 weather-app-helm-charts/weather-app-weather/weather-app-weather-0.1.0.tgz
```
## UI

```t
 helm upgrade --install weather-app-ui weather-app-helm-charts/weather-app-ui/weather-app-ui-0.1.0.tgz
```

# Steps using Docker Containers:

## MYSQL DB:

```t
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=aditya mysql
```

## Auth:

```t
docker build -t auth:v1.0.0 auth/
docker run -d -p 8080:8080 -e DB_HOST=172.17.0.1 -e DB_PASSWORD=aditya auth:v1.0.0
```
```bash
curl -XPOST -d '{"user_name":"user1","user_password":"mypass"}' localhost:8080/users

curl -XPOST -d '{"user_name":"user1","user_password":"mypass"}' localhost:8080/users/user1
```

## Weather:

```t
docker build -t weather:v1.0.0 weather/
docker run -d -p 5000:5000 -e APIKEY=ecbc396f46mshb65cbb1f82cf334p1fcc87jsna5e962a3c542 weather:v1.0.0
```

## UI:

```t
docker build -t ui:v1.0.0 ui/
docker run -d -p 3000:3000 -e AUTH_HOST=172.17.0.1 -e AUTH_PORT=8080 -e WEATHER_HOST=172.17.0.1 -e WEATHER_PORT=5000 ui:v1.0.0
```

# Steps using Docker Compose:

```t
docker compose up -d
```