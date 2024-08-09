# Provider Template

`upjet-provider-template` is a [Crossplane](https://crossplane.io/) provider that
is built using [Upjet](https://github.com/crossplane/upjet) code
generation tools and exposes XRM-conformant managed resources for the
Template API.

## Getting Started

Install the provider by using the following command after changing the image tag
to the [latest release](https://marketplace.upbound.io/providers/upbound/upjet-provider-template):
```
up ctp provider install upbound/upjet-provider-template:v0.1.0
```

Alternatively, you can use declarative installation:
```
cat <<EOF | kubectl apply -f -
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: upjet-provider-template
spec:
  package: upbound/upjet-provider-template:v0.1.0
EOF
```

Notice that in this example Provider resource is referencing ControllerConfig with debug enabled.

You can see the API reference [here](https://doc.crds.dev/github.com/upbound/upjet-provider-template).

## Developing

Run code-generation pipeline:
```console
go run cmd/generator/main.go "$PWD"
```

Run against a Kubernetes cluster:

```console
make run
```

Build, push, and install:

```console
make all
```

Build binary:

```console
make build
```












# Crossplane Akash Provider

This Crossplane provider enables you to manage and reconcile Akash Network resources, such as deployments, directly from your Kubernetes cluster using Crossplane.

## Features

- **Manage Akash Deployments**: Automate the creation, update, and deletion of Akash deployments.
- **Network Resource Reconciliation**: Seamlessly integrate Akash network resources into your Kubernetes environment.
- **Crossplane Integration**: Leverage Crossplane’s powerful composition and reconciliation features to manage your Akash resources declaratively.

## Getting Started

### Prerequisites

- [Crossplane](https://crossplane.io) installed in your Kubernetes cluster.
- Akash CLI configured and accessible from the Kubernetes nodes.


## Install

To install the Akash provider without modifications, use the Crossplane CLI in a Kubernetes cluster where Crossplane is installed:

```console
crossplane xpkg install provider xpkg.upbound.io/web7/provider-akash:v0.1.0
```

You can also manually install the Akash provider by creating a Provider directly:

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: provider-akash
spec:
  package: xpkg.upbound.io/web7/provider-akash:v0.1.0
```


## Configure the Provider

   Create a ProviderConfig to configure the Akash provider and apply it:


```console
kubectl apply -f - <<EOF
   apiVersion: akash.web7.md/v1alpha1
   kind: ProviderConfig
   metadata:
     name: akash-provider
   spec:
     keyName: "my-key"
     keyringBackend: "test"
     accountAddress: "akash1..."
     net: "mainnet"
     version: "v0.15.0"
     chainId: "akashnet-2"
     node: "https://rpc.akash.forbole.com"
     home: "/root/.akash"
     path: "akash"
     providersApi: "https://akashapi.test.net"
     EOF
```

## Usage

Once installed and configured, the Crossplane Akash provider will reconcile Akash network resources based on your Kubernetes manifests.

- **Create**: New resources will be created on the Akash network.
- **Update**: Any changes in the manifest will be reflected on the Akash deployment.
- **Delete**: Deleting the Kubernetes resource will clean up the corresponding Akash resource.

## Examples

Check out the `examples/` directory for more sample configurations and usage scenarios.

## Troubleshooting

- **Logs**: Check the Crossplane provider logs for any errors during reconciliation.
- **Akash CLI**: Verify the state of your deployments using the Akash CLI.


## License

This project is licensed under the [Apache 2.0 License](LICENSE).







## Report a Bug

For filing bugs, suggesting improvements, or requesting new features, please
open an [issue](https://github.com/upbound/upjet-provider-template/issues).
