# Running AWS Glue ETL locally

### 1. Pre-requisites

- docker

### 2. Config files

- src/config/spark/spark-defaults.conf - Glue jars were added to classpath
- src/config/spark/pom.xml - This is not really required. It was added just in case you want to read/write Avro format via Spark not via Glue libs
- src/config/aws/config - AWS Region and Response Format Settings
- src/config/aws/credentials - AWS Connection Credentials

### 3. Code Clone

```
git clone https://github.com/FoFxjc/glue-docker-compose.git
```

### 4. Change AWS Info

1. src/config/aws/config

```
[default]
region = ap-northeast-1
output = json
```

2. src/config/aws/credentials

```
[default]
aws_access_key_id = <your-access-key-id>
aws_secret_access_key = <your-secret-access-key>
```
### 5. Build

```
docker build -t glue_local -f glue.dockerfile .
```

### 6. Create Local Jupyter Folder --optional

```
mkdir jupyter_working_dir
```

### 7. Launch container

**${PWD}/jupyter_working_dir** - host machine jupyter notebook working dir under current folder

```
docker run -d -p 8888:8888 -p 4040:4040 -v ${PWD}/jupyter_working_dir:/root/jupyter_working_dir -v ${PWD}/aws:/root/.aws --name glue_jupyter glue_local
```

### 8. Open Jupyter Notebook in host Brower

```
http://localhost:8888/
```

### 9. Stop and Remove the Container --optional

```
docker stop glue_jupyter && docker rm glue_jupyter
```
