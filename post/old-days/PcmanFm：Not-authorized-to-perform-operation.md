## 问题
普通用户下，PcmanFm不能直接挂载非系统分区，提示Not authorized to perform operation
## 解决
root 下edit
```
/usr/share/polkit-1/actions/org.freedesktop.UDisks2.policy
```
on
```
 <action id="org.freedesktop.udisks2.filesystem-mount-system">
    <description>Mount a filesystem on a system device</description>
    ...
      <allow_any>auth_admin</allow_any>
      <allow_inactive>auth_admin</allow_inactive>
      <allow_active>yes</allow_active> // 更改这里为yes 
    </defaults>
  </action>
```
## 效果
OK
