---
title: "Using cloud inti in virtual box"
date: "10-10-2022"
---

# Setting up the lab

## Me rambling

I started looking to set up a hacking lab to practice some pentesting. Inorder to do so I needed some machines. Kali, windows and some ubuntu/debian servers. It has been a while since I have had to do this kind of setup. As a developer I have been in containers and while those are :100: useful later on I wanted to get back into VMs.

## VirtualBoxs and cloud-init

I grabbed the ova files for Kali and Windows and those started with no issues :rocket:. I was able to get them in a NatNetork and talking. It was a really helpful hacking victim.

Then came Ubuntu and a lost Sunday. I found the cloud-images here https://cloud-images.ubuntu.com. Downloaded the OVA file, imported it, updated the network and got to the login screen. Where I could not login. There was no default. So as a decent enough developer I turned to Google.

I found out pretty quickly that the OVA relied on cloud-init. Something that would be nice to see in a readme or something in the directory structure but regardless I knew the tooling.
With a bunch more Gooogling I found that this relied on a mounted file to parse some YAML to setup some configs. There was no one good here is the way to get this running so below are my steps on a Windows 11 machine.

## Steps to get Ubuntu cloud image Running in VirtualBox

1. You will need WSL2 installed and running.
2. I worked in (ubuntu path) `/mnt/c/Users/Me/Documents/Code/vm-images/cidata`
3. Create 2 file `user-data`
   1. `meta-data` - general box information like hostname
   2. `user-data` - setting up groups and users
4. I downloaded the template that Amazon had
   1. https://cdn.amazonlinux.com/os-images/2.0.20190612/README.cloud-init
   2. It helped make sure the YAML was correct
5. Install `sudo apt install whois`
   1. This give you `mkpasswd` to generate a password.
   2. `mkpasswd -m sha-512 -s`- the password prompt is what you want hashed
6. `meta-data` - I really only used the hostname
7. `user-data`
   1. I could not use plain-text passwords
   2. Alignment here is correct
   3. The hashed password does not seem to need quotes like some suggest.

```
#cloud-config
# vim:syntax=yaml
users:
  # A user by the name ec2-user is created in the image by default.
  - default
  # The following entry creates user1 and assigns a plain text password.
  # Please note Security best practises recommend not using plain text password.
  # The hash is for the password test1234
  - name: ispriv
    gecos: test ispriv with plain passwd configured and sudo nopasswd enabled
    groups: sudo
    sudo: ["ALL=(ALL) NOPASSWD:ALL"]
    passwd: $6$7ZCQ7FB3pY$B4VmokACOoly3MhSJLCm/xy8NqfJDMPlIShHfqjXjwjmVphbnKGrBoJbdgdxd3CL5Rq2h/iE49fBjRiBbbQQx/
    lock_passwd: false
```

8. Creating an iso, ususally `seed.iso`, to mount in the vm
   1. Install `sudo apt install cloud-image-utils`
      1. This is built to create iso with `user-data` and `meta-data`.
      2. Run `cloud-localds seed.iso user-data meta-data`
   2. Congrats the hard stuff is done
9. In the VM that is created by importing the ova add an optical drive with seed.iso
10. Boot the VM and you should be able to login with `ispriv`:`test1234`
