---
template: blog-post
title: The Data Engineer Toolbox on MacBook Air
slug: the-data-engineer-toolbox-on-macbook-air
date: 2021-09-30 15:46
description: The Data Engineer Toolbox on Macbook Air M1
featuredImage: /assets/featured-toolbox-data-engineer-1500x800.jpeg
---
Macbook Air M1 is a game changer considering not only the power of ARM CPU but also its autonomy up to 15+ hours.

Those performances came with some constraints as a developper when installing required tools and preparing the environment since the installation of some of them is not straightforward for tools not yet ARM ready

I’m sharing the toolbox that every data engineer need to install on Macbook Air M1 2020.

This toolbox includes:

* Homebrew
* Rosetta 2
* Python 3
* Git
* Google Cloud SDK
* Docker
* Airflow
* Terraform

Which is not an exclusive list anyway, but can saves you time and the setup could be finished in 20 minutes.

# Homebrew

Homebrew is a MacOS package manager you definitely need to install required stuff that aren’t installed by default

When it came to M1 chip, this is not straightforward. homebrew need to be installed on top of rosetta 2 which is an abstraction & emulation layer to run x86_64 instruction on ARM based CPU.

### Step#1: Rosetta 2 installation

```
softwareupdate --install-rosetta
```

### Step#2: Homebrew installation

```
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

### Step#3: Update packages

```
arch -x86_64 brew update
```

### Step#4: Run Terminal with Rosetta 2

you need to activate the option in:

Application —>Utilities —> Terminal —> Get info —>tick the option as shown below



![](https://mrekaya.com/wp-content/uploads/2021/02/terminal-macbookpro-130x300.png)

### Step#5: Run install

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

# Python 3

For Python we are going to install the native version via brew:

```
/opt/homebrew/bin/brew install python
```

Version 3.9.1 will be installed which is native to ARM arch compatible with M1



![](https://mrekaya.com/wp-content/uploads/2021/02/python39-1024x321.png)

# Git

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency

The installation is straightforward using Homebrew

```
brew install git
```

And That’s it

# Google Cloud SDK

### Step#1:

```
curl <https://sdk.cloud.google.com> > install.sh
chmod +x install.sh
arch -x86_64 install.sh --disable-prompts
```

### Step#2: Optional

Add Cloud SDK tools to your path:

```
 ./google-cloud-sdk/install.sh
```

### Step#3:

Restart your shell:

```
exec -l $SHELL
```

### Step#4:

Run gcloud init to initialize the gcloud environment:

```
gcloud init
```

# Docker desktop

Docker desktop for Apple M1 still in preview and can be downloaded [here](https://www.notion.so/Setup-MacBook-M1-7241924a04ce40f494185928ef0bc0c5) with the limitations below. the full details are [here](https://www.notion.so/Setup-MacBook-M1-7241924a04ce40f494185928ef0bc0c5).

* The tech preview build does not update automatically. You must manually install any future versions of Docker Desktop.
* You must install Rosetta 2 as some binaries are still Darwin/AMD64.
* The DNS name `host.docker.internal` only works if you add `-add-host=host.docker.internal:host-gateway` to the `docker run` command
* The DNS name `vm.docker.internal` does not work.
* Kubernetes does not initialize because of a missing DNS name.
* osxfs file sharing does not work.
* The HTTP proxy is not enabled.
* Not all images are available for ARM64. You can add `-platform linux/amd64` to run an Intel image under emulation. In particular, the [mysql](https://hub.docker.com/_/mysql?tab=tags&page=1&ordering=last_updated) image is not available for ARM64. You can work around this issue by using a [mariadb](https://hub.docker.com/_/mariadb?tab=tags&page=1&ordering=last_updated) image.
* The kernel may panic. If so, look in `~/Library/Containers/com.docker.docker/Data/vms/0/console.log` for a BUG or kernel panic to report.
* The **Restart** option in the Docker menu may not work.

# Apache Airflow

[Airflow](https://airflow.apache.org/docs/apache-airflow/stable/index.html) is a platform to programmatically author, schedule and monitor workflows. a must have for a data engineer

We will use a dockerized version of apache airflow.

The following [image](https://github.com/puckel/docker-airflow) will be used. Already have 3k+ stars on github. we are going to clone the repo and run airflow with CeleryExecutor

### Step#1:

```
git clone https://github.com/puckel/docker-airflow.git
```

### Step#2

Pull & Run Airflow with CeleryExecutor

```
docker-compose -f docker-compose-CeleryExecutor.yml up -d
```

# Terraform

Terraform is an open-source infrastructure as code tool, codifies cloud APIs into declarative configuration files.

The installation is straightforward using Homebrew

```
brew install terraform
```

The last released version will be installed by default. 0.14 at the moment when writing this post



![](https://mrekaya.com/wp-content/uploads/2021/02/terraform-1024x138.png)



[](https://mrekaya.com/the-data-engineer-toolbox-on-macbook-air/# "Facebook")[](https://mrekaya.com/the-data-engineer-toolbox-on-macbook-air/# "Twitter")