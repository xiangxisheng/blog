# PVE附加VHDX到虚拟机

## 一、附加VHDX
第1步：打开nbd功能
```
modprobe nbd max_part=4
```

第2步：挂载vhdx到nbd设备里
```
qemu-nbd -c /dev/nbd0 <VHDX文件路径>
```

第3步：附加nbd设备到VM虚拟机里
```
qm set <虚拟机编号> -scsi1 /dev/nbd0
```

# 二、取消附加

第1步：在控制台中分离scsi

第2步：分离nbd
qemu-nbd -d /dev/nbd0

第3步：查看已挂载的nbd
```
ps -o command -C qemu-nbd
```

