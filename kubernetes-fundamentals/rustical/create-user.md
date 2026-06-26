# Create User

First identify pod.

```sh
kubectl -n calendar get pods
NAME                        READY   STATUS    RESTARTS   AGE
rustical-5bb8d88c88-t2t7m   1/1     Running   0          81m
```

Than create the user account with the password.

```sh
kubectl -n calendar exec -it rustical-5bb8d88c88-t2t7m -- rustical principals create cjjackson -p individual --password
```

Input the password, there is no confirm.

You should be able to login via frontend, it only work via https or localhost
