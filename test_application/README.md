# Tests

```bash

helm install --name wordpress-magico --set wordpressUsername=admin,wordpressPassword=password,mariadb.mariadbRootPassword=secretpassword,persistence.size=500Mi,persistence.storageClass=gluster-heketi stable/wordpress

```
