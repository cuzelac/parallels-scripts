# Parallels Automation for CentOS VMs

## Description

Some automation tools I've written to help manage Parallels VMs running CentOS

This has been tested and used extensively with Parallels 7

## Setup

Before you can use pnew, you'll need to build a cloneable template

1. Make sure the `p*` files in `bin` are somewhere in your `$PATH`
1. Build a CentOS VM in Parallels
1. Install Parallels Tools in that VM
1. put `root/setup.sh` in the VM's /root and make sure it's executable
1. Shut down the vm 
    * you can optionally clone it to a template so you don't
      accidentally screw up your base image

            prlctl clone BASE_VM_NAME --name NEW_NAME --template

1. Update the variable `BASE` with the UUID of your base VM
    * for templates: `prlctl list --template`
    * for regular VMs: `prlctl list --all`
1. Try it out: `pnew NEW_VM_NAME`

## Usage

1. Clone a new VM with `pnew VM_NAME`
1. Start up and ssh into a stopped or suspended VM with `pstart VM_NAME`
1. Log in to a running VM with `pssh VM_NAME`
1. Get the IP address of a VM with `pip VM_NAME`
    * useful for copying files around

## Notes / TODOs

* If you can avoid it, don't use LVM - it makes it harder for Parallels
  to compress the disks
* current e2fsprogs: git clone http://git.kernel.org/cgit/fs/ext2/e2fsprogs.git
    * It contains 'e4defrag' which may help Parallels save disk space
* How to find RPMs and sort by size: `rpm -qa --qf '%{SIZE}\t%{NAME}\n' | sort -n`
