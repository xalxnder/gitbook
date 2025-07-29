# LVM

## Creating Logical Volumes (Without Partition)

#### 1. **Create the Physical Volume (PV) on the whole disk**

```bash
sudo pvcreate /dev/sdb
```

> ⚠️ Do **not** format the disk or partition it — this command writes LVM metadata directly to the disk.

***

#### 🔸 2. **Create a Volume Group (VG)**

```bash
sudo vgcreate nexus-vg /dev/sdb
```

\`

***

#### 🔸 3. **Create Logical Volumes (LVs)**

**One for DB Data (100G):**

```
sudo lvcreate -L 100G -n nexus-dbdata nexus-vg
```

\`\
**One for Config (use the rest of the space):**

```
sudo lvcreate -l 100%FREE -n nexus-config nexus-vg
```

***

#### 🔸 4. **Create Filesystems**

```
sudo mkfs.xfs /dev/nexus-vg/nexus-dbdata 
sudo mkfs.xfs /dev/nexus-vg/nexus-config
```

***

#### 🔸 5. **Create Mount Points**

```
sudo mkdir -p /opt/nexus-db sudo mkdir -p /opt/nexus-config
```

***

#### 🔸 6. **Add Entries in FSTAB**

```
/dev/common/blob /mnt/common xfs defaults 0 0  
/dev/itacsit/blob /mnt/itacsit xfs defaults 0 0                                                                                                                              
/dev/bit/data /opt/test xfs defaults 0 0
```

#### 🔸 7. **Mount**

```
mount -a
systemctl daemon reload
```

## Resizing LVM Logical Volumes

To increase the size of a logical volume, you need to have disk space available in the volume group, so we address that first.

> \[!TIP] The size of an XFS file system cannot be decreased; it can only be increased. If you need a file system that can be shrunk in size, use Ext4, not XFS.

### Resizing Volume Groups

The `vgextend` command is used to add storage to a volume group, and the `vgreduce` command is used to take physical volumes out of a volume group. For the exam, you WILL need to know how to extend. Here are the steps:\
22\. Make sure that a physical volume or device is available to be added to the volume group.\
23\. Use `vgextend` to extend the volume group. The new disk space will show immediately in the volume group.\
24\. Verify everything with the `vgs` command.

### Resizing Logical Volumes and File Systems

Logical volumes can be extended with the `lvextend` command. This command has a very useful option -r to take care of extending the file systems on the logical volume at the same time; it is recommended to use this option and not the alternative approach that separately extends the logical volumes and the file systems on top of the logical volumes. The easiest and most intuitive way to do that is by using -L followed by a + sign and the amount of disk space you want to add, as in `lvresize -L +1G -r /dev/vgdata/lvdata`.
