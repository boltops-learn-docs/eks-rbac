<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/eks-rbac/blob/master/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# EKS RBAC Examples and An Approach

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This repo contains RBAC examples. It shows one approach and strategy to managing permissions. Every company's needs are different. It's also dependent on the cluster and environment setup.

## Users

User | Description
---|---
test-admin | Full access to all resources.
test-read-all | Read access to all resources.
test-app1-dev-read | Read access to app1 dev.
test-app2-dev-write | Write access to app2 dev.
test-app2-owner | Read access to all resources and full access to app2 for prod and dev.

## Apps/Deployments

Deployment | Namespace
---|---
web | app1-dev
web | app1-prod
web | app2-dev
web | app2-prod

## Misc: Useful Commands

Create Roles:

    for i in $(ls | egrep '(app|read-all)') ; do echo $i ; cd $i ; kubectl apply -f . ; cd - ; done

View Roles:

    kubectl get rolebinding,clusterrolebinding --all-namespaces
    kubectl get rolebinding,clusterrolebinding --all-namespaces | egrep -v '(system|eks)'

Test Write Change:

    kubectl set image deploy web web=nginx
    kubectl set image deploy web web=httpd

Can I test commands:

    kubectl auth can-i '*' '*'
    kubectl auth can-i get pods --all-namespaces
    kubectl auth can-i create pods --all-namespaces

## Video

[![Watch the video](https://uploads-learn.boltops.com/ryjfu8f98s6y0z31mo8d0q89fdgb)](https://learn.boltops.com/courses/aws-eks/lessons/eks-rbac-an-approach-and-strategy-with-examples)

Note: Premium video content requires a subscription.
