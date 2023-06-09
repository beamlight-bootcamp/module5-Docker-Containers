# Entering a container at runtime

When we enter a Docker container at runtime, it means we are accessing the container's environment interactively, allowing us to execute commands and interact with the container's file system and processes.

To enter a Docker container, we can use the `docker exec` command followed by the container ID or name, and optionally specify a command to execute within the container.

Here's an example of entering a running container:

```
docker exec -it <container-name> /bin/bash
```

In this example, the `-it` flags are used to allocate a pseudo-TTY and keep the session interactive. `/bin/bash` specifies the command to be executed within the container, in this case, launching an interactive Bash shell.

After running this command, we will be inside the container, and we can run commands as if we were on a regular command line. We can navigate the container's file system, install software, view logs, modify configurations, and perform other operations just as we would on a physical or virtual machine.

Entering a container at runtime provides a way to troubleshoot, debug, and manage running containers. It allows us to directly interact with the containerized application, inspect its internal state, and perform any necessary tasks within the container's environment.

```
Mohammads-MacBook-Air:~ mohammadashadali$ docker run -it --name apache httpd /bin/bash
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
f03b40093957: Already exists 
abaf8619eb1c: Pull complete 
e3fe37d0c2ad: Pull complete 
52a1e37affe5: Pull complete 
49d8a68fd903: Pull complete 
Digest: sha256:1bb3f7669a85713906e695599d29c58ab40d4e6409907946609d92a428e95b49
Status: Downloaded newer image for httpd:latest
root@65e95f389ed0:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs	modules
root@65e95f389ed0:/usr/local/apache2# pwd
/usr/local/apache2
root@65e95f389ed0:/usr/local/apache2# exit
exit
Mohammads-MacBook-Air:~ mohammadashadali$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
# Entering a running container in detatched mode

Sample Output:

```
Mohammads-MacBook-Air:~ mohammadashadali$ docker run -dit --name apache2 httpd /bin/bash
c627a4140adfdd2fee9156a71c94edd5c0ceadcc7989b5f1b4fe401b2fc40f0f
Mohammads-MacBook-Air:~ mohammadashadali$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
c627a4140adf        httpd               "/bin/bash"         10 seconds ago      Up 9 seconds        80/tcp              apache2
Mohammads-MacBook-Air:~ mohammadashadali$ docker exec -it apache2 /bin/bash
root@c627a4140adf:/usr/local/apache2# ls
bin  build  cgi-bin  conf  error  htdocs  icons  include  logs	modules
root@c627a4140adf:/usr/local/apache2# exit
exit
Mohammads-MacBook-Air:~ mohammadashadali$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED              STATUS              PORTS               NAMES
c627a4140adf        httpd               "/bin/bash"         About a minute ago   Up About a minute   80/tcp              apache2
```

# Docker Logging

The `docker logs` command allows us to view the logs generated by a running Docker container. It provides a convenient way to inspect the output and monitor the behavior of a containerized application.

Here's the basic syntax of the `docker logs` command:

```
docker logs [OPTIONS] <container-id>
```

Let's explore some commonly used options:

- `-f, --follow`: By using this option, you can continuously stream the container's logs in real-time, similar to the `tail -f` command. It allows you to monitor the live output of the container.

- `--tail=<number>`: This option specifies the number of lines from the end of the log to display. For example, `--tail=10` will show the last 10 lines of the log.

- `--since=<timestamp>`: You can use this option to display logs since a specific timestamp. For instance, `--since="2023-05-30T12:00:00"` will show logs generated since May 30, 2023, at 12:00:00.

- `--until=<timestamp>`: This option allows you to display logs until a specific timestamp. For example, `--until="2023-05-31T12:00:00"` will show logs generated up until May 31, 2023, at 12:00:00.

- `--timestamps`: By including this option, the log output will include timestamps for each log entry, indicating when the log was generated.

Here are a few examples demonstrating the usage of `docker logs`:

1. View the logs of a running container:
   ```
   docker logs <container-id>
   ```

2. Stream the live logs of a running container:
   ```
   docker logs -f <container-id>
   ```

3. Display the last 20 lines of the container's logs:
   ```
   docker logs --tail=20 <container-id>
   ```

4. Show logs generated since a specific timestamp:
   ```
   docker logs --since="2023-05-30T12:00:00" <container-id>
   ```

The `docker logs` command provides an easy way to access and analyze the logs produced by our Docker containers, allowing us to troubleshoot issues, monitor application output, and gain insights into the container's behavior.
