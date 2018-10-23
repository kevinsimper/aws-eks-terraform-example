# How to AWS EKS and Terraform

Examples is loaned from https://github.com/terraform-providers/terraform-provider-aws/tree/master/examples/eks-getting-started

Have downloaded aws-iam-authenticator, kubectl and terraform installed and in PATH.

```
aws-iam-authenticator -v
kubectl -v
terraform -v
```

## Have credentials

You can use AWS_PROFILE or define the environment variables like this:

```
aws configure
```

or add them manually in `~/.aws/credentials` and remember to set region in `~/.aws/config`.

## Terraform

Now you can run

```
terraform init
```

and it will download the `http` and `aws` terraform modules.

Then you can run

```
terraform apply
```

and now will your cluster be created.

It will take 25 minutes.

If it fails you can run `terraform apply` again to continue where it stopped.

# Finished setup

Now we need to connect the nodes to the control plane.

You can run this to get the config file, save it as `config_aws_auth.yaml`:

```
$ terraform output config_map_aws_auth
```

then you can connect to the cluster:

```
$ aws eks update-kubeconfig --name terraform-eks-demo
```

and then apply the config

```
$ kubectl apply -f config_aws_auth.yaml
```

and then watch the nodes join the cluster

```
$ kubectl get nodes --watch
```
