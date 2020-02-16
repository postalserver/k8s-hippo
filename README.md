# Postal

This repository contains the configuration required to deploy Postal to a Kubernetes Cluster using [Hippo](https://adam.ac/hippo).

## Prerequisites

Before you can get started, make sure you have the `hippo-cli` gem installed.

```
$ gem install hippo-cli
```

You should also ensure that you have `kubectl` and `helm` installed and are configured correctly.

## Installing

You need to decide on a location to store any configuration for your Postal instance. This is a local directory on your computer that you may check into version control. It maintains the state for multiple instances of Postal across multiple clusters.

Begin by using `hippo setup` to create your configuration directory. Once created, you'll have a directory containing `hippo.yaml` file with details of where to find the manifest for deploying Postal.

```bash
$ hippo setup path/to/config --remote https://github.com/postalhq/k8s-hippo
```

Once setup, you should enter your new config directory and create a new "stage". In this example, we'll call it `production`.

```bash
$ cd path/to/config
$ hippo production create
```

Follow the instructions to choose the name of the namespace and the `kubectl` context name to use when deploying.

Running this will create a directory with the same name as the stage in your config directory. You can now add any configuration which may be needed. You should look in `production/config.yaml` first and add necessary data. You can then look at adding any required secrets.

```bash
$ hippo production secrets
```

Once you have added this, you can go ahead and install any dependent packages.

```bash
$ hippo production prepare
```

Now, just wait for these packages to be fully installed. You can monitor progress using `hippo production status`. You should wait until all new services & pods are fully ready before continuing.

When ready, you can go ahead and install the application for the first time.

```bash
$ hippo production install
```

This will then push all configuration and deployments needed. If the deployments are successful, services will also be applied. Monitor the status as needed and review logs if things aren't going to plan.

```bash
$ hippo production status
$ hippo production logs
```

## Next steps

Once running, you can make your first user using the console:

```bash
$ hippo production console -c 'bin/postal make-user'
```

* Review the `hippo production status` output to find the IP allocated for your incoming SMTP.
* Ensure certificates have been issued and the web interface is available on the hostname you have entered.
* Configure any required DNS as appropriate.

