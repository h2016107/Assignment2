# Assignment2
Block device drivers are integrated with buffer cache mechanism for its implementation. The various steps involved in the implementation are as follows. The first step is to register for a major number of the device. It is done using register_blkdev function. Then we have the request queue for queuing the read and write requests.Spin lock is used with the request queue for its concurrent access protection and a request function to process the requests queued in the request queue. The device file operations are provided through the struct block_device_operations.The block device related specific things are registered using gendisk structure.
Ram_device.c and ram_device.h holds RAM operations like vmalloc, memcpy etc.They provide disk operation APIs like init,cleanup,read,write etc.
Partition.c and partition.h helps to emulate the various partition tables on the disk on RAM.
Ram_block.c is the core block driver implementation casting the disk on RAM as the block device files (/dev/rb*) to user space.

$ make -C /lib/modules/$(uname -r)/build M=$PWD modules 
The command to build module.

sudo insmod bram.ko
The above command to load kernel module

ls -l /dev/rb*
The above command to see whether block device files are created or not.
rb1, rb2 and rb3 are the primary partitions, with rb2 being the extended partition and containing three logical partitions rb5, rb6 and rb7.

sudo fdisk -l /dev/rb
The above command to clearly see the partitions.
sudo chmod 777 /dev/rb2
The above command to give all priviledge to a particular partition where we want to read or write
sudo cat /dev/rb2
The above command to read partition
sudo cat > /dev/rb2
The above command to write and then press enter and then save by pressing control plus s.
sudo cat /dev/rb2
Finally use above command to read the value we wrote.It is read correctly.




