![](https://img.shields.io/badge/Arista-CVP%20Automation-blue)  ![](https://img.shields.io/badge/Arista-EOS%20Automation-blue) ![GitHub](https://img.shields.io/github/license/arista-netdevops-community/docker-avd-base) ![Docker Pulls](https://img.shields.io/docker/pulls/avdteam/base) ![Docker Image Size (tag)](https://img.shields.io/docker/image-size/avdteam/base/latest) ![Docker Image Version (tag latest semver)](https://img.shields.io/docker/v/avdteam/base/latest)
# AVD Base Image


Image with all python requirements installed to then run [__Arista Validated Design__](https://github.com/aristanetworks/ansible-avd) collection with a minimal configuration overhead. It can be used to support local development using following workflow

__Docker image:__ [`avdteam/base`](https://hub.docker.com/repository/docker/avdteam/base)

## Description

### Available Tags

- [`3.6`](3.6/Dockerfile)
- [`3.7`](3.7/Dockerfile)
- [`3.8`](3.8/Dockerfile) / (latest)
- [`centos-7`](centos-7/Dockerfile) (deprecated)
- [`centos-8`](centos-8/Dockerfile) (deprecated)

### Available variables

These variables are used in `CMD` to customize container content using [`-e` option of docker](https://docs.docker.com/engine/reference/commandline/run/#set-environment-variables--e---env---env-file) cli:

- `AVD_REQUIREMENTS`: Path to a `requirements.txt` to install during container startup.
- `AVD_ANSIBLE`: Ansible version to install in container when booting up

To see how to customize your container with this option, you can refer to [How to install ansible and Python requirements page](docs/run-options.md)

## How to leverage image

This image can be leveraged in different use-cases such as ansible or gNMI automation for Arista products.

In every scenario, you can use an isolated shell to test your automation workflow or you can start a shell with a mount point to use your local content.

### Arista Validated Design

This docker image was primarily built to support development and playbook execution of [Arista Validated Design project](https://github.com/aristanetworks/ansible-avd).

Here are some repositories leveraging [__`avdteam/base`__](https://hub.docker.com/repository/docker/avdteam/base):

- [Ansible AVD & Cloudvision example](https://github.com/arista-netdevops-community/ansible-avd-cloudvision-demo)
- [Ansible AVD & CVP TOI lab](https://github.com/arista-netdevops-community/ansible-cvp-toi)

### Generic Arista Automation Purpose

Docker image has been extended to support all Arista automation tools.

Here are some EOS automation examples leveraging [__`avdteam/base`__](https://hub.docker.com/repository/docker/avdteam/base):

- [eAPI automation example repository](https://github.com/arista-netdevops-community/arista_eos_automation_with_eAPI)
- [Ansible automation repository](https://github.com/arista-netdevops-community/arista_eos_automation_with_ansible)
- [Pyang and Pyangbind repository](https://github.com/arista-netdevops-community/gnmi_demo_with_arista_eos)
- [Netconf example](https://github.com/arista-netdevops-community/arista_eos_automation_with_ncclient)


## Run container

### Start isolated shell

```shell
$ docker run --rm -it avdteam/base:3.6
➜  /projects
```

You can also configure your shell with an alias to make it easy to start container

```shell
# Configure alias in bashrc
alias avd-shell='docker run -it --rm avdteam/base:latest zsh'

# Run alias command
$ avd-shell
➜  /projects
```

### Start shell in your project

```shell
$ docker run --rm -it -v ${PWD}:/projects avdteam/base:3.6
➜  /projects ls
Makefile  README.md  activate-arista.cvp-logs.env
```

You can also configure your shell with an alias to make it easy to start container

```shell
# Configure alias in bashrc
alias avd-shell='docker run -it --rm \
	-v ${PWD}/:/projects \
	avdteam/base:latest zsh'

# Run alias command
$ avd-shell
➜  /projects
Makefile  README.md  activate-arista.cvp-logs.env
```

### Update container image

To update container image, just run docker command:

```shell
$ docker pull avdteam/base:3.6
3.6: Pulling from avdteam/base
Digest: sha256:1602b5ab710c3a3ac9a8e93c1672c295afcd262c01b6201c0f5f83b50ff42705
Status: Image is up to date for avdteam/base:3.6
docker.io/avdteam/base:3.6
```

## Additional Resources

- [Build and Maintain avd-docker-image](docs/image-info.md)
- [Options to run avd image and make custom container](docs/run-options.md)

## License

Project is published under [Apache 2.0 License](./LICENSE)