*Journal, Rasmus Groth, Utterslev, Copenhagen, Denmark*
Started: 20190426
Edited: 20190426

# How to mount a linode server as a drive on a mac
[DigitalOcean tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh)

[Dowload and install FUSE and SSHFS for osx](https://osxfuse.github.io/)

Create a directory for the mount
```
sudo mkdir /mnt/ccat_linode
```

```
sudo sshfs -o allow_other,defer_permissions root@176.58.121.49:/ /mnt/ccat_linode
```
