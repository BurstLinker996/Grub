# 什么是Grub?

## 官方介绍
GNU GRUB is a  [Multiboot](http://www.gnu.org/software/grub/manual/multiboot/multiboot.html)  boot loader. It was derived from GRUB, the  **GRand Unified Bootloader**, which was originally designed and implemented by Erich Stefan Boleyn.

Briefly, a  _boot loader_  is the first software program that runs when a computer starts. It is responsible for loading and transferring control to the operating system  _kernel_  software (such as  [the Hurd](https://www.gnu.org/software/hurd/hurd.html)  or Linux). The kernel, in turn, initializes the rest of the operating system (e.g. GNU).

##  Wiki中文百科
**GNU GRUB**（简称“GRUB”）是一个来自[GNU项目](https://zh.wikipedia.org/wiki/GNU%E8%A8%88%E5%8A%83 "类Unix系统")的[启动引导程序](https://zh.wikipedia.org/wiki/%E5%90%AF%E5%8A%A8%E5%BC%95%E5%AF%BC%E7%A8%8B%E5%BA%8F)。GRUB是[多启动规范](https://zh.wikipedia.org/w/index.php?title=%E5%A4%9A%E5%90%AF%E5%8A%A8%E8%A7%84%E8%8C%83&action=edit&redlink=1 "多启动规范（页面不存在）")的实现，它允许用户可以在计算机内同时拥有多个操作系统，并在计算机启动时选择希望运行的操作系统。GRUB可用于选择操作系统分区上的不同[内核](https://zh.wikipedia.org/wiki/%E5%86%85%E6%A0%B8 "内核")，也可用于向这些内核传递启动参数。

GNU GRUB的前身为**Grand Unified Bootloader**。它主要用于[类Unix系统](https://zh.wikipedia.org/wiki/%E7%B1%BBUnix%E7%B3%BB%E7%BB%9F)；同大多[Linux发行版](https://zh.wikipedia.org/wiki/Linux%E5%8F%91%E8%A1%8C%E7%89%88 "启动引导程序")一样，[GNU](https://zh.wikipedia.org/wiki/GNU "GNU")系统也采用GNU GRUB作为它的启动器。[Solaris](https://zh.wikipedia.org/wiki/Solaris "Solaris")从10 1/06版开始在x86系统上也采用GNU GRUB作为启动器。


### 本仓库是应用grub实现多系统引导菜单的配置示例，核心配置请看[grub.cfg](/grub/grub.cfg)。以下是某个引导菜单项的声明语法：

    #使用menuentry定义引导菜单项"PartAssist"
    #menuentry用法: menuentry title [--class=class …] [--users=users] [--unrestricted] [--hotkey=key] [--id=id] [arg …] { command; … }
    menuentry "PartAssist"  {
        #$1表示title也就是PartAssist
        #使用search查找卷标是PartAssist的分区并设置为根设备
        search --label $1 --set
        #链式引导PartAssist分区下的bootx64.efi
        chainloader /efi/boot/bootx64.efi
        echo $1
    }

### QEMU预览效果：
<img src="/screenshot/preview.png"/>

<font color=red size=5>注意本仓库是在本地移动硬盘的分区结构下进行测试的，仓库配置仅供参考和测试，请按实际本地环境进行修改。</font>
