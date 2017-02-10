# No space left on device error

If you got this error running docker you need resize you image.

Docker on Mac OSX create a file 
```
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
``` 
where contains everything (at least I think so)... this image by default is created with a size of 20GB.

How to fix it?
You could try these commands which release data unused. 

```
docker rm $(docker ps -q -f 'status=exited')
docker rmi $(docker images -q -f "dangling=true")
```

if error is present, the solution is resize the default image.

```
rm ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2
```

```
Restart docker
```

```
/Applications/Docker.app/Contents/MacOS/qemu-img resize \ 
~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/Docker.qcow2 +10G
```

Happy Hacking
