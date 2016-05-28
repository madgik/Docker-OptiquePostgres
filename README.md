# Postgres with Optique data - Docker 

## Docker Installation

Install Docker (on linux) or Docker-toolbox (on Windows/Mac) 
  - [Mac](https://docs.docker.com/mac/step_one/)
  - [Windows](https://docs.docker.com/windows/step_one/)
  - [Linux](https://docs.docker.com/linux/step_one/)  

Linux only: [Use docker without sudo](http://askubuntu.com/a/477554)

## Optique Postgres Installation
1. Open a terminal (Docker Quickstart Terminal on Windows/Mac or standard terminal on Linux).
2. Download zip and unzip or “git clone” from OptiquePostgres repository


  ```bash
  $ git clone https://github.com/madgik/Docker-OptiquePostgres.git
  ```
3. Linux only:

  ```bash
  $ sudo service docker start
  ```
4. Navigate to the Stream Server Directory:

  ```bash
  $ cd <path to Docker-OptiquePostgres>
  ```
5. Build Stream Server image (this may take a few minutes the first time):

  ```bash
  $ docker build -t postgresserver .
  ```

## Run Optique Postgres container
1. Execute:
  ```bash
  $ docker run -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword -i -t --rm  --name postgresserver postgresserver
  ```
2. The "-e POSTGRES_PASSWORD=mysecretpassword" argument is optional.
3. To change the port the container listens to you need to change the first part of the "-p <chage-this>:5432" argument.
3. Leave this console open while you are working and then [stop the container](#exit-container).
4. Find your docker machine IP
  1. On Linux is: localhost
  2. On Windows/Mac open a new Docker Quickstart Terminal and run:
  ```
  $ docker-machine ip
  ```
  It will return your docker-machine ip **(from now on use this instead of localhost if you are on Windows or Mac)**.

## Functionality and Settings
- The postgres server inside the container has one database named "nw"
- The default user will be "postgres" and a password can be set but it is optional


## Test the Optique Postgres
Test the Optique Postgres using [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) 
```bash
$ psql -p 5432 -U postgres -h <dockerip>
```
## Exit Optique Postgres container
To gracefully stop your docker container:

1. Select your Optique Postgres docker console.
2. Press Ctrl+C.
3. Close the console.

## Add datasets
To load your dataset into the postgres database of the container:
1. Create a sql script file and save it in the same directory as the Dockerfile of this repository
2. Modify the Dockerfile of this repository and after the line 
```
RUN mkdir /docker-entrypoint-initdb.d
```
you must add your script file to the container 
```
ADD <name-of-your-script-file>  /docker-entrypoint-initdb.d/
```






