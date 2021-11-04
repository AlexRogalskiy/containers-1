# [nerdctl][2] multi-platform
 A sample repo to demo non-native(multi-platform) `openjdk` container images using `nerdctl`






## Install

 - Install [containerd][0] with [multi-platform][1] support
 
```bash
$ wget "https://github.com/containerd/nerdctl/releases/download/v0.13.0/nerdctl-full-0.13.0-linux-arm64.tar.gz"
$ mkdir .local  # or /usr/local
$ tar Cxzvvf ~/.local nerdctl-full-0.13.0-linux-arm64.tar.gz
$ export PATH=$PATH:~/.local/bin

# Install CNI plugins
$ sudo mkdir -p /opt/cni/bin
$ wget "https://github.com/containernetworking/plugins/releases/download/v1.0.1/cni-plugins-linux-arm64-v1.0.1.tgz"
$ sudo tar Cxzvvf /opt/cni/bin cni-plugins-linux-arm64-v1.0.1.tgz

# Enable Rootful mode
$ sudo systemctl enable --now containerd

# Install cross-platform emulators
$ sudo nerdctl run --privileged --rm tonistiigi/binfmt --install all
$ ls -1 /proc/sys/fs/binfmt_misc/qemu*

# arm64,x86_64 etc
$ sudo nerdctl run --rm --platform=s390x alpine uname -a
Linux 4e155a2bc889 5.10.61-0-virt #1-Alpine SMP Mon, 30 Aug 2021 07:41:25 UTC s390x Linux
```

 - Update [nerdctl][2] on [Rancher Desktop][3]

```bash
$ LIMA_HOME="$HOME/Library/Application Support/rancher-desktop/lima" "/Applications/Rancher Desktop.app/Contents/Resources/resources/darwin/lima/bin/limactl" shell 0
$ sudo apk add curl
$ curl -sfL https://github.com/containerd/nerdctl/releases/download/v0.13.0/nerdctl-0.13.0-linux-amd64.tar.gz | sudo tar xz -C /usr/local/bin -f -
$ nerdctl --version
```


[0]: https://github.com/containerd/containerd
[1]: https://github.com/containerd/nerdctl/blob/master/docs/multi-platform.md
[2]: https://github.com/containerd/nerdctl
[3]: https://github.com/rancher-sandbox/rancher-desktop