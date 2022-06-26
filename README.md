```sh
(
name=haskell
curl -o preseed.cfg https://www.debian.org/releases/bullseye/example-preseed.txt
cat <<EOF >> preseed.cfg
d-i grub-installer/bootdev string default
d-i netcfg/get_hostname string debian11-$name
d-i passwd/root-login boolean false
d-i passwd/user-fullname string whs
d-i passwd/user-password password magic
d-i passwd/user-password-again password magic
d-i passwd/username string whs
d-i preseed/late_command string apt-install openssh-server
popularity-contest popularity-contest/participate boolean false
tasksel tasksel/first multiselect standard
EOF
virt-install \
  --disk size=20 \
  --initrd-inject preseed.cfg \
  --location https://deb.debian.org/debian/dists/bullseye/main/installer-amd64/ \
  --memory 2048 \
  --name debian11-$name \
  --network bridge:virbr0 \
  --os-variant debian11 \
  --vcpus 2 \
  ;
)
```

```sh
sudo apt-get install -y \
  build-essential \
  curl \
  libffi-dev \
  libffi7 \
  libgmp-dev \
  libgmp10 \
  libncurses-dev \
  libncurses5 \
  libtinfo5 \
  ;
```

```sh
curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | sh
```

```sh
source /home/whs/.ghcup/env
```
