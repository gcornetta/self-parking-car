## How to configure Raspberry Pi for P2P connnection

Log into the Raspberry Pi, then go to `/etc/network`folder:

```
$ cd /etc/network`
```
Edit the `interfaces` file; however, for safety, save a backup copy:

```
$ sudo cp interfaces interfaces.backup
```

```
$ sudo apt-get install \
  apt-transport-https \
  ca-certificates \
  curl \
  gnupg2 \
  software-properties-common
```

3. Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```
4. Use the following command to set up the **stable** repository. To install the package for `armv7` (32-bit architecture) you can use the following command:
```
$ sudo add-apt-repository \
   "deb [arch=armhf] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```
If you run into trouble with the previous command try the following steps:

* First set up the new repository in a `docker.list` file like so:
```
$ echo "deb [arch=armhf] https://download.docker.com/linux/raspbian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list
```
* Then update the repository by running:
```
$ sudo apt-get update
```
* If you experience issues with the latest version, you can check the available versions by running:

```
$ apt-cache madison docker-ce
```

* Then install the version you want (for example `18.0.6`) by running the following command:

```
$ sudo apt-get install docker-ce=18.06.2~ce~3-0~raspbian containerd.io
```

Otherwise, for `armv8`(64-bit architecture) you can use the following:
```
$ sudo add-apt-repository \
   "deb [arch=arm64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
```
5. Update the `apt` package index:
```
$ sudo apt-get update
```
6. Install the latest version of **Docker CE** and **containerd**: 
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```
To install a specific version of **Docker CE**, list the available versions in the repo, then select and install:

1. First list the versions available in your repo:
```
$ apt-cache madison docker-ce

  docker-ce | 5:18.09.1~3-0~debian-stretch | https://download.docker.com/linux/debian stretch/stable amd64 Packages
  docker-ce | 5:18.09.0~3-0~debian-stretch | https://download.docker.com/linux/debian stretch/stable amd64 Packages
  docker-ce | 18.06.1~ce~3-0~debian        | https://download.docker.com/linux/debian stretch/stable amd64 Packages
  docker-ce | 18.06.0~ce~3-0~debian        | https://download.docker.com/linux/debian stretch/stable amd64 Packages
  ...
```
2. Then install a specific version using the version string from the second column, for example, `5:18.09.1~3-0~debian-stretch`:
```
$ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io
```
### Installation with convenience script
Docker offers also the possibility to install **Docker engine** using a convenience script
```
curl -sSL https://get.docker.com | sh
```
You need `root` or `sudo` provoleges to run this script. Also, note that the script could be outdated and your architecture could be not supported.

### Executing docker as a non-root user
If you would like to use Docker as a non-root user, you should now consider adding your user (for example `pi` the default user on a Raspberry pi) to the “docker” group with something like:
```
sudo usermod -aG docker pi
```

Remember to log out and back in for this to take effect.

## Uninstalling Docker CE
To uninstall the **Docker CE** package type:
```
$ sudo apt-get purge docker-ce
```

Observe that images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes type:

```
$ sudo rm -rf /var/lib/docker
