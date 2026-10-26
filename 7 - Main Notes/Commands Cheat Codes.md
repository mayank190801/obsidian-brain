
2024-07-17 09:01
Status: #baby
Tags: 


#### Cheatcode for cors  (pretty insane)
 open /Applications/Google\ Chrome.app --args  --disable-web-security --user-data-dir="/var/tmp/Chrome dev session"

#### Deleting process on mac 
https://medium.com/@ryanminjaeshin/how-to-fix-port-8080-already-in-use-error-on-a-mac-4e367565c688#:~:text=Now%20that%20you've%20identified,forcing%20it%20to%20terminate%20immediately.&text=Replace%2012345%20with%20the%20PID,you%20identified%20in%20step%201.

# Commands Cheat Codes

##### CSS
 https://github.com/mayank190801/CSS_Syntax/blob/main/cheatsheet.txt
#### JavaScript
 https://github.com/mayank190801/CSS_Syntax/blob/main/cheatsheet.txt

#### Docker 
- docker 
- docker run mongo 
- docker images (It will list all the images present)
- docker ps (It will list all the containers running)
- docker run -d mongo (Run the image in a container with detached mode, not in the same terminal)
- docker run -p 27018:27017 -d mongo  (Attaching a port to your container)
- docker kill :containerID (how to shut down an container)
- docker rmi :image --force (to delete the image from your machine)
- docker build -t backend-app . (-t :name helps you give a name to your image, '.' is for the current location)
- docker exec  (to execute an command inside the container)
- docker exec <container_name_or_id> ls /path/to/directory (list all files in the container)
- docker exec -it <container_name_or_id> /bin/bash  (interact with the container)
- docker volume create volume_database
- docker run -v volume_database:/data/db -p 27017:27017 mongo
- docker volume ls
- docker logs :containerId 









# **References**

[[Docker]]