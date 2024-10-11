
1. First You need to make sure you have enough space on hdd where you created the image 

2.  Next  you open the terminal and cd into the directory where your vms are, for example the default location is "/var/lib/libvirt/images" , so you run the command

 ```   
     cd /var/lib/libvirt/images
```

3. Next step is to run the "ls" command in the directory to see the images and choose the one you want to resize, for example "image.qcow2".

```
     ls
```

4. Than you can run the command  
    
```
     sudo qemu-img resize image.qcow2 sizeG
```

 where "size" is the size you want to add to the vm 
 if you are directly cd in the directory ( capital G not lowercase ! ) or run the command

```
	 sudo qemu-img resize /var/lib/libvirt/images/image.qcow2 sizeG
```