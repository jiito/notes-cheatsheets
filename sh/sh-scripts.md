# Shell Scripts  


### Redirecting output (silencing)

eg:
```bash
docker build -f ./packages/clone-cloud-sql/Dockerfile -t gcr.io/onx-datastore/pygis-clone-cloud-sql:latest . > /dev/null 2>&1
```

### Checking empty string 
[Article](https://www.cyberciti.biz/faq/unix-linux-bash-script-check-if-variable-is-empty/)
```bash
if [ -z "$var" ]
then
      echo "\$var is empty"
else
      echo "\$var is NOT empty"
fi
```
