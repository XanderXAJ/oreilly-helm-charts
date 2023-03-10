# Values.yaml Lab

From: https://github.com/AdminTurnedDevOps/PearsonCourses/blob/main/Helm-Charts-For-Kubernetes/Segment4/lab.md

`nginxvalues` chart copied from: https://github.com/AdminTurnedDevOps/PearsonCourses/tree/main/Helm-Charts-For-Kubernetes/Segment4/nginxvalues

## Create Namespaces
```
kubectl create namespace dev
kubectl create namespace staging
kubectl create namespace prod
```

## Charge Directory
`cd Segment4`

## Install For Dev
`helm install nginxdev nginxvalues -n dev -f nginxvalues/values/dev/values.yaml`
`kubectl get pods -n dev`

## Install For Staging
`helm install nginxstaging nginxvalues -n staging -f nginxvalues/values/staging/values.yaml`
`kubectl get pods -n staging`

## Install For Prod
`helm install nginxprod nginxvalues -n prod -f nginxvalues/values/prod/values.yaml`
`kubectl get pods -n prod`

## Cleanup
`helm uninstall nginxdev -n dev`
`helm uninstall nginxstaging -n staging`
`helm uninstall nginxprod -n prod`

# Running Configs With Values.yaml

1. Create three files:
`values-dev.yaml`
`values-staging.yaml`
`values-prod.yaml`

Once created, popular the Value files with your choice of values

2. Create namespaces
```
kubectl create namespace dev
kubectl create namespace staging
kubectl create namespace prod
```

3. Create the Helm Charts
```
helm install nginxdev nginxvalues -n dev -f values-dev.yaml
helm install nginxstaging nginxvalues -n staging -f values-staging.yaml
helm install nginxprod nginxvalues -n prod -f values-prod.yaml
```


4. Cleanup
```
helm uninstall nginxdev -n dev
helm uninstall nginxstaging -n staging
helm uninstall nginxprod -n prod
```

# Helm Chart Pipelines/Go Templates

The purpose of this lab is to use some of the functions that you learned about in this section to create a Helm Chart and update values of the Helm Chart with pipeline values

1. Create a Helm Chart
`helm create nginxpipelines`

2. Open up the Helm Chart and go to templates --> `deployment.yaml`

3. Replace line 6 of the `deployment.yaml` with the following:
`{{- include "nginxpipelines.labels" . | nindent 4 | lower }}`

This code ensures that the labels are all lower case, per the `lower` pipeline because per best practices and standards, lowercase RFC 1123 subdomain must consist of lower case alphanumeric characters, so you want to ensure that your labels are lowercase.

4. Run the following to install the Helm Chart
`helm install nginxupdate .`

5. Clean up
`helm uninstall nginxupdate`

## Conditionals

1. View the `conditionals` directory
