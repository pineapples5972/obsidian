---
{"dg-publish":true,"permalink":"/unsorted/error-journal/","tags":["#Unsorted","#solutions"],"noteIcon":""}
---

### Nix pkg unable to install or delete packages
**OS**: Arch Linux 
**Tags**: #linux #nix #packages

**Description**: Error: this derivation has bad 'meta.outputsToInstall/Uninstall' 
**References**: https://discourse.nixos.org/t/error-this-derivation-has-bad-meta-outputstoinstall/20019 

**Reproduce:**
After trying to install or uninstall a package:
`nix-env -e calibre`
or trying to upgrade a package:
`nix-env -u --always calibre`

would see this error
`Error: this derivation has bad 'meta.outputsToInstall/Uninstall`

**Solution**: 
save list of packages with `nix-env -q > cur.gen`
switch to pretty old generation like 1 month ago `nix-env --list-generations` and `nix-env --switch-generation 50` 
run `nix-channel --update` and `nix-env -u` uninstall the packages that no longer needed and install the packages that saved at start.

---
### Unable to Update CentOS7
**OS:** CentOS 7 or 8
**Tags:** #linux #CentOS #Update #YUM
**Description:** Cant Update system
**References:** https://stackoverflow.com/questions/70963985/error-failed-to-download-metadata-for-repo-appstream-cannot-prepare-internal

```
yum update -y
Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
```

**Solution:** 
Go to `/etc/yum.repos.d/`

Run:
```
sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*`
sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
`sudo yum update -y
```

---
### Communicate different pods using Podman

**OS:** Arch Linux
**Tags:** #podman #Docker #network
**References:** https://stackoverflow.com/questions/71141056/communicate-different-pods-using-podman

**Description:**
I am deploying several Pods using podman-compose. To do so, each pod has its own definition in a podman-compose.yaml file that I execute in rootless mode (so all containers in a Pod coexist in the same host/IP). However, I would like to make able a container in a Pod to reach a service exposed by a container in another pod.

**Solution:**
```
podman network create $NETWORK_NAME

podman pod create --name $POD1 --network $NETWORK_NAME

podman pod create --name $POD2 --network $NETWORK_NAME

podman run -it --detach --pod $POD1 --name $CONTAINER1 --network $NETWORK_NAME image_name

podman run -it --detach --pod $POD2 --name $CONTAINER2 --network $NETWORK_NAME image_name

```

---
### Unable to Connect to EC2 instance with RDP 
**Type:** Fixed RDP EC2 Instance cert error
**OS:** Amazon Linux (Fedora base)
**Tags:** #AWS, #cloud, #EC2, #RDP 

**Description:** 
While trying to run GUI EC2 instance (MATE Desktop Enviroment) I got this certificate error while checking log with
`systemctl status xrdp`
`.... /etc/xrdp/cert.pem and key.pem not found` <-- Something like this

**Solution:**
so we should generate the keys for them.
just login with ssh or ec2-connect from gui
and run this command 
`sudo openssl req -x509 -newkey rsa:2048 -nodes -keyout /etc/xrdp/key.pem -out /etc/xrdp/cert.pem -days 365`

and reload the RDP service
`systemctl restart xrdp`

**Extra Notes: -**
 