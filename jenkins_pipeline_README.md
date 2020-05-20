
```
docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v $PWD/jenkins_data:/var/jenkins_home:z -t jenkins/jenkins:lts
```

If container fails, check the logs
```
$ docker logs jenkins
```

## If it is permissions error like this
```
┌─[andre@optiplex7020]─[~]
└──╼ $docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                      PORTS               NAMES
fe10b6892937        jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   54 seconds ago      Exited (1) 50 seconds ago                       jenkins-pipeline
┌─[andre@optiplex7020]─[~]
└──╼ $docker logs jenkins-pipeline
touch: cannot touch '/var/jenkins_home/copy_reference_file.log': Permission denied
Can not write to /var/jenkins_home/copy_reference_file.log. Wrong volume permissions?
```
### Change the permissions, owner and restart the jenkins container instance
```
┌─[andre@optiplex7020]─[~]
└──╼ $sudo chmod 777 jenkins_pipeline_container_data/

─[andre@optiplex7020]─[~]
└──╼ $sudo chown -R andre:andre jenkins_pipeline_container_data/


drwxrwxrwx  2 andre andre    4096 Apr 11 13:25  jenkins_pipeline_container_data

# restart and ensure container is running
┌─[andre@optiplex7020]─[~]
└──╼ $docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                     PORTS               NAMES
fe10b6892937        jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   9 minutes ago       Exited (1) 9 minutes ago                       jenkins-pipeline
┌─[andre@optiplex7020]─[~]
└──╼ $docker start fe10b6892937
fe10b6892937
┌─[andre@optiplex7020]─[~]
└──╼ $docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                              NAMES
fe10b6892937        jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   9 minutes ago       Up 3 seconds        0.0.0.0:8080->8080/tcp, 0.0.0.0:50000->50000/tcp   jenkins-pipeline
```

## Open a browser and go to http://localhost:8080
## obtain the password through the docker logs
```
$ *************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

fb5ceb48a84e460084adc238f2684a31

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************

```

