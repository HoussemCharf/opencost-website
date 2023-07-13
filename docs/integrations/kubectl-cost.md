---
sidebar_position: 3
---

# kubectl cost

`kubectl-cost` is a [kubectl plugin](https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/) that provides easy CLI access to Kubernetes cost allocation metrics via the [OpenCost API](/api). It allows developers, devops, and others to quickly determine the cost and efficiency for any Kubernetes workload.

Installation instructions: [kubectl cost](https://github.com/kubecost/kubectl-cost):

## kubectl-cost usage

`kubectl cost` will need to be pointed at the OpenCost service. The below example assumes you followed the [installation instructions](../installation/install).

Potentially set an alias:

```sh
alias kcac='kubectl cost --service-port 9003 --service-name opencost --kubecost-namespace opencost --allocation-path /allocation/compute'
```

Find the cost of each namespace based on the last five days:

```sh
kubectl cost --service-port 9003 --service-name opencost --kubecost-namespace opencost --allocation-path /allocation/compute  \
    namespace \
    --historical \
    --window 5d \
    --show-cpu \
    --show-memory \
    --show-pv \
    --show-efficiency=false
```

Find the total projected monthly costs based on the last two hours:

```sh
kubectl cost --service-port 9003 --service-name opencost --kubecost-namespace opencost --allocation-path /allocation/compute  \
    namespace \
    --window 2h \
    --show-efficiency=true
```

Using the alias, show the total costs of all resources with the label app:
> **Note**: Unallocated represents resources not using the label

```sh
kcac label --historical -l app --window 5d
```
