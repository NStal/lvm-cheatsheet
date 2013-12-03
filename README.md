lvm-cheatsheet
==============

LVM cheat sheet

We can test lvm by creating IMG file using dd and mount the image as a loop device. And use the loop device as the fake disk. using losetup to create a loop device. (don't include in the cheat sheet)


```bash
# create physical volume
pvcreate /dev/loop0
pvcreate /dev/loop1

# create volume group
vgcreate lvm-volume-group-name /dev/loop0 /dev/loop1 <any other list,...>

# check created volume group
vgscan 

# create logic volum
lvcreate -n logical-volume-name --size 1g lvm-volume-group-name
lvcreate -n logical-volume-name2 --size 2g lvm-volume-group-name

# now we can mount /dev/lvm-volume-group-name/logical-volume-name (or name2) as a normal partition

# view logical partition info
lvdisplay

# resize (add)
lvextend -L+1G /dev/lvm-volume-group-name/logical-volume-name

# if we nolonger want the disk, then delete it
lvremove /dev/lvm-volume-group-name/logical-volume-name
```
