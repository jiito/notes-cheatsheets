# System Administration Notes

## Installing Packages

### Fix dependencies

#### using --fix-missing

```bash
apt-get install -y --fix-missing libfuse-dev
```

### find package version

```bash
apt-cache policy <package name>
```

### install specific version

```bash
sudo apt-get install <package name>=<version>
```

## LDAP

### Connecting via CL 

#### Install packages

```bash
sudo yum install openldap-clients
```


