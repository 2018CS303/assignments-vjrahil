# Docker Case Study -


## Automate Infra allocation for Learning and Development

-   Dynamic Allocation of Linux systems for users
-   Each user should have independent Linux System
-   Specific training environment should be created in Container
-   User should not allow to access other containers/images
-   User should not allow to access docker command
-   Monitor participants containers
-   Debug/live demo for the participants if they have any doubts/bug in running applications.
-   Automate container creation and deletion.
# Setup Linux containers for users
1.  Allocation of a Linux based system can be achieved through a shell script  `create_user_container.sh`. Such a script would create a docker container for each user based on a docker image.

-   `users.txt`
 ```
-Rahil
-Gautami
-Tanmay
```

1.  -   `createContainers.sh`
        
        echo -n "Enter name of file with usernames: "
        read file
        while read user
            do
                docker create -it --name $user <Docker Image> /bin/bash
            done < $file
        
        where  `<Docker Image>`  is whichever image you want to run.
        
2.  Fill the entries in  `users.txt`  with usernames and run the shell script  `createContainers.sh`. This creates a docker container corresponding to each username from  `users.txt`.
    
3.  The user can then start using the allocated container by running the  `useContainers.sh`  script.
    
    -   `useContainers.sh`
        
        echo -n "Enter your username: "
        read name
        docker start $name
        docker attach $name

# Monitor the containers

To monitor the activities of a particular user use the shell script  `monitor_container.sh`

-   `monitor_container.sh`

#! /bin/bash
echo -n "Enter the container name which has to ne monitored : "
read name
docker logs -f $name
And this will produce a flow chart:
# Deleting the containers

Automate the task of deletion of containers through the shell script  `delete_container.sh`

-   `delete_container.sh`

echo -n "Enter the user list file : "
read file

while read user
  do
    docker stop $user
    docker rm $user
  done < $file

** Note ** : To execute the shell script, use the following command

  sh <shell_script>
