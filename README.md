# ansible

This is docker cluster with all the ansible requiremets. Which you can use to practice ansible. This is having 1 ansible master and 6 slave nodes.

# Run Ansible Cluster 

```
docker-compose up
```

# Once it is up, you can login to master container using 

```
docker exec -it ${MASTER_CONTAINER_ID}
```
