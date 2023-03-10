# Hands-On Lab

From: https://github.com/AdminTurnedDevOps/PearsonCourses/blob/main/Helm-Charts-For-Kubernetes/Segment3/lab.md

## Create the Helm Chart
1. `helm create nginxupdate`

Test the Helm Chart
2. `helm install nginx nginxupdate --dry-run --debug`

## Upgrade The Helm Chart

1. View the Chart
`helm list -a`

2. Deploy the Helm Chart
`helm install nginx nginxupdate`

3. Run `kubectl get deployments` to see the current `replicaSet`

4. Within the `values.yaml`, change the replica count from `1` to `3`

5. Run the upgrade command
`helm upgrade nginx nginxupdate/`

6. Run `kubectl get deployments` to see that the `replicaSet` changed.

## View Helm Chart History

1. `helm history nginxapp`
2. Make a change to the `values.yaml`, for example, change the `replicacount` from `1` to `2`
3. `helm upgrade nginxapp .`

## Test The Helm Chart

1. `helm test nginxapp`

## Rollback The Helm Chart

1. Retrieve the history of the Helm Chart
`helm history nginx`

2. Take note of the revision number that you want to roll back to

3. Run the rollback command to the revision you wish to roll back to
`helm rollback nginx 2`

## Delete The Helm Chart
1. Run the following command
`helm uninstall nginx`
