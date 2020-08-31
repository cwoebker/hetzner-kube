我是光年实验室高级招聘经理。
我在github上访问了你的开源项目，你的代码超赞。你最近有没有在看工作机会，我们在招软件开发工程师，拉钩和BOSS等招聘网站也发布了相关岗位，有公司和职位的详细信息。
我们公司在杭州，业务主要做流量增长，是很多大型互联网公司的流量顾问。公司弹性工作制，福利齐全，发展潜力大，良好的办公环境和学习氛围。
公司官网是http://www.gnlab.com,公司地址是杭州市西湖区古墩路紫金广场B座，若你感兴趣，欢迎与我联系，
电话是0571-88839161，手机号：18668131388，微信号：echo 'bGhsaGxoMTEyNAo='|base64 -D ,静待佳音。如有打扰，还请见谅，祝生活愉快工作顺利。


[![Build Status](https://travis-ci.org/xetys/hetzner-kube.svg?branch=master)](https://travis-ci.org/xetys/hetzner-kube)
[![Go Report Card](https://goreportcard.com/badge/github.com/xetys/hetzner-kube)](https://goreportcard.com/report/github.com/xetys/hetzner-kube)
[![Maintainability](https://api.codeclimate.com/v1/badges/3ef5b31a84811e3b8b02/maintainability)](https://codeclimate.com/github/xetys/hetzner-kube/maintainability)
[![Gitter chat](https://badges.gitter.im/hetzner-kube.png)](https://gitter.im/hetzner-kube)

# hetzner-kube: fast and easy setup of kubernetes clusters on Hetzner Cloud

This project contains a CLI tool to easily provision [kubernetes](https://kubernetes.io) clusters
on [Hetzner Cloud](https://hetzner.com/cloud).

This is my very first tool written in Go.

## How to install

### Binary releases

Get the binary from [releases page](https://github.com/xetys/hetzner-kube/releases)

### From source

`hetzner-kube` is written in [Go](https://golang.org/). To install Go please follow the instructions on its homepage.

To get and build `hetzner-kube` from source run this command:

```
$ go get -u github.com/xetys/hetzner-kube
```

The project source will now be in your `$GOPATH` directory (`$GOPATH/src/github.com/xetys/hetzner-kube`) and the binary will be in `$GOPATH/bin`.

If you want to build it yourself later, you can change into the source directory and run `go build` or `go install`.

### Code completion

#### BASH

To load completion run

```bash
source <(hetzner-kube completion bash)
```

To configure your bash shell to load completions for each session add to your "~/.bashrc" file

```bash
# ~/.bashrc or ~/.profile
echo 'source <(hetzner-kube completion bash)\n' >> ~/.bashrc
```

Or you can add it to your `bash_completition.d` folder:

```bash
# On linux
hetzner-kube completion bash > /etc/bash_completion.d/hetzner-kube
# On OSX with completion installed via brew (`brew install bash-completion`)
hetzner-kube completion bash > /usr/local/etc/bash_completion.d/hetzner-kube
```

#### ZSH

To configure your zsh shell to load completions run following commands:

```bash
# On linux
hetzner-kube completion zsh | sudo tee /usr/share/zsh/vendor-completions/_hetzner-kube
# On OSX
hetzner-kube completion zsh | sudo tee /usr/share/zsh/site-functions/_hetzner-kube
```

Than rebuild autocomplete function with:

```
compinits
```

## Usage

In your [Hetzner Console](https://console.hetzner.cloud) generate an API token and

```bash
$ hetzner-kube context add my-project
Token: <PASTE-TOKEN-HERE>
```

Then you need to add an SSH key:

```bash
$ hetzner-kube ssh-key add -n my-key
```

This assumes, you already have a SSH keypair `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`

And finally, you can create a cluster by running:

```bash
$ hetzner-kube cluster create --name my-cluster --ssh-key my-key
```

This will provision a brand new kubernetes cluster in latest version!

For a full list of options that can be passed to the ```cluster create``` command, see the [Cluster Create Guide](docs/cluster-create.md) for more information.

## HA-clusters

You can build high available clusters with hetzner-kube. Read the [High availability Guide](docs/high-availability.md) for
further information.

# Custom Options

## addons

You can install some addons to your cluster using the `cluster addon` sub-command. Get a list of addons using:

```bash
$ hetzner-kube cluster addon list
```

### contributing new addons

You want to add some cool stuff to hetzner-kube? It's quite easy! Learn how to add new addons in the [Developing Addons](docs/cluster-addons.md) documentation.

## cloud-init

If you like to run some scripts or install some additional packages while provisioning new servers, you can use cloud-init
```
$ hetzner-kube cluster create --name my-cluster --nodes 3 --ssh-key my-key --cloud-init <PATH-TO-FILE>
```
An example file to make all nodes ansible ready. The comment on the first line is important:

```yaml
#cloud-config
package_update: true
packages:
 - python
```

## Full tutorial

[This article](http://stytex.de/blog/2018/01/29/deploy-kubernetes-hetzner-cloud-openebs/) guides through a full cluster setup.
