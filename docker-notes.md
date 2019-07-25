# Docker Notes 

## Removing Containers 

### Tagged with <none>

```bash 
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

This works by using rmi with a list of image ids. To get the image ids we call docker images then pipe it to grep "^\<none>'". The grep will filter it down to only lines with the value “\<none>” in the repository column. Then to extract the id out of the third column we pipe it to awk "{print $3}" which will print the third column of each line passed to it.

see source [here](https://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html)

### Stopped containers 

```bash
docker rm $(docker ps -a -q)
```

This will remove all stopped containers by getting a list of all containers with docker ps -a -q and passing their ids to docker rm. This should not remove any running containers, and it will tell you it can’t remove a running image. 

see source [here](https://jimhoskins.com/2013/07/27/remove-untagged-docker-images.html)

## Registry 

### Query 

#### Get all images 

```bash
curl -s -X GET https://myregistry:5000/v2/_catalog
> {"repositories":["redis","ubuntu"]}
```

-s == silent mode 

#### Get all tags

```bash
curl  -s -X GET https://myregistry:5000/v2/ubuntu/tags/list
> {"name":"ubuntu","tags":["14.04"]}
```

