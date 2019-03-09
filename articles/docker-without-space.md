# No space left on device error

If you got this error running docker you need resize you image.

Docker on Mac OSX create a file located on 
```
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
``` 
where contains everything (at least I think so)... this image by default is created with a size of 20GB.

How to fix it?
You could try these commands which release data unused. 

## Cleanup
Delete the orphaned volumes in Docker, you can use the built-in docker volume command. The built-in command also deletes any directory in `/var/lib/docker/volumes` that is not a volume so make sure you didn't put anything in there you want to save.

```
docker rmi $(docker images -q -f "dangling=true")
```

Remove stopped containers.
```
docker rm $(docker ps -q -f 'status=exited')
```

Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are dangling (not associated with a container):

```
docker system prune
```

Also consider removing all the unused Images.

```
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

if error is present, the solution is resize the default image.

```
rm ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
```

Restart docker


```
/Applications/Docker.app/Contents/MacOS/qemu-img resize \ 
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2 +10G
```

Happy Hacking
