# Nginx Operator

This is basic operator which creates a nginx deployment. This example is a very good starting point to anyone start developing
kubernetes operators.

## Tools Version
| Tool        | Version  |
|-------------|----------|
| kubebuilder | `3.13.0` |


## Create Project

In this section we create project folder and initialize the operator project. Kubebuilder creates all the neccessary
biolderplate for us.

```shell
# Project folder
export PROJECT_PATH=~/projects/nginx-operator
mkdir -p $PROJECT_PATH && cd $PROJECT_PATH

# Init operator project
kubebuilder init --domain example.dom --repo github.com/cdivitotawela/nginx-operator

# Create API. Enter y for both create Resource and Controller
kubebuilder create api --group examples --version v1 --kind Nginx
```

## Run Project

We have not done anything yet. But we can run the project while it won't do anything.

```shell
# Start kind cluster
kind create cluster --name operators

# Generate manifests
make manifests

# Install manifests
make install

# Run operator
make run
```

## Updating Code

Update the file api/v1/nginx_types.go by adding the CRD spec
```go
type NginxSpec struct {
	Tag      string `json:"tag,omitempty"`
	Replicas int32  `json:"replicas,omitempty"`
}
```
