
安装osxfuse最新版：https://github.com/osxfuse/osxfuse/releases；
安装ntfs-3g开源实现：brew install ntfs-3g
进入macos 恢复模式（启动时使用Command+R）;
csrutil disable; 关闭mac 系统完整性保护；
重启，进入正常模式；csrutil status 检查是否关闭系统完整性保护；
重新挂载根目录，使得系统关键目录可写：sudo mount -uw / 
备份原有mount_ntfs命令：sudo mv /sbin/mount_ntfs /sbin/mount_ntfs.original 
创建软链接，指向ntfs-3g命令：sudo ln -s /usr/local/sbin/mount_ntfs /sbin/mount_ntfs
重新，进入恢复模式，重新开启系统完整性保护：csrutil enable 
重新进入正常模式；重新插入U盘，即可可读可写；
mount 查看挂载情况：状态正常
