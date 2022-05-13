# commands

## create docker network
docker network create mongo-network

## start mongodb
docker run -d \
    -p 27017:27017  \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    --name mongodb \
    --net mongo-network \
    mongo

## start mongo-express
docker run -d \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME="admin" \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD="password" \
    --network mongo-network \
    --name mongo-express \
    -e ME_CONFIG_MONGODB_SERVER="mongodb" \
    mongo-express

## experiments
docker run -d \
    -p 3000:3000 \
    --network mongo-network \
    --name webapp \
    nanajanashia/k8s-demo-app:v1.0


    #-e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
    #-e ME_CONFIG_BASICAUTH_USERNAME="user" \
    #-e ME_CONFIG_BASICAUTH_PASSWORD="fairly long password" \