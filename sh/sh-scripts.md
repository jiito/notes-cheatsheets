# Shell Scripts  


### Redirecting output (silencing)

eg:
```bash
docker build -f ./packages/clone-cloud-sql/Dockerfile -t gcr.io/onx-datastore/pygis-clone-cloud-sql:latest . > /dev/null 2>&1
```
