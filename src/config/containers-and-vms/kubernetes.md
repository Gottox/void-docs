# Kubernetes

Kubernetes, also known as K8s, is a flexible and scalable container
orchestration system. The recommended way to use Kubernetes on Void is through
the [k0s](https://k0sproject.io/) distribution which manages most of the 
complexity and allows both, single node and large cluster setups.

To setup a kubernetes cluster, install the `k0s` package is installed. Once that is done
continue with the desired setup section.

# Master Node Setup

1. [Enable](../services/index.md#enabling-services) the `k0s` service

2. Once the `k0s` service is up and running create a new worker token:
   `k0s -c /etc/k0s/k0s.conf token create --role=worker > /etc/k0s/worker.token`

3. [Enable](../services/index.md#enabling-services) the `k0s-worker` service.

4. copy the kubeconfig into you local `.kube` directory:
   `cp /var/lib/k0s/pki/admin.conf > ~/.kube/config`

5. Test if the cluster is correctly running: `kubectl get nodes`.
   It may take a few minutes until the nodes gets ready.

# Troubleshooting

* Void doesn't ship [kine](https://github.com/k3s-io/kine) at the moment. So
  currently the only supported storage backend for kubernetes is `etcd`.

* Due to permission restrictions Void introduced you cannot run a `k0s server`
  with the `--enable-worker` enabled. Please use the `k0s-worker` server in
	conjunction with the `k0s` service instead.

# Further Reading

For further information consult the official [k0s documentation](https://docs.k0sproject.io/)
