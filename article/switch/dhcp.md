# 如何在华为交换机上给自己的终端设备DHCP静态绑定一个特别IP

首先在用户模式下输入
```
display ip pool interface Vlanif81 used | include 1b7c
```
后面的1b7c就是自己终端设备的mac地址后4位
```
 -------------------------------------------------------------------------------------
 Client-ID format as follows:            
   DHCP  : mac-address                 PPPoE   : mac-address            
   IPSec : user-id/portnumber/vrf      PPP     : interface index            
   L2TP  : cpu-slot/session-id         SSL-VPN : user-id/session-id
 -------------------------------------------------------------------------------------
  Index              IP             Client-ID    Type       Left   Status           
 -------------------------------------------------------------------------------------
   4534    10.81.42.99         b485-e1a0-1b7c    DHCP    7775112   Used
 -------------------------------------------------------------------------------------
```
可以看到自己绑定了一个10.81.42.99的IP
同样也是在用户模式下输入reset指令把MAC地址绑定的IP回收掉
```
reset ip pool interface Vlanif81 10.81.42.99
```
然后再进到
```
system-view
interface Vlanif 81
dhcp server static-bind ip-address 10.81.1.1 mac-address b485-e1a0-1b7c
```
