# docker
docker cleanup commands

# Remove not running containers
docker ps -a | grep 'Exited' | awk '{print $1}' | xargs --no-run-if-empty docker rm

# Remove old containers
docker ps -a | grep 'weeks ago' | awk '{print $1}' | xargs --no-run-if-empty docker rm

# Remove not tagget images
docker images | grep "<none>" | awk '{print $3}' | xargs docker rmi

# Delete all containers
docker rm $(docker ps -a -q)

# Delete all images
docker rmi $(docker images -q)

# Actually clean up stopped containers:
docker rm -v $(docker ps -a -q -f status=exited)

# delete dangling images
docker rmi $(docker images -q -f dangling=true)
