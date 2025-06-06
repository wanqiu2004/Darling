## 拍摄快照
 使用快照保留虚拟机状态
 使用快照管理器
 恢复到快照
 在关机时拍摄快照或恢复到快照
 启用自动保护快照
 启用后台快照
 从快照中排除虚拟磁盘
 删除快照


### 使用快照保留虚拟机状态
对于本地虚拟机，每个线性过程可以拍摄超过 100 个快照。

### 使用快照管理器
查看虚拟机的所有快照，并在快照管理器中直接对其进行操作
下列任务必须使用快照管理器执行：
- 在快照菜单中显示自动保护快照。
- 防止自动保护快照被删除。
- 重命名快照或更改快照的描述。
- 删除快照。

所有快照操作可在虚拟机菜单下的快照菜单中作为菜单项提供。
对于使用物理磁盘的虚拟机，您无法拍摄快照。
可对客户机操作系统的驱动器进行碎片整理

###在关机时拍摄快照或恢复到快照
虚拟机 > 设置 > 选项 > 快照

###启用自动保护快照
指定的时间间隔定期拍摄快照
自动保护只会在虚拟机处于开启状态时拍摄快照
虚拟机 > 设置 > 选项 > 自动保护 > 启用自动保护
达到最大自动保护快照数后，Workstation Pro 每次拍摄新的自动保护快照时会删除最早的自动保护
快照。此设置不会影响您所能拍摄和保留的手动快照的数量。

###从快照中排除虚拟磁盘
希望将一些磁盘恢复到快照，同时保留对其他磁盘所做的所有更改。
关闭虚拟机。
删除现有快照。
虚拟机 > 设置 > 硬件
选择要排除的驱动器，然后单击高级。
选择独立，然后选择磁盘模式。

###删除快照
删除快照不会影响虚拟机的当前状态。
如果快照已用于创建克隆，则会变为锁定状态。如果删除锁定的快照，通过该快照创建的克隆将无法继续正常工作。
如果快照关联的虚拟机已被指定为克隆模板，则无法删除快照。