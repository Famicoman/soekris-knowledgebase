
### From Soekris Info Wiki



Jump to: [navigation](Configuration_for_Gentoo.html#column-one), [search](Configuration_for_Gentoo.html#searchInput) 
This applies to net4801


make.conf for Gentoo :




```
# These settings were set by the catalyst build script that automatically built this stage
# Please consult /etc/make.conf.example for a more detailed example
CFLAGS="-O2 -march=i586 -pipe"
CHOST="i586-pc-linux-gnu"
CXXFLAGS="${CFLAGS}"
MAKEOPTS="-j2"
SYNC="rsync://rsync.europe.gentoo.org/gentoo-portage"
USE="-X -gtk -gnome -kde apache2 ftp lm\_sensors mmx mysql ncurses nptl nptlonly pdf ruby verbose"
PORTAGE\_RSYNC\_EXTRA\_OPTS="--exclude-from=/etc/portage/rsync\_excludes"

```

  

.config for kernel 2.6.20-gentoo-r8 :  



  





```
# Automatically generated make config: don't edit
# Linux kernel version: 2.6.20-gentoo-r8
# Tue May  8 18:53:17 2007
#
CONFIG\_X86\_32=y
CONFIG\_GENERIC\_TIME=y
CONFIG\_LOCKDEP\_SUPPORT=y
CONFIG\_STACKTRACE\_SUPPORT=y
CONFIG\_SEMAPHORE\_SLEEPERS=y
CONFIG\_X86=y
CONFIG\_MMU=y
CONFIG\_GENERIC\_ISA\_DMA=y
CONFIG\_GENERIC\_IOMAP=y
CONFIG\_GENERIC\_BUG=y
CONFIG\_GENERIC\_HWEIGHT=y
CONFIG\_ARCH\_MAY\_HAVE\_PC\_FDC=y
CONFIG\_DMI=y
CONFIG\_DEFCONFIG\_LIST="/lib/modules/$UNAME\_RELEASE/.config" 

#
# Code maturity level options
#
CONFIG\_EXPERIMENTAL=y
CONFIG\_BROKEN\_ON\_SMP=y
CONFIG\_INIT\_ENV\_ARG\_LIMIT=32

#
# General setup
#
CONFIG\_LOCALVERSION=""
# CONFIG\_LOCALVERSION\_AUTO is not set
CONFIG\_SWAP=y
CONFIG\_SYSVIPC=y
# CONFIG\_IPC\_NS is not set
# CONFIG\_POSIX\_MQUEUE is not set
# CONFIG\_BSD\_PROCESS\_ACCT is not set
# CONFIG\_TASKSTATS is not set
# CONFIG\_UTS\_NS is not set
# CONFIG\_AUDIT is not set
CONFIG\_IKCONFIG=y
CONFIG\_IKCONFIG\_PROC=y
CONFIG\_SYSFS\_DEPRECATED=y
# CONFIG\_RELAY is not set
CONFIG\_INITRAMFS\_SOURCE=""
CONFIG\_CC\_OPTIMIZE\_FOR\_SIZE=y
CONFIG\_SYSCTL=y
# CONFIG\_EMBEDDED is not set
CONFIG\_UID16=y
CONFIG\_SYSCTL\_SYSCALL=y
CONFIG\_KALLSYMS=y
# CONFIG\_KALLSYMS\_EXTRA\_PASS is not set
CONFIG\_HOTPLUG=y
CONFIG\_PRINTK=y
CONFIG\_BUG=y
CONFIG\_ELF\_CORE=y
CONFIG\_BASE\_FULL=y
CONFIG\_FUTEX=y
CONFIG\_EPOLL=y
CONFIG\_SHMEM=y
CONFIG\_SLAB=y
CONFIG\_VM\_EVENT\_COUNTERS=y
CONFIG\_RT\_MUTEXES=y
# CONFIG\_TINY\_SHMEM is not set
CONFIG\_BASE\_SMALL=0
# CONFIG\_SLOB is not set 

#
# Loadable module support
#
CONFIG\_MODULES=y
CONFIG\_MODULE\_UNLOAD=y
CONFIG\_MODULE\_FORCE\_UNLOAD=y
# CONFIG\_MODVERSIONS is not set
# CONFIG\_MODULE\_SRCVERSION\_ALL is not set
CONFIG\_KMOD=y

#
# Block layer
#
CONFIG\_BLOCK=y
# CONFIG\_LBD is not set
# CONFIG\_BLK\_DEV\_IO\_TRACE is not set
# CONFIG\_LSF is not set

#
# IO Schedulers
#
CONFIG\_IOSCHED\_NOOP=y
# CONFIG\_IOSCHED\_AS is not set
# CONFIG\_IOSCHED\_DEADLINE is not set
CONFIG\_IOSCHED\_CFQ=y
# CONFIG\_DEFAULT\_AS is not set
# CONFIG\_DEFAULT\_DEADLINE is not set
CONFIG\_DEFAULT\_CFQ=y
# CONFIG\_DEFAULT\_NOOP is not set
CONFIG\_DEFAULT\_IOSCHED="cfq"

#
# Processor type and features
#
# CONFIG\_SMP is not set
CONFIG\_X86\_PC=y
# CONFIG\_X86\_ELAN is not set
# CONFIG\_X86\_VOYAGER is not set
# CONFIG\_X86\_NUMAQ is not set
# CONFIG\_X86\_SUMMIT is not set
# CONFIG\_X86\_BIGSMP is not set
# CONFIG\_X86\_VISWS is not set
# CONFIG\_X86\_GENERICARCH is not set
# CONFIG\_X86\_ES7000 is not set
# CONFIG\_PARAVIRT is not set
# CONFIG\_M386 is not set
# CONFIG\_M486 is not set
# CONFIG\_M586 is not set
# CONFIG\_M586TSC is not set
# CONFIG\_M586MMX is not set
# CONFIG\_M686 is not set
# CONFIG\_MPENTIUMII is not set
# CONFIG\_MPENTIUMIII is not set
# CONFIG\_MPENTIUMM is not set
# CONFIG\_MCORE2 is not set
# CONFIG\_MPENTIUM4 is not set
# CONFIG\_MK6 is not set
# CONFIG\_MK7 is not set
# CONFIG\_MK8 is not set
# CONFIG\_MCRUSOE is not set
# CONFIG\_MEFFICEON is not set
# CONFIG\_MWINCHIPC6 is not set
# CONFIG\_MWINCHIP2 is not set
# CONFIG\_MWINCHIP3D is not set
CONFIG\_MGEODEGX1=y
# CONFIG\_MGEODE\_LX is not set
# CONFIG\_MCYRIXIII is not set
# CONFIG\_MVIAC3\_2 is not set
# CONFIG\_X86\_GENERIC is not set
CONFIG\_X86\_CMPXCHG=y
CONFIG\_X86\_XADD=y
CONFIG\_X86\_L1\_CACHE\_SHIFT=4
CONFIG\_RWSEM\_XCHGADD\_ALGORITHM=y
# CONFIG\_ARCH\_HAS\_ILOG2\_U32 is not set
# CONFIG\_ARCH\_HAS\_ILOG2\_U64 is not set
CONFIG\_GENERIC\_CALIBRATE\_DELAY=y
CONFIG\_X86\_PPRO\_FENCE=y
CONFIG\_X86\_WP\_WORKS\_OK=y
CONFIG\_X86\_INVLPG=y
CONFIG\_X86\_BSWAP=y
CONFIG\_X86\_POPAD\_OK=y
CONFIG\_X86\_CMPXCHG64=y
CONFIG\_X86\_ALIGNMENT\_16=y
CONFIG\_X86\_TSC=y
# CONFIG\_HPET\_TIMER is not set
CONFIG\_PREEMPT\_NONE=y
# CONFIG\_PREEMPT\_VOLUNTARY is not set
# CONFIG\_PREEMPT is not set
CONFIG\_X86\_UP\_APIC=y
CONFIG\_X86\_UP\_IOAPIC=y
CONFIG\_X86\_LOCAL\_APIC=y
CONFIG\_X86\_IO\_APIC=y
CONFIG\_X86\_MCE=y
CONFIG\_X86\_MCE\_NONFATAL=y
# CONFIG\_X86\_MCE\_P4THERMAL is not set
CONFIG\_VM86=y
# CONFIG\_TOSHIBA is not set
# CONFIG\_I8K is not set
# CONFIG\_X86\_REBOOTFIXUPS is not set
# CONFIG\_MICROCODE is not set
# CONFIG\_X86\_MSR is not set
# CONFIG\_X86\_CPUID is not set

#
# Firmware Drivers
#
# CONFIG\_EDD is not set
# CONFIG\_DELL\_RBU is not set
# CONFIG\_DCDBAS is not set
CONFIG\_NOHIGHMEM=y
# CONFIG\_HIGHMEM4G is not set
# CONFIG\_HIGHMEM64G is not set
CONFIG\_PAGE\_OFFSET=0xC0000000
CONFIG\_ARCH\_FLATMEM\_ENABLE=y
CONFIG\_ARCH\_SPARSEMEM\_ENABLE=y
CONFIG\_ARCH\_SELECT\_MEMORY\_MODEL=y
CONFIG\_ARCH\_POPULATES\_NODE\_MAP=y
CONFIG\_SELECT\_MEMORY\_MODEL=y
CONFIG\_FLATMEM\_MANUAL=y
# CONFIG\_DISCONTIGMEM\_MANUAL is not set
# CONFIG\_SPARSEMEM\_MANUAL is not set
CONFIG\_FLATMEM=y
CONFIG\_FLAT\_NODE\_MEM\_MAP=y
CONFIG\_SPARSEMEM\_STATIC=y
CONFIG\_SPLIT\_PTLOCK\_CPUS=4
# CONFIG\_RESOURCES\_64BIT is not set
# CONFIG\_MATH\_EMULATION is not set
CONFIG\_MTRR=y
# CONFIG\_EFI is not set
# CONFIG\_SECCOMP is not set
CONFIG\_HZ\_100=y
# CONFIG\_HZ\_250 is not set
# CONFIG\_HZ\_300 is not set
# CONFIG\_HZ\_1000 is not set
CONFIG\_HZ=100
# CONFIG\_KEXEC is not set
CONFIG\_PHYSICAL\_START=0x100000
# CONFIG\_RELOCATABLE is not set
CONFIG\_PHYSICAL\_ALIGN=0x100000
CONFIG\_COMPAT\_VDSO=y

#
# Power management options (ACPI, APM)
#
CONFIG\_PM=y
# CONFIG\_PM\_LEGACY is not set
# CONFIG\_PM\_DEBUG is not set
# CONFIG\_PM\_SYSFS\_DEPRECATED is not set
CONFIG\_SOFTWARE\_SUSPEND=y
CONFIG\_PM\_STD\_PARTITION="/dev/hda2"

#
# ACPI (Advanced Configuration and Power Interface) Support
#
CONFIG\_ACPI=y
# CONFIG\_ACPI\_SLEEP is not set
# CONFIG\_ACPI\_AC is not set
# CONFIG\_ACPI\_BATTERY is not set
# CONFIG\_ACPI\_BUTTON is not set
# CONFIG\_ACPI\_VIDEO is not set
# CONFIG\_ACPI\_HOTKEY is not set
# CONFIG\_ACPI\_FAN is not set
# CONFIG\_ACPI\_DOCK is not set
# CONFIG\_ACPI\_PROCESSOR is not set
# CONFIG\_ACPI\_ASUS is not set
# CONFIG\_ACPI\_IBM is not set
# CONFIG\_ACPI\_TOSHIBA is not set
CONFIG\_ACPI\_BLACKLIST\_YEAR=0
# CONFIG\_ACPI\_DEBUG is not set
CONFIG\_ACPI\_EC=y
CONFIG\_ACPI\_POWER=y
CONFIG\_ACPI\_SYSTEM=y
CONFIG\_X86\_PM\_TIMER=y
# CONFIG\_ACPI\_CONTAINER is not set
# CONFIG\_ACPI\_SBS is not set

#
# APM (Advanced Power Management) BIOS Support
#
# CONFIG\_APM is not set

#
# CPU Frequency scaling
#
CONFIG\_CPU\_FREQ=y
CONFIG\_CPU\_FREQ\_TABLE=y
# CONFIG\_CPU\_FREQ\_DEBUG is not set
CONFIG\_CPU\_FREQ\_STAT=y
# CONFIG\_CPU\_FREQ\_STAT\_DETAILS is not set
CONFIG\_CPU\_FREQ\_DEFAULT\_GOV\_PERFORMANCE=y
# CONFIG\_CPU\_FREQ\_DEFAULT\_GOV\_USERSPACE is not set
CONFIG\_CPU\_FREQ\_GOV\_PERFORMANCE=y
# CONFIG\_CPU\_FREQ\_GOV\_POWERSAVE is not set
# CONFIG\_CPU\_FREQ\_GOV\_USERSPACE is not set
# CONFIG\_CPU\_FREQ\_GOV\_ONDEMAND is not set
# CONFIG\_CPU\_FREQ\_GOV\_CONSERVATIVE is not set

#
# CPUFreq processor drivers
#
# CONFIG\_X86\_POWERNOW\_K6 is not set
# CONFIG\_X86\_POWERNOW\_K7 is not set
# CONFIG\_X86\_POWERNOW\_K8 is not set
CONFIG\_X86\_GX\_SUSPMOD=y
# CONFIG\_X86\_SPEEDSTEP\_CENTRINO is not set
# CONFIG\_X86\_SPEEDSTEP\_ICH is not set
# CONFIG\_X86\_SPEEDSTEP\_SMI is not set
# CONFIG\_X86\_P4\_CLOCKMOD is not set
# CONFIG\_X86\_CPUFREQ\_NFORCE2 is not set
# CONFIG\_X86\_LONGRUN is not set

#
# shared options
#
# CONFIG\_X86\_SPEEDSTEP\_LIB is not set

#
# Bus options (PCI, PCMCIA, EISA, MCA, ISA)
#
CONFIG\_PCI=y
# CONFIG\_PCI\_GOBIOS is not set
# CONFIG\_PCI\_GOMMCONFIG is not set
# CONFIG\_PCI\_GODIRECT is not set
CONFIG\_PCI\_GOANY=y
CONFIG\_PCI\_BIOS=y
CONFIG\_PCI\_DIRECT=y
CONFIG\_PCI\_MMCONFIG=y
# CONFIG\_PCIEPORTBUS is not set
# CONFIG\_PCI\_MSI is not set
CONFIG\_HT\_IRQ=y
CONFIG\_ISA\_DMA\_API=y
CONFIG\_ISA=y
# CONFIG\_EISA is not set
# CONFIG\_MCA is not set
CONFIG\_SCx200=y
CONFIG\_SCx200HR\_TIMER=y

#
# PCCARD (PCMCIA/CardBus) support
#
# CONFIG\_PCCARD is not set

#
# PCI Hotplug Support
#
# CONFIG\_HOTPLUG\_PCI is not set

#
# Executable file formats
#
CONFIG\_BINFMT\_ELF=y
# CONFIG\_BINFMT\_AOUT is not set
# CONFIG\_BINFMT\_MISC is not set

#
# Networking
#
CONFIG\_NET=y

#
# Networking options
#
# CONFIG\_NETDEBUG is not set
CONFIG\_PACKET=y
CONFIG\_PACKET\_MMAP=y
CONFIG\_UNIX=y
CONFIG\_XFRM=y
# CONFIG\_XFRM\_USER is not set
# CONFIG\_XFRM\_SUB\_POLICY is not set
# CONFIG\_NET\_KEY is not set
CONFIG\_INET=y
CONFIG\_IP\_MULTICAST=y
CONFIG\_IP\_ADVANCED\_ROUTER=y
CONFIG\_ASK\_IP\_FIB\_HASH=y
# CONFIG\_IP\_FIB\_TRIE is not set
CONFIG\_IP\_FIB\_HASH=y
CONFIG\_IP\_MULTIPLE\_TABLES=y
# CONFIG\_IP\_ROUTE\_MULTIPATH is not set
# CONFIG\_IP\_ROUTE\_VERBOSE is not set
CONFIG\_IP\_PNP=y
# CONFIG\_IP\_PNP\_DHCP is not set
# CONFIG\_IP\_PNP\_BOOTP is not set
# CONFIG\_IP\_PNP\_RARP is not set
CONFIG\_NET\_IPIP=y
# CONFIG\_NET\_IPGRE is not set
# CONFIG\_IP\_MROUTE is not set
# CONFIG\_ARPD is not set
# CONFIG\_SYN\_COOKIES is not set
# CONFIG\_INET\_AH is not set
# CONFIG\_INET\_ESP is not set
# CONFIG\_INET\_IPCOMP is not set
# CONFIG\_INET\_XFRM\_TUNNEL is not set
CONFIG\_INET\_TUNNEL=y
CONFIG\_INET\_XFRM\_MODE\_TRANSPORT=y
CONFIG\_INET\_XFRM\_MODE\_TUNNEL=y
CONFIG\_INET\_XFRM\_MODE\_BEET=y
CONFIG\_INET\_DIAG=y
CONFIG\_INET\_TCP\_DIAG=y
CONFIG\_TCP\_CONG\_ADVANCED=y
CONFIG\_TCP\_CONG\_BIC=y
CONFIG\_TCP\_CONG\_CUBIC=m
CONFIG\_TCP\_CONG\_WESTWOOD=m
CONFIG\_TCP\_CONG\_HTCP=m
# CONFIG\_TCP\_CONG\_HSTCP is not set
# CONFIG\_TCP\_CONG\_HYBLA is not set
# CONFIG\_TCP\_CONG\_VEGAS is not set
# CONFIG\_TCP\_CONG\_SCALABLE is not set
# CONFIG\_TCP\_CONG\_LP is not set
# CONFIG\_TCP\_CONG\_VENO is not set
CONFIG\_DEFAULT\_BIC=y
# CONFIG\_DEFAULT\_CUBIC is not set
# CONFIG\_DEFAULT\_HTCP is not set
# CONFIG\_DEFAULT\_VEGAS is not set
# CONFIG\_DEFAULT\_WESTWOOD is not set
# CONFIG\_DEFAULT\_RENO is not set
CONFIG\_DEFAULT\_TCP\_CONG="bic"
# CONFIG\_TCP\_MD5SIG is not set

#
# IP: Virtual Server Configuration
#
CONFIG\_IP\_VS=m
# CONFIG\_IP\_VS\_DEBUG is not set
CONFIG\_IP\_VS\_TAB\_BITS=12

#
# IPVS transport protocol load balancing support
#
# CONFIG\_IP\_VS\_PROTO\_TCP is not set
# CONFIG\_IP\_VS\_PROTO\_UDP is not set
# CONFIG\_IP\_VS\_PROTO\_ESP is not set
# CONFIG\_IP\_VS\_PROTO\_AH is not set

#
# IPVS scheduler
#
# CONFIG\_IP\_VS\_RR is not set
# CONFIG\_IP\_VS\_WRR is not set
# CONFIG\_IP\_VS\_LC is not set
# CONFIG\_IP\_VS\_WLC is not set
# CONFIG\_IP\_VS\_LBLC is not set
# CONFIG\_IP\_VS\_LBLCR is not set
# CONFIG\_IP\_VS\_DH is not set
# CONFIG\_IP\_VS\_SH is not set
# CONFIG\_IP\_VS\_SED is not set
# CONFIG\_IP\_VS\_NQ is not set

#
# IPVS application helper
#
# CONFIG\_IPV6 is not set
# CONFIG\_INET6\_XFRM\_TUNNEL is not set
# CONFIG\_INET6\_TUNNEL is not set
# CONFIG\_NETWORK\_SECMARK is not set
CONFIG\_NETFILTER=y
# CONFIG\_NETFILTER\_DEBUG is not set
CONFIG\_BRIDGE\_NETFILTER=y

#
# Core Netfilter Configuration
#
# CONFIG\_NETFILTER\_NETLINK is not set
# CONFIG\_NF\_CONNTRACK\_ENABLED is not set
CONFIG\_NETFILTER\_XTABLES=m
CONFIG\_NETFILTER\_XT\_TARGET\_CLASSIFY=m
CONFIG\_NETFILTER\_XT\_TARGET\_MARK=m
CONFIG\_NETFILTER\_XT\_TARGET\_NFQUEUE=m
# CONFIG\_NETFILTER\_XT\_TARGET\_NFLOG is not set
CONFIG\_NETFILTER\_XT\_MATCH\_COMMENT=m
CONFIG\_NETFILTER\_XT\_MATCH\_DCCP=m
# CONFIG\_NETFILTER\_XT\_MATCH\_DSCP is not set
CONFIG\_NETFILTER\_XT\_MATCH\_ESP=m
CONFIG\_NETFILTER\_XT\_MATCH\_LENGTH=m
CONFIG\_NETFILTER\_XT\_MATCH\_LIMIT=m
CONFIG\_NETFILTER\_XT\_MATCH\_MAC=m
CONFIG\_NETFILTER\_XT\_MATCH\_MARK=m
# CONFIG\_NETFILTER\_XT\_MATCH\_POLICY is not set
CONFIG\_NETFILTER\_XT\_MATCH\_MULTIPORT=m
CONFIG\_NETFILTER\_XT\_MATCH\_PHYSDEV=m
CONFIG\_NETFILTER\_XT\_MATCH\_PKTTYPE=m
# CONFIG\_NETFILTER\_XT\_MATCH\_QUOTA is not set
CONFIG\_NETFILTER\_XT\_MATCH\_REALM=m
CONFIG\_NETFILTER\_XT\_MATCH\_SCTP=m
# CONFIG\_NETFILTER\_XT\_MATCH\_STATISTIC is not set
CONFIG\_NETFILTER\_XT\_MATCH\_STRING=m
CONFIG\_NETFILTER\_XT\_MATCH\_TCPMSS=m
# CONFIG\_NETFILTER\_XT\_MATCH\_HASHLIMIT is not set

#
# IP: Netfilter Configuration
#
# CONFIG\_IP\_NF\_QUEUE is not set
CONFIG\_IP\_NF\_IPTABLES=m
CONFIG\_IP\_NF\_MATCH\_IPRANGE=m
CONFIG\_IP\_NF\_MATCH\_TOS=m
CONFIG\_IP\_NF\_MATCH\_RECENT=m
CONFIG\_IP\_NF\_MATCH\_ECN=m
CONFIG\_IP\_NF\_MATCH\_AH=m
CONFIG\_IP\_NF\_MATCH\_TTL=m
# CONFIG\_IP\_NF\_MATCH\_OWNER is not set
# CONFIG\_IP\_NF\_MATCH\_ADDRTYPE is not set
CONFIG\_IP\_NF\_FILTER=m
# CONFIG\_IP\_NF\_TARGET\_REJECT is not set
CONFIG\_IP\_NF\_TARGET\_LOG=m
# CONFIG\_IP\_NF\_TARGET\_ULOG is not set
# CONFIG\_IP\_NF\_TARGET\_TCPMSS is not set
# CONFIG\_IP\_NF\_MANGLE is not set
CONFIG\_IP\_NF\_RAW=m
# CONFIG\_IP\_NF\_ARPTABLES is not set

#
# Bridge: Netfilter Configuration
#
CONFIG\_BRIDGE\_NF\_EBTABLES=m
# CONFIG\_BRIDGE\_EBT\_BROUTE is not set
# CONFIG\_BRIDGE\_EBT\_T\_FILTER is not set
# CONFIG\_BRIDGE\_EBT\_T\_NAT is not set
# CONFIG\_BRIDGE\_EBT\_802\_3 is not set
# CONFIG\_BRIDGE\_EBT\_AMONG is not set
# CONFIG\_BRIDGE\_EBT\_ARP is not set
# CONFIG\_BRIDGE\_EBT\_IP is not set
# CONFIG\_BRIDGE\_EBT\_LIMIT is not set
# CONFIG\_BRIDGE\_EBT\_MARK is not set
# CONFIG\_BRIDGE\_EBT\_PKTTYPE is not set
# CONFIG\_BRIDGE\_EBT\_STP is not set
# CONFIG\_BRIDGE\_EBT\_VLAN is not set
# CONFIG\_BRIDGE\_EBT\_ARPREPLY is not set
# CONFIG\_BRIDGE\_EBT\_DNAT is not set
# CONFIG\_BRIDGE\_EBT\_MARK\_T is not set
# CONFIG\_BRIDGE\_EBT\_REDIRECT is not set
# CONFIG\_BRIDGE\_EBT\_SNAT is not set
# CONFIG\_BRIDGE\_EBT\_LOG is not set
# CONFIG\_BRIDGE\_EBT\_ULOG is not set

#
# DCCP Configuration (EXPERIMENTAL)
#
# CONFIG\_IP\_DCCP is not set

#
# SCTP Configuration (EXPERIMENTAL)
#
# CONFIG\_IP\_SCTP is not set

#
# TIPC Configuration (EXPERIMENTAL)
#
# CONFIG\_TIPC is not set
# CONFIG\_ATM is not set
CONFIG\_BRIDGE=y
CONFIG\_VLAN\_8021Q=y
# CONFIG\_DECNET is not set
CONFIG\_LLC=y
# CONFIG\_LLC2 is not set
# CONFIG\_IPX is not set
# CONFIG\_ATALK is not set
# CONFIG\_X25 is not set
# CONFIG\_LAPB is not set
# CONFIG\_ECONET is not set
CONFIG\_WAN\_ROUTER=m

#
# QoS and/or fair queueing
#
CONFIG\_NET\_SCHED=y
CONFIG\_NET\_SCH\_FIFO=y
# CONFIG\_NET\_SCH\_CLK\_JIFFIES is not set
CONFIG\_NET\_SCH\_CLK\_GETTIMEOFDAY=y
# CONFIG\_NET\_SCH\_CLK\_CPU is not set

#
# Queueing/Scheduling
#
# CONFIG\_NET\_SCH\_CBQ is not set
# CONFIG\_NET\_SCH\_HTB is not set
# CONFIG\_NET\_SCH\_HFSC is not set
# CONFIG\_NET\_SCH\_PRIO is not set
# CONFIG\_NET\_SCH\_RED is not set
# CONFIG\_NET\_SCH\_SFQ is not set
# CONFIG\_NET\_SCH\_TEQL is not set
# CONFIG\_NET\_SCH\_TBF is not set
# CONFIG\_NET\_SCH\_GRED is not set
# CONFIG\_NET\_SCH\_DSMARK is not set
# CONFIG\_NET\_SCH\_NETEM is not set
# CONFIG\_NET\_SCH\_INGRESS is not set

#
# Classification
#
# CONFIG\_NET\_CLS\_BASIC is not set
# CONFIG\_NET\_CLS\_TCINDEX is not set
# CONFIG\_NET\_CLS\_ROUTE4 is not set
CONFIG\_NET\_CLS\_ROUTE=y
# CONFIG\_NET\_CLS\_FW is not set
# CONFIG\_NET\_CLS\_U32 is not set
# CONFIG\_NET\_CLS\_RSVP is not set
# CONFIG\_NET\_CLS\_RSVP6 is not set
# CONFIG\_NET\_EMATCH is not set
# CONFIG\_NET\_CLS\_ACT is not set
# CONFIG\_NET\_CLS\_POLICE is not set
# CONFIG\_NET\_ESTIMATOR is not set

#
# Network testing
#
# CONFIG\_NET\_PKTGEN is not set
# CONFIG\_HAMRADIO is not set
# CONFIG\_IRDA is not set
# CONFIG\_BT is not set
# CONFIG\_IEEE80211 is not set
CONFIG\_FIB\_RULES=y

#
# Device Drivers
#

#
# Generic Driver Options
#
CONFIG\_STANDALONE=y
CONFIG\_PREVENT\_FIRMWARE\_BUILD=y
# CONFIG\_FW\_LOADER is not set
# CONFIG\_SYS\_HYPERVISOR is not set

#
# Connector - unified userspace <-> kernelspace linker
#
# CONFIG\_CONNECTOR is not set

#
# Memory Technology Devices (MTD)
#
# CONFIG\_MTD is not set

#
# Parallel port support
#
CONFIG\_PARPORT=y
CONFIG\_PARPORT\_PC=y
# CONFIG\_PARPORT\_SERIAL is not set
# CONFIG\_PARPORT\_PC\_FIFO is not set
# CONFIG\_PARPORT\_PC\_SUPERIO is not set
# CONFIG\_PARPORT\_GSC is not set
# CONFIG\_PARPORT\_AX88796 is not set
CONFIG\_PARPORT\_1284=y

#
# Plug and Play support
#
# CONFIG\_PNP is not set

#
# Block devices
#
# CONFIG\_BLK\_DEV\_FD is not set
# CONFIG\_BLK\_DEV\_XD is not set
# CONFIG\_PARIDE is not set
# CONFIG\_BLK\_CPQ\_DA is not set
# CONFIG\_BLK\_CPQ\_CISS\_DA is not set
# CONFIG\_BLK\_DEV\_DAC960 is not set
# CONFIG\_BLK\_DEV\_UMEM is not set
# CONFIG\_BLK\_DEV\_COW\_COMMON is not set
CONFIG\_BLK\_DEV\_LOOP=y
# CONFIG\_BLK\_DEV\_CRYPTOLOOP is not set
# CONFIG\_BLK\_DEV\_NBD is not set
# CONFIG\_BLK\_DEV\_SX8 is not set
# CONFIG\_BLK\_DEV\_UB is not set
# CONFIG\_BLK\_DEV\_RAM is not set
# CONFIG\_BLK\_DEV\_INITRD is not set
# CONFIG\_CDROM\_PKTCDVD is not set
# CONFIG\_ATA\_OVER\_ETH is not set

#
# Misc devices
#
# CONFIG\_IBM\_ASM is not set
# CONFIG\_SGI\_IOC4 is not set
# CONFIG\_TIFM\_CORE is not set

#
# ATA/ATAPI/MFM/RLL support
#
CONFIG\_IDE=y
CONFIG\_BLK\_DEV\_IDE=y

#
# Please see Documentation/ide.txt for help/info on IDE drives
#
# CONFIG\_BLK\_DEV\_IDE\_SATA is not set
# CONFIG\_BLK\_DEV\_HD\_IDE is not set
CONFIG\_BLK\_DEV\_IDEDISK=y
# CONFIG\_IDEDISK\_MULTI\_MODE is not set
CONFIG\_BLK\_DEV\_IDECD=y
# CONFIG\_BLK\_DEV\_IDETAPE is not set
# CONFIG\_BLK\_DEV\_IDEFLOPPY is not set
# CONFIG\_BLK\_DEV\_IDESCSI is not set
# CONFIG\_IDE\_TASK\_IOCTL is not set

#
# IDE chipset support/bugfixes
#
# CONFIG\_IDE\_GENERIC is not set
# CONFIG\_BLK\_DEV\_CMD640 is not set
CONFIG\_BLK\_DEV\_IDEPCI=y
CONFIG\_IDEPCI\_SHARE\_IRQ=y
# CONFIG\_BLK\_DEV\_OFFBOARD is not set
# CONFIG\_BLK\_DEV\_GENERIC is not set
# CONFIG\_BLK\_DEV\_OPTI621 is not set
# CONFIG\_BLK\_DEV\_RZ1000 is not set
CONFIG\_BLK\_DEV\_IDEDMA\_PCI=y
# CONFIG\_BLK\_DEV\_IDEDMA\_FORCED is not set
CONFIG\_IDEDMA\_PCI\_AUTO=y
# CONFIG\_IDEDMA\_ONLYDISK is not set
# CONFIG\_BLK\_DEV\_AEC62XX is not set
# CONFIG\_BLK\_DEV\_ALI15X3 is not set
# CONFIG\_BLK\_DEV\_AMD74XX is not set
# CONFIG\_BLK\_DEV\_ATIIXP is not set
# CONFIG\_BLK\_DEV\_CMD64X is not set
# CONFIG\_BLK\_DEV\_TRIFLEX is not set
# CONFIG\_BLK\_DEV\_CY82C693 is not set
# CONFIG\_BLK\_DEV\_CS5520 is not set
# CONFIG\_BLK\_DEV\_CS5530 is not set
# CONFIG\_BLK\_DEV\_CS5535 is not set
# CONFIG\_BLK\_DEV\_HPT34X is not set
# CONFIG\_BLK\_DEV\_HPT366 is not set
# CONFIG\_BLK\_DEV\_JMICRON is not set
CONFIG\_BLK\_DEV\_SC1200=y
# CONFIG\_BLK\_DEV\_PIIX is not set
# CONFIG\_BLK\_DEV\_IT821X is not set
# CONFIG\_BLK\_DEV\_NS87415 is not set
# CONFIG\_BLK\_DEV\_PDC202XX\_OLD is not set
# CONFIG\_BLK\_DEV\_PDC202XX\_NEW is not set
# CONFIG\_BLK\_DEV\_SVWKS is not set
# CONFIG\_BLK\_DEV\_SIIMAGE is not set
# CONFIG\_BLK\_DEV\_SIS5513 is not set
# CONFIG\_BLK\_DEV\_SLC90E66 is not set
# CONFIG\_BLK\_DEV\_TRM290 is not set
CONFIG\_BLK\_DEV\_VIA82CXXX=y
# CONFIG\_IDE\_ARM is not set
# CONFIG\_IDE\_CHIPSETS is not set
CONFIG\_BLK\_DEV\_IDEDMA=y
# CONFIG\_IDEDMA\_IVB is not set
CONFIG\_IDEDMA\_AUTO=y
# CONFIG\_BLK\_DEV\_HD is not set

#
# SCSI device support
#
# CONFIG\_RAID\_ATTRS is not set
CONFIG\_SCSI=y
CONFIG\_SCSI\_TGT=m
# CONFIG\_SCSI\_NETLINK is not set
# CONFIG\_SCSI\_PROC\_FS is not set

#
# SCSI support type (disk, tape, CD-ROM)
#
CONFIG\_BLK\_DEV\_SD=y
# CONFIG\_CHR\_DEV\_ST is not set
# CONFIG\_CHR\_DEV\_OSST is not set
# CONFIG\_BLK\_DEV\_SR is not set
# CONFIG\_CHR\_DEV\_SG is not set
# CONFIG\_CHR\_DEV\_SCH is not set

#
# Some SCSI devices (e.g. CD jukebox) support multiple LUNs
#
# CONFIG\_SCSI\_MULTI\_LUN is not set
# CONFIG\_SCSI\_CONSTANTS is not set
# CONFIG\_SCSI\_LOGGING is not set
# CONFIG\_SCSI\_SCAN\_ASYNC is not set

#
# SCSI Transports
#
# CONFIG\_SCSI\_SPI\_ATTRS is not set
# CONFIG\_SCSI\_FC\_ATTRS is not set
# CONFIG\_SCSI\_ISCSI\_ATTRS is not set
# CONFIG\_SCSI\_SAS\_ATTRS is not set
# CONFIG\_SCSI\_SAS\_LIBSAS is not set

#
# SCSI low-level drivers
#
# CONFIG\_ISCSI\_TCP is not set
# CONFIG\_BLK\_DEV\_3W\_XXXX\_RAID is not set
# CONFIG\_SCSI\_3W\_9XXX is not set
# CONFIG\_SCSI\_7000FASST is not set
# CONFIG\_SCSI\_ACARD is not set
# CONFIG\_SCSI\_AHA152X is not set
# CONFIG\_SCSI\_AHA1542 is not set
# CONFIG\_SCSI\_AACRAID is not set
# CONFIG\_SCSI\_AIC7XXX is not set
# CONFIG\_SCSI\_AIC7XXX\_OLD is not set
# CONFIG\_SCSI\_AIC79XX is not set
# CONFIG\_SCSI\_AIC94XX is not set
# CONFIG\_SCSI\_DPT\_I2O is not set
# CONFIG\_SCSI\_ADVANSYS is not set
# CONFIG\_SCSI\_IN2000 is not set
# CONFIG\_SCSI\_ARCMSR is not set
# CONFIG\_MEGARAID\_NEWGEN is not set
# CONFIG\_MEGARAID\_LEGACY is not set
# CONFIG\_MEGARAID\_SAS is not set
# CONFIG\_SCSI\_HPTIOP is not set
# CONFIG\_SCSI\_BUSLOGIC is not set
# CONFIG\_SCSI\_DMX3191D is not set
# CONFIG\_SCSI\_DTC3280 is not set
# CONFIG\_SCSI\_EATA is not set
# CONFIG\_SCSI\_FUTURE\_DOMAIN is not set
# CONFIG\_SCSI\_GDTH is not set
# CONFIG\_SCSI\_GENERIC\_NCR5380 is not set
# CONFIG\_SCSI\_GENERIC\_NCR5380\_MMIO is not set
# CONFIG\_SCSI\_IPS is not set
# CONFIG\_SCSI\_INITIO is not set
# CONFIG\_SCSI\_INIA100 is not set
# CONFIG\_SCSI\_PPA is not set
# CONFIG\_SCSI\_IMM is not set
# CONFIG\_SCSI\_NCR53C406A is not set
# CONFIG\_SCSI\_STEX is not set
# CONFIG\_SCSI\_SYM53C8XX\_2 is not set
# CONFIG\_SCSI\_IPR is not set
# CONFIG\_SCSI\_PAS16 is not set
# CONFIG\_SCSI\_PSI240I is not set
# CONFIG\_SCSI\_QLOGIC\_FAS is not set
# CONFIG\_SCSI\_QLOGIC\_1280 is not set
# CONFIG\_SCSI\_QLA\_FC is not set
# CONFIG\_SCSI\_QLA\_ISCSI is not set
# CONFIG\_SCSI\_LPFC is not set
# CONFIG\_SCSI\_SEAGATE is not set
# CONFIG\_SCSI\_SYM53C416 is not set
# CONFIG\_SCSI\_DC395x is not set
# CONFIG\_SCSI\_DC390T is not set
# CONFIG\_SCSI\_T128 is not set
# CONFIG\_SCSI\_U14\_34F is not set
# CONFIG\_SCSI\_ULTRASTOR is not set
# CONFIG\_SCSI\_NSP32 is not set
# CONFIG\_SCSI\_DEBUG is not set
# CONFIG\_SCSI\_SRP is not set

#
# Serial ATA (prod) and Parallel ATA (experimental) drivers
#
CONFIG\_ATA=m
# CONFIG\_ATA\_NONSTANDARD is not set
# CONFIG\_SATA\_AHCI is not set
# CONFIG\_SATA\_SVW is not set
# CONFIG\_ATA\_PIIX is not set
# CONFIG\_SATA\_MV is not set
# CONFIG\_SATA\_NV is not set
# CONFIG\_PDC\_ADMA is not set
# CONFIG\_SATA\_QSTOR is not set
# CONFIG\_SATA\_PROMISE is not set
# CONFIG\_SATA\_SX4 is not set
# CONFIG\_SATA\_SIL is not set
# CONFIG\_SATA\_SIL24 is not set
# CONFIG\_SATA\_SIS is not set
# CONFIG\_SATA\_ULI is not set
# CONFIG\_SATA\_VIA is not set
# CONFIG\_SATA\_VITESSE is not set
# CONFIG\_PATA\_ALI is not set
# CONFIG\_PATA\_AMD is not set
# CONFIG\_PATA\_ARTOP is not set
# CONFIG\_PATA\_ATIIXP is not set
# CONFIG\_PATA\_CMD64X is not set
# CONFIG\_PATA\_CS5520 is not set
# CONFIG\_PATA\_CS5530 is not set
# CONFIG\_PATA\_CS5535 is not set
# CONFIG\_PATA\_CYPRESS is not set
# CONFIG\_PATA\_EFAR is not set
# CONFIG\_ATA\_GENERIC is not set
# CONFIG\_PATA\_HPT366 is not set
# CONFIG\_PATA\_HPT37X is not set
# CONFIG\_PATA\_HPT3X2N is not set
# CONFIG\_PATA\_HPT3X3 is not set
# CONFIG\_PATA\_IT821X is not set
# CONFIG\_PATA\_JMICRON is not set
# CONFIG\_PATA\_LEGACY is not set
# CONFIG\_PATA\_TRIFLEX is not set
# CONFIG\_PATA\_MARVELL is not set
# CONFIG\_PATA\_MPIIX is not set
# CONFIG\_PATA\_OLDPIIX is not set
# CONFIG\_PATA\_NETCELL is not set
# CONFIG\_PATA\_NS87410 is not set
# CONFIG\_PATA\_OPTI is not set
# CONFIG\_PATA\_OPTIDMA is not set
# CONFIG\_PATA\_PDC\_OLD is not set
# CONFIG\_PATA\_QDI is not set
# CONFIG\_PATA\_RADISYS is not set
# CONFIG\_PATA\_RZ1000 is not set
CONFIG\_PATA\_SC1200=m
# CONFIG\_PATA\_SERVERWORKS is not set
# CONFIG\_PATA\_PDC2027X is not set
# CONFIG\_PATA\_SIL680 is not set
# CONFIG\_PATA\_SIS is not set
# CONFIG\_PATA\_VIA is not set
# CONFIG\_PATA\_WINBOND is not set
# CONFIG\_PATA\_WINBOND\_VLB is not set

#
# Old CD-ROM drivers (not SCSI, not IDE)
#
# CONFIG\_CD\_NO\_IDESCSI is not set

#
# Multi-device support (RAID and LVM)
#
# CONFIG\_MD is not set

#
# Fusion MPT device support
#
# CONFIG\_FUSION is not set
# CONFIG\_FUSION\_SPI is not set
# CONFIG\_FUSION\_FC is not set
# CONFIG\_FUSION\_SAS is not set

#
# IEEE 1394 (FireWire) support
#
# CONFIG\_IEEE1394 is not set

#
# I2O device support
#
# CONFIG\_I2O is not set

#
# Macintosh device drivers
#
# CONFIG\_MAC\_EMUMOUSEBTN is not set

#
# Network device support
#
CONFIG\_NETDEVICES=y
# CONFIG\_DUMMY is not set
# CONFIG\_BONDING is not set
# CONFIG\_EQUALIZER is not set
# CONFIG\_TUN is not set

#
# ARCnet devices
#
# CONFIG\_ARCNET is not set

#
# PHY device support
#
# CONFIG\_PHYLIB is not set

#
# Ethernet (10 or 100Mbit)
#
CONFIG\_NET\_ETHERNET=y
CONFIG\_MII=y
# CONFIG\_HAPPYMEAL is not set
# CONFIG\_SUNGEM is not set
# CONFIG\_CASSINI is not set
# CONFIG\_NET\_VENDOR\_3COM is not set
# CONFIG\_LANCE is not set
# CONFIG\_NET\_VENDOR\_SMC is not set
# CONFIG\_NET\_VENDOR\_RACAL is not set

#
# Tulip family network device support
#
# CONFIG\_NET\_TULIP is not set
# CONFIG\_AT1700 is not set
# CONFIG\_DEPCA is not set
# CONFIG\_HP100 is not set
# CONFIG\_NET\_ISA is not set
CONFIG\_NET\_PCI=y
# CONFIG\_PCNET32 is not set
# CONFIG\_AMD8111\_ETH is not set
# CONFIG\_ADAPTEC\_STARFIRE is not set
# CONFIG\_AC3200 is not set
# CONFIG\_APRICOT is not set
# CONFIG\_B44 is not set
# CONFIG\_FORCEDETH is not set
# CONFIG\_CS89x0 is not set
# CONFIG\_DGRS is not set
# CONFIG\_EEPRO100 is not set
CONFIG\_E100=y
# CONFIG\_FEALNX is not set
CONFIG\_NATSEMI=y
# CONFIG\_NE2K\_PCI is not set
# CONFIG\_8139CP is not set
# CONFIG\_8139TOO is not set
# CONFIG\_SIS900 is not set
# CONFIG\_EPIC100 is not set
# CONFIG\_SUNDANCE is not set
# CONFIG\_TLAN is not set
# CONFIG\_VIA\_RHINE is not set
# CONFIG\_NET\_POCKET is not set

#
# Ethernet (1000 Mbit)
#
# CONFIG\_ACENIC is not set
# CONFIG\_DL2K is not set
# CONFIG\_E1000 is not set
# CONFIG\_NS83820 is not set
# CONFIG\_HAMACHI is not set
# CONFIG\_YELLOWFIN is not set
# CONFIG\_R8169 is not set
# CONFIG\_SIS190 is not set
# CONFIG\_SKGE is not set
# CONFIG\_SKY2 is not set
# CONFIG\_SK98LIN is not set
# CONFIG\_VIA\_VELOCITY is not set
# CONFIG\_TIGON3 is not set
# CONFIG\_BNX2 is not set
# CONFIG\_QLA3XXX is not set

#
# Ethernet (10000 Mbit)
#
# CONFIG\_CHELSIO\_T1 is not set
# CONFIG\_IXGB is not set
# CONFIG\_S2IO is not set
# CONFIG\_MYRI10GE is not set
# CONFIG\_NETXEN\_NIC is not set

#
# Token Ring devices
#
# CONFIG\_TR is not set

#
# Wireless LAN (non-hamradio)
#
# CONFIG\_NET\_RADIO is not set

#
# Wan interfaces
#
# CONFIG\_WAN is not set
# CONFIG\_FDDI is not set
# CONFIG\_HIPPI is not set
# CONFIG\_PLIP is not set
# CONFIG\_PPP is not set
# CONFIG\_SLIP is not set
# CONFIG\_NET\_FC is not set
# CONFIG\_SHAPER is not set
# CONFIG\_NETCONSOLE is not set
# CONFIG\_NETPOLL is not set
# CONFIG\_NET\_POLL\_CONTROLLER is not set

#
# ISDN subsystem
#
# CONFIG\_ISDN is not set

#
# Telephony Support
#
# CONFIG\_PHONE is not set

#
# Input device support
#
CONFIG\_INPUT=y
# CONFIG\_INPUT\_FF\_MEMLESS is not set

#
# Userland interfaces
#
CONFIG\_INPUT\_MOUSEDEV=y
CONFIG\_INPUT\_MOUSEDEV\_PSAUX=y
CONFIG\_INPUT\_MOUSEDEV\_SCREEN\_X=1280
CONFIG\_INPUT\_MOUSEDEV\_SCREEN\_Y=1024
# CONFIG\_INPUT\_JOYDEV is not set
# CONFIG\_INPUT\_TSDEV is not set
CONFIG\_INPUT\_EVDEV=y
# CONFIG\_INPUT\_EVBUG is not set

#
# Input Device Drivers
#
CONFIG\_INPUT\_KEYBOARD=y
CONFIG\_KEYBOARD\_ATKBD=y
# CONFIG\_KEYBOARD\_SUNKBD is not set
# CONFIG\_KEYBOARD\_LKKBD is not set
# CONFIG\_KEYBOARD\_XTKBD is not set
# CONFIG\_KEYBOARD\_NEWTON is not set
# CONFIG\_KEYBOARD\_STOWAWAY is not set
CONFIG\_INPUT\_MOUSE=y
CONFIG\_MOUSE\_PS2=y
# CONFIG\_MOUSE\_SERIAL is not set
# CONFIG\_MOUSE\_INPORT is not set
# CONFIG\_MOUSE\_LOGIBM is not set
# CONFIG\_MOUSE\_PC110PAD is not set
# CONFIG\_MOUSE\_VSXXXAA is not set
# CONFIG\_INPUT\_JOYSTICK is not set
# CONFIG\_INPUT\_TOUCHSCREEN is not set
# CONFIG\_INPUT\_MISC is not set

#
# Hardware I/O ports
#
CONFIG\_SERIO=y
CONFIG\_SERIO\_I8042=y
# CONFIG\_SERIO\_SERPORT is not set
# CONFIG\_SERIO\_CT82C710 is not set
# CONFIG\_SERIO\_PARKBD is not set
# CONFIG\_SERIO\_PCIPS2 is not set
CONFIG\_SERIO\_LIBPS2=y
# CONFIG\_SERIO\_RAW is not set
# CONFIG\_GAMEPORT is not set

#
# Character devices
#
CONFIG\_VT=y
CONFIG\_VT\_CONSOLE=y
CONFIG\_HW\_CONSOLE=y
CONFIG\_VT\_HW\_CONSOLE\_BINDING=y
# CONFIG\_SERIAL\_NONSTANDARD is not set

#
# Serial drivers
#
CONFIG\_SERIAL\_8250=y
CONFIG\_SERIAL\_8250\_CONSOLE=y
CONFIG\_SERIAL\_8250\_PCI=y
CONFIG\_SERIAL\_8250\_NR\_UARTS=2
CONFIG\_SERIAL\_8250\_RUNTIME\_UARTS=2
# CONFIG\_SERIAL\_8250\_EXTENDED is not set

#
# Non-8250 serial port support
#
CONFIG\_SERIAL\_CORE=y
CONFIG\_SERIAL\_CORE\_CONSOLE=y
# CONFIG\_SERIAL\_JSM is not set
CONFIG\_UNIX98\_PTYS=y
CONFIG\_LEGACY\_PTYS=y
CONFIG\_LEGACY\_PTY\_COUNT=256
CONFIG\_PRINTER=y
# CONFIG\_LP\_CONSOLE is not set
# CONFIG\_PPDEV is not set
# CONFIG\_TIPAR is not set

#
# IPMI
#
# CONFIG\_IPMI\_HANDLER is not set

#
# Watchdog Cards
#
CONFIG\_WATCHDOG=y
# CONFIG\_WATCHDOG\_NOWAYOUT is not set

#
# Watchdog Device Drivers
#
# CONFIG\_SOFT\_WATCHDOG is not set
# CONFIG\_ACQUIRE\_WDT is not set
# CONFIG\_ADVANTECH\_WDT is not set
# CONFIG\_ALIM1535\_WDT is not set
# CONFIG\_ALIM7101\_WDT is not set
# CONFIG\_SC520\_WDT is not set
# CONFIG\_EUROTECH\_WDT is not set
# CONFIG\_IB700\_WDT is not set
# CONFIG\_IBMASR is not set
# CONFIG\_WAFER\_WDT is not set
# CONFIG\_I6300ESB\_WDT is not set
# CONFIG\_I8XX\_TCO is not set
# CONFIG\_ITCO\_WDT is not set
# CONFIG\_SC1200\_WDT is not set
CONFIG\_SCx200\_WDT=m
# CONFIG\_PC87413\_WDT is not set
# CONFIG\_60XX\_WDT is not set
# CONFIG\_SBC8360\_WDT is not set
# CONFIG\_CPU5\_WDT is not set
# CONFIG\_SMSC37B787\_WDT is not set
# CONFIG\_W83627HF\_WDT is not set
# CONFIG\_W83697HF\_WDT is not set
# CONFIG\_W83877F\_WDT is not set
# CONFIG\_W83977F\_WDT is not set
# CONFIG\_MACHZ\_WDT is not set
# CONFIG\_SBC\_EPX\_C3\_WATCHDOG is not set

#
# ISA-based Watchdog Cards
#
# CONFIG\_PCWATCHDOG is not set
# CONFIG\_MIXCOMWD is not set
# CONFIG\_WDT is not set

#
# PCI-based Watchdog Cards
#
# CONFIG\_PCIPCWATCHDOG is not set
# CONFIG\_WDTPCI is not set

#
# USB-based Watchdog Cards
#
# CONFIG\_USBPCWATCHDOG is not set
# CONFIG\_HW\_RANDOM is not set
CONFIG\_NVRAM=y
CONFIG\_RTC=y
# CONFIG\_DTLK is not set
# CONFIG\_R3964 is not set
# CONFIG\_APPLICOM is not set
# CONFIG\_SONYPI is not set
CONFIG\_AGP=y
# CONFIG\_AGP\_ALI is not set
# CONFIG\_AGP\_ATI is not set
# CONFIG\_AGP\_AMD is not set
# CONFIG\_AGP\_AMD64 is not set
# CONFIG\_AGP\_INTEL is not set
# CONFIG\_AGP\_NVIDIA is not set
# CONFIG\_AGP\_SIS is not set
# CONFIG\_AGP\_SWORKS is not set
CONFIG\_AGP\_VIA=y
# CONFIG\_AGP\_EFFICEON is not set
CONFIG\_DRM=y
# CONFIG\_DRM\_TDFX is not set
# CONFIG\_DRM\_R128 is not set
CONFIG\_DRM\_RADEON=y
# CONFIG\_DRM\_MGA is not set
# CONFIG\_DRM\_SIS is not set
# CONFIG\_DRM\_VIA is not set
# CONFIG\_DRM\_SAVAGE is not set
# CONFIG\_MWAVE is not set
CONFIG\_SCx200\_GPIO=m
CONFIG\_PC8736x\_GPIO=m
CONFIG\_NSC\_GPIO=m
# CONFIG\_CS5535\_GPIO is not set
# CONFIG\_RAW\_DRIVER is not set
# CONFIG\_HPET is not set
# CONFIG\_HANGCHECK\_TIMER is not set

#
# TPM devices
#
# CONFIG\_TCG\_TPM is not set
# CONFIG\_TELCLOCK is not set

#
# I2C support
#
CONFIG\_I2C=y
CONFIG\_I2C\_CHARDEV=y

#
# I2C Algorithms
#
CONFIG\_I2C\_ALGOBIT=y
# CONFIG\_I2C\_ALGOPCF is not set
# CONFIG\_I2C\_ALGOPCA is not set

#
# I2C Hardware Bus support
#
# CONFIG\_I2C\_ALI1535 is not set
# CONFIG\_I2C\_ALI1563 is not set
# CONFIG\_I2C\_ALI15X3 is not set
# CONFIG\_I2C\_AMD756 is not set
# CONFIG\_I2C\_AMD8111 is not set
# CONFIG\_I2C\_ELEKTOR is not set
# CONFIG\_I2C\_I801 is not set
# CONFIG\_I2C\_I810 is not set
# CONFIG\_I2C\_PIIX4 is not set
CONFIG\_I2C\_ISA=y
# CONFIG\_I2C\_NFORCE2 is not set
# CONFIG\_I2C\_OCORES is not set
# CONFIG\_I2C\_PARPORT is not set
# CONFIG\_I2C\_PARPORT\_LIGHT is not set
# CONFIG\_I2C\_PROSAVAGE is not set
# CONFIG\_I2C\_SAVAGE4 is not set
CONFIG\_SCx200\_I2C=m
CONFIG\_SCx200\_I2C\_SCL=12
CONFIG\_SCx200\_I2C\_SDA=13
# CONFIG\_SCx200\_ACB is not set
# CONFIG\_I2C\_SIS5595 is not set
# CONFIG\_I2C\_SIS630 is not set
# CONFIG\_I2C\_SIS96X is not set
# CONFIG\_I2C\_STUB is not set
# CONFIG\_I2C\_VIA is not set
CONFIG\_I2C\_VIAPRO=y
# CONFIG\_I2C\_VOODOO3 is not set
# CONFIG\_I2C\_PCA\_ISA is not set

#
# Miscellaneous I2C Chip support
#
# CONFIG\_SENSORS\_DS1337 is not set
# CONFIG\_SENSORS\_DS1374 is not set
# CONFIG\_SENSORS\_EEPROM is not set
# CONFIG\_SENSORS\_PCF8574 is not set
# CONFIG\_SENSORS\_PCA9539 is not set
# CONFIG\_SENSORS\_PCF8591 is not set
# CONFIG\_SENSORS\_MAX6875 is not set
# CONFIG\_I2C\_DEBUG\_CORE is not set
# CONFIG\_I2C\_DEBUG\_ALGO is not set
# CONFIG\_I2C\_DEBUG\_BUS is not set
# CONFIG\_I2C\_DEBUG\_CHIP is not set

#
# SPI support
#
# CONFIG\_SPI is not set
# CONFIG\_SPI\_MASTER is not set

#
# Dallas's 1-wire bus
#
# CONFIG\_W1 is not set

#
# Hardware Monitoring support
#
CONFIG\_HWMON=y
CONFIG\_HWMON\_VID=y
# CONFIG\_SENSORS\_ABITUGURU is not set
# CONFIG\_SENSORS\_ADM1021 is not set
# CONFIG\_SENSORS\_ADM1025 is not set
# CONFIG\_SENSORS\_ADM1026 is not set
# CONFIG\_SENSORS\_ADM1031 is not set
# CONFIG\_SENSORS\_ADM9240 is not set
# CONFIG\_SENSORS\_K8TEMP is not set
# CONFIG\_SENSORS\_ASB100 is not set
# CONFIG\_SENSORS\_ATXP1 is not set
# CONFIG\_SENSORS\_DS1621 is not set
# CONFIG\_SENSORS\_F71805F is not set
# CONFIG\_SENSORS\_FSCHER is not set
# CONFIG\_SENSORS\_FSCPOS is not set
# CONFIG\_SENSORS\_GL518SM is not set
# CONFIG\_SENSORS\_GL520SM is not set
CONFIG\_SENSORS\_IT87=y
# CONFIG\_SENSORS\_LM63 is not set
# CONFIG\_SENSORS\_LM75 is not set
# CONFIG\_SENSORS\_LM77 is not set
# CONFIG\_SENSORS\_LM78 is not set
# CONFIG\_SENSORS\_LM80 is not set
# CONFIG\_SENSORS\_LM83 is not set
# CONFIG\_SENSORS\_LM85 is not set
# CONFIG\_SENSORS\_LM87 is not set
# CONFIG\_SENSORS\_LM90 is not set
# CONFIG\_SENSORS\_LM92 is not set
# CONFIG\_SENSORS\_MAX1619 is not set
CONFIG\_SENSORS\_PC87360=m
# CONFIG\_SENSORS\_PC87427 is not set
# CONFIG\_SENSORS\_SIS5595 is not set
# CONFIG\_SENSORS\_SMSC47M1 is not set
# CONFIG\_SENSORS\_SMSC47M192 is not set
# CONFIG\_SENSORS\_SMSC47B397 is not set
# CONFIG\_SENSORS\_VIA686A is not set
# CONFIG\_SENSORS\_VT1211 is not set
# CONFIG\_SENSORS\_VT8231 is not set
# CONFIG\_SENSORS\_W83781D is not set
# CONFIG\_SENSORS\_W83791D is not set
# CONFIG\_SENSORS\_W83792D is not set
# CONFIG\_SENSORS\_W83793 is not set
# CONFIG\_SENSORS\_W83L785TS is not set
# CONFIG\_SENSORS\_W83627HF is not set
# CONFIG\_SENSORS\_W83627EHF is not set
# CONFIG\_SENSORS\_HDAPS is not set
# CONFIG\_HWMON\_DEBUG\_CHIP is not set

#
# Multimedia devices
#
CONFIG\_VIDEO\_DEV=y
CONFIG\_VIDEO\_V4L1=y
CONFIG\_VIDEO\_V4L1\_COMPAT=y
CONFIG\_VIDEO\_V4L2=y

#
# Video Capture Adapters
#

#
# Video Capture Adapters
#
# CONFIG\_VIDEO\_ADV\_DEBUG is not set
# CONFIG\_VIDEO\_HELPER\_CHIPS\_AUTO is not set

#
# Encoders/decoders and other helper chips
#

#
# Audio decoders
#
# CONFIG\_VIDEO\_TVAUDIO is not set
# CONFIG\_VIDEO\_TDA7432 is not set
# CONFIG\_VIDEO\_TDA9840 is not set
# CONFIG\_VIDEO\_TDA9875 is not set
# CONFIG\_VIDEO\_TEA6415C is not set
# CONFIG\_VIDEO\_TEA6420 is not set
# CONFIG\_VIDEO\_MSP3400 is not set
# CONFIG\_VIDEO\_CS53L32A is not set
# CONFIG\_VIDEO\_TLV320AIC23B is not set
# CONFIG\_VIDEO\_WM8775 is not set
# CONFIG\_VIDEO\_WM8739 is not set

#
# Video decoders
#
# CONFIG\_VIDEO\_BT819 is not set
# CONFIG\_VIDEO\_BT856 is not set
# CONFIG\_VIDEO\_BT866 is not set
# CONFIG\_VIDEO\_KS0127 is not set
# CONFIG\_VIDEO\_OV7670 is not set
# CONFIG\_VIDEO\_SAA7110 is not set
# CONFIG\_VIDEO\_SAA7111 is not set
# CONFIG\_VIDEO\_SAA7114 is not set
# CONFIG\_VIDEO\_SAA711X is not set
# CONFIG\_VIDEO\_SAA7191 is not set
# CONFIG\_VIDEO\_TVP5150 is not set
# CONFIG\_VIDEO\_VPX3220 is not set

#
# Video and audio decoders
#
# CONFIG\_VIDEO\_CX25840 is not set

#
# MPEG video encoders
#
# CONFIG\_VIDEO\_CX2341X is not set

#
# Video encoders
#
# CONFIG\_VIDEO\_SAA7127 is not set
# CONFIG\_VIDEO\_SAA7185 is not set
# CONFIG\_VIDEO\_ADV7170 is not set
# CONFIG\_VIDEO\_ADV7175 is not set

#
# Video improvement chips
#
# CONFIG\_VIDEO\_UPD64031A is not set
# CONFIG\_VIDEO\_UPD64083 is not set
# CONFIG\_VIDEO\_VIVI is not set
# CONFIG\_VIDEO\_BT848 is not set
# CONFIG\_VIDEO\_PMS is not set
# CONFIG\_VIDEO\_BWQCAM is not set
# CONFIG\_VIDEO\_CQCAM is not set
# CONFIG\_VIDEO\_W9966 is not set
# CONFIG\_VIDEO\_CPIA is not set
# CONFIG\_VIDEO\_CPIA2 is not set
# CONFIG\_VIDEO\_SAA5246A is not set
# CONFIG\_VIDEO\_SAA5249 is not set
# CONFIG\_TUNER\_3036 is not set
# CONFIG\_VIDEO\_STRADIS is not set
# CONFIG\_VIDEO\_ZORAN is not set
CONFIG\_VIDEO\_SAA7134=y
# CONFIG\_VIDEO\_MXB is not set
# CONFIG\_VIDEO\_DPC is not set
# CONFIG\_VIDEO\_HEXIUM\_ORION is not set
# CONFIG\_VIDEO\_HEXIUM\_GEMINI is not set
# CONFIG\_VIDEO\_CX88 is not set
# CONFIG\_VIDEO\_CAFE\_CCIC is not set

#
# V4L USB devices
#
# CONFIG\_VIDEO\_PVRUSB2 is not set
# CONFIG\_VIDEO\_EM28XX is not set
# CONFIG\_VIDEO\_USBVISION is not set
# CONFIG\_USB\_VICAM is not set
# CONFIG\_USB\_IBMCAM is not set
# CONFIG\_USB\_KONICAWC is not set
# CONFIG\_USB\_QUICKCAM\_MESSENGER is not set
# CONFIG\_USB\_ET61X251 is not set
# CONFIG\_VIDEO\_OVCAMCHIP is not set
# CONFIG\_USB\_W9968CF is not set
# CONFIG\_USB\_OV511 is not set
# CONFIG\_USB\_SE401 is not set
# CONFIG\_USB\_SN9C102 is not set
# CONFIG\_USB\_STV680 is not set
# CONFIG\_USB\_ZC0301 is not set
# CONFIG\_USB\_PWC is not set

#
# Radio Adapters
#
# CONFIG\_RADIO\_CADET is not set
# CONFIG\_RADIO\_RTRACK is not set
# CONFIG\_RADIO\_RTRACK2 is not set
# CONFIG\_RADIO\_AZTECH is not set
# CONFIG\_RADIO\_GEMTEK is not set
# CONFIG\_RADIO\_GEMTEK\_PCI is not set
# CONFIG\_RADIO\_MAXIRADIO is not set
# CONFIG\_RADIO\_MAESTRO is not set
# CONFIG\_RADIO\_SF16FMI is not set
# CONFIG\_RADIO\_SF16FMR2 is not set
# CONFIG\_RADIO\_TERRATEC is not set
# CONFIG\_RADIO\_TRUST is not set
# CONFIG\_RADIO\_TYPHOON is not set
# CONFIG\_RADIO\_ZOLTRIX is not set
# CONFIG\_USB\_DSBR is not set

#
# Digital Video Broadcasting Devices
#
# CONFIG\_DVB is not set
CONFIG\_VIDEO\_TUNER=y
CONFIG\_VIDEO\_BUF=y
CONFIG\_VIDEO\_IR=y
# CONFIG\_USB\_DABUSB is not set

#
# Graphics support
#
# CONFIG\_FIRMWARE\_EDID is not set
CONFIG\_FB=y
CONFIG\_FB\_DDC=y
CONFIG\_FB\_CFB\_FILLRECT=y
CONFIG\_FB\_CFB\_COPYAREA=y
CONFIG\_FB\_CFB\_IMAGEBLIT=y
# CONFIG\_FB\_MACMODES is not set
# CONFIG\_FB\_BACKLIGHT is not set
CONFIG\_FB\_MODE\_HELPERS=y
# CONFIG\_FB\_TILEBLITTING is not set
# CONFIG\_FB\_CIRRUS is not set
# CONFIG\_FB\_PM2 is not set
# CONFIG\_FB\_CYBER2000 is not set
# CONFIG\_FB\_ARC is not set
# CONFIG\_FB\_ASILIANT is not set
# CONFIG\_FB\_IMSTT is not set
# CONFIG\_FB\_VGA16 is not set
# CONFIG\_FB\_VESA is not set
CONFIG\_VIDEO\_SELECT=y
# CONFIG\_FB\_HGA is not set
# CONFIG\_FB\_S1D13XXX is not set
# CONFIG\_FB\_NVIDIA is not set
# CONFIG\_FB\_RIVA is not set
# CONFIG\_FB\_I810 is not set
# CONFIG\_FB\_INTEL is not set
# CONFIG\_FB\_MATROX is not set
CONFIG\_FB\_RADEON=y
CONFIG\_FB\_RADEON\_I2C=y
# CONFIG\_FB\_RADEON\_DEBUG is not set
# CONFIG\_FB\_ATY128 is not set
# CONFIG\_FB\_ATY is not set
# CONFIG\_FB\_SAVAGE is not set
# CONFIG\_FB\_SIS is not set
# CONFIG\_FB\_NEOMAGIC is not set
# CONFIG\_FB\_KYRO is not set
# CONFIG\_FB\_3DFX is not set
# CONFIG\_FB\_VOODOO1 is not set
# CONFIG\_FB\_CYBLA is not set
# CONFIG\_FB\_TRIDENT is not set
# CONFIG\_FB\_GEODE is not set
# CONFIG\_FB\_VIRTUAL is not set

#
# Console display driver support
#
CONFIG\_VGA\_CONSOLE=y
# CONFIG\_VGACON\_SOFT\_SCROLLBACK is not set
# CONFIG\_MDA\_CONSOLE is not set
CONFIG\_DUMMY\_CONSOLE=y
CONFIG\_FRAMEBUFFER\_CONSOLE=y
# CONFIG\_FRAMEBUFFER\_CONSOLE\_ROTATION is not set
# CONFIG\_FONTS is not set
CONFIG\_FONT\_8x8=y
CONFIG\_FONT\_8x16=y

#
# Logo configuration
#
# CONFIG\_LOGO is not set
# CONFIG\_BACKLIGHT\_LCD\_SUPPORT is not set
# CONFIG\_FB\_SPLASH is not set

#
# Speakup console speech
#
# CONFIG\_SPEAKUP is not set

#
# Sound
#
# CONFIG\_SOUND is not set

#
# HID Devices
#
CONFIG\_HID=y

#
# USB support
#
CONFIG\_USB\_ARCH\_HAS\_HCD=y
CONFIG\_USB\_ARCH\_HAS\_OHCI=y
CONFIG\_USB\_ARCH\_HAS\_EHCI=y
CONFIG\_USB=y
# CONFIG\_USB\_DEBUG is not set

#
# Miscellaneous USB options
#
CONFIG\_USB\_DEVICEFS=y
# CONFIG\_USB\_BANDWIDTH is not set
# CONFIG\_USB\_DYNAMIC\_MINORS is not set
# CONFIG\_USB\_SUSPEND is not set
# CONFIG\_USB\_OTG is not set

#
# USB Host Controller Drivers
#
CONFIG\_USB\_EHCI\_HCD=m
# CONFIG\_USB\_EHCI\_SPLIT\_ISO is not set
# CONFIG\_USB\_EHCI\_ROOT\_HUB\_TT is not set
# CONFIG\_USB\_EHCI\_TT\_NEWSCHED is not set
# CONFIG\_USB\_ISP116X\_HCD is not set
CONFIG\_USB\_OHCI\_HCD=y
# CONFIG\_USB\_OHCI\_BIG\_ENDIAN is not set
CONFIG\_USB\_OHCI\_LITTLE\_ENDIAN=y
# CONFIG\_USB\_UHCI\_HCD is not set
# CONFIG\_USB\_SL811\_HCD is not set

#
# USB Device Class drivers
#
CONFIG\_USB\_ACM=m
# CONFIG\_USB\_PRINTER is not set

#
# NOTE: USB\_STORAGE enables SCSI, and 'SCSI disk support'
#

#
# may also be needed; see USB\_STORAGE Help for more information
#
CONFIG\_USB\_STORAGE=y
# CONFIG\_USB\_STORAGE\_DEBUG is not set
# CONFIG\_USB\_STORAGE\_DATAFAB is not set
# CONFIG\_USB\_STORAGE\_FREECOM is not set
# CONFIG\_USB\_STORAGE\_ISD200 is not set
# CONFIG\_USB\_STORAGE\_DPCM is not set
# CONFIG\_USB\_STORAGE\_USBAT is not set
# CONFIG\_USB\_STORAGE\_SDDR09 is not set
# CONFIG\_USB\_STORAGE\_SDDR55 is not set
# CONFIG\_USB\_STORAGE\_JUMPSHOT is not set
# CONFIG\_USB\_STORAGE\_ALAUDA is not set
# CONFIG\_USB\_STORAGE\_KARMA is not set
# CONFIG\_USB\_LIBUSUAL is not set

#
# USB Input Devices
#
CONFIG\_USB\_HID=m
# CONFIG\_USB\_HIDINPUT\_POWERBOOK is not set
# CONFIG\_HID\_FF is not set
# CONFIG\_USB\_HIDDEV is not set

#
# USB HID Boot Protocol drivers
#
# CONFIG\_USB\_KBD is not set
# CONFIG\_USB\_MOUSE is not set
# CONFIG\_USB\_AIPTEK is not set
# CONFIG\_USB\_WACOM is not set
# CONFIG\_USB\_ACECAD is not set
# CONFIG\_USB\_KBTAB is not set
# CONFIG\_USB\_POWERMATE is not set
# CONFIG\_USB\_TOUCHSCREEN is not set
# CONFIG\_USB\_YEALINK is not set
# CONFIG\_USB\_XPAD is not set
# CONFIG\_USB\_ATI\_REMOTE is not set
# CONFIG\_USB\_ATI\_REMOTE2 is not set
# CONFIG\_USB\_KEYSPAN\_REMOTE is not set
# CONFIG\_USB\_APPLETOUCH is not set

#
# USB Imaging devices
#
# CONFIG\_USB\_MDC800 is not set
# CONFIG\_USB\_MICROTEK is not set

#
# USB Network Adapters
#
# CONFIG\_USB\_CATC is not set
# CONFIG\_USB\_KAWETH is not set
# CONFIG\_USB\_PEGASUS is not set
# CONFIG\_USB\_RTL8150 is not set
# CONFIG\_USB\_USBNET\_MII is not set
# CONFIG\_USB\_USBNET is not set
# CONFIG\_USB\_MON is not set

#
# USB port drivers
#
# CONFIG\_USB\_USS720 is not set

#
# USB Serial Converter support
#
# CONFIG\_USB\_SERIAL is not set

#
# USB Miscellaneous drivers
#
# CONFIG\_USB\_EMI62 is not set
# CONFIG\_USB\_EMI26 is not set
# CONFIG\_USB\_ADUTUX is not set
# CONFIG\_USB\_AUERSWALD is not set
# CONFIG\_USB\_RIO500 is not set
# CONFIG\_USB\_LEGOTOWER is not set
# CONFIG\_USB\_LCD is not set
# CONFIG\_USB\_LED is not set
# CONFIG\_USB\_CYPRESS\_CY7C63 is not set
# CONFIG\_USB\_CYTHERM is not set
# CONFIG\_USB\_PHIDGET is not set
# CONFIG\_USB\_IDMOUSE is not set
# CONFIG\_USB\_FTDI\_ELAN is not set
# CONFIG\_USB\_APPLEDISPLAY is not set
# CONFIG\_USB\_SISUSBVGA is not set
# CONFIG\_USB\_LD is not set
# CONFIG\_USB\_TRANCEVIBRATOR is not set
# CONFIG\_USB\_TEST is not set

#
# USB DSL modem support
#

#
# USB Gadget Support
#
# CONFIG\_USB\_GADGET is not set

#
# MMC/SD Card support
#
# CONFIG\_MMC is not set

#
# LED devices
#
CONFIG\_NEW\_LEDS=y
# CONFIG\_LEDS\_CLASS is not set

#
# LED drivers
#

#
# LED Triggers
#
# CONFIG\_LEDS\_TRIGGERS is not set

#
# InfiniBand support
#
# CONFIG\_INFINIBAND is not set

#
# EDAC - error detection and reporting (RAS) (EXPERIMENTAL)
#
# CONFIG\_EDAC is not set

#
# Real Time Clock
#
CONFIG\_RTC\_LIB=m
CONFIG\_RTC\_CLASS=m

#
# RTC interfaces
#
CONFIG\_RTC\_INTF\_SYSFS=m
CONFIG\_RTC\_INTF\_PROC=m
CONFIG\_RTC\_INTF\_DEV=m
# CONFIG\_RTC\_INTF\_DEV\_UIE\_EMUL is not set

#
# RTC drivers
#
# CONFIG\_RTC\_DRV\_X1205 is not set
# CONFIG\_RTC\_DRV\_DS1307 is not set
# CONFIG\_RTC\_DRV\_DS1553 is not set
# CONFIG\_RTC\_DRV\_ISL1208 is not set
# CONFIG\_RTC\_DRV\_DS1672 is not set
# CONFIG\_RTC\_DRV\_DS1742 is not set
# CONFIG\_RTC\_DRV\_PCF8563 is not set
# CONFIG\_RTC\_DRV\_PCF8583 is not set
# CONFIG\_RTC\_DRV\_RS5C372 is not set
# CONFIG\_RTC\_DRV\_M48T86 is not set
# CONFIG\_RTC\_DRV\_TEST is not set
# CONFIG\_RTC\_DRV\_V3020 is not set

#
# DMA Engine support
#
# CONFIG\_DMA\_ENGINE is not set

#
# DMA Clients
#

#
# DMA Devices
#

#
# Virtualization
#
# CONFIG\_KVM is not set

#
# File systems
#
CONFIG\_EXT2\_FS=y
# CONFIG\_EXT2\_FS\_XATTR is not set
# CONFIG\_EXT2\_FS\_XIP is not set
CONFIG\_EXT3\_FS=y
CONFIG\_EXT3\_FS\_XATTR=y
# CONFIG\_EXT3\_FS\_POSIX\_ACL is not set
# CONFIG\_EXT3\_FS\_SECURITY is not set
# CONFIG\_EXT4DEV\_FS is not set
CONFIG\_JBD=y
# CONFIG\_JBD\_DEBUG is not set
CONFIG\_FS\_MBCACHE=y
# CONFIG\_REISERFS\_FS is not set
# CONFIG\_JFS\_FS is not set
# CONFIG\_FS\_POSIX\_ACL is not set
# CONFIG\_XFS\_FS is not set
# CONFIG\_GFS2\_FS is not set
# CONFIG\_OCFS2\_FS is not set
# CONFIG\_MINIX\_FS is not set
# CONFIG\_ROMFS\_FS is not set
# CONFIG\_INOTIFY is not set
# CONFIG\_QUOTA is not set
CONFIG\_DNOTIFY=y
# CONFIG\_AUTOFS\_FS is not set
# CONFIG\_AUTOFS4\_FS is not set
# CONFIG\_FUSE\_FS is not set

#
# CD-ROM/DVD Filesystems
#
CONFIG\_ISO9660\_FS=y
CONFIG\_JOLIET=y
CONFIG\_ZISOFS=y
CONFIG\_ZISOFS\_FS=y
# CONFIG\_UDF\_FS is not set

#
# DOS/FAT/NT Filesystems
#
CONFIG\_FAT\_FS=y
CONFIG\_MSDOS\_FS=m
CONFIG\_VFAT\_FS=y
CONFIG\_FAT\_DEFAULT\_CODEPAGE=850
CONFIG\_FAT\_DEFAULT\_IOCHARSET="iso8859-1"
# CONFIG\_NTFS\_FS is not set

#
# Pseudo filesystems
#
CONFIG\_PROC\_FS=y
CONFIG\_PROC\_KCORE=y
CONFIG\_PROC\_SYSCTL=y
CONFIG\_SYSFS=y
CONFIG\_TMPFS=y
# CONFIG\_TMPFS\_POSIX\_ACL is not set
# CONFIG\_HUGETLBFS is not set
# CONFIG\_HUGETLB\_PAGE is not set
CONFIG\_RAMFS=y
# CONFIG\_CONFIGFS\_FS is not set

#
# Miscellaneous filesystems
#
# CONFIG\_ADFS\_FS is not set
# CONFIG\_AFFS\_FS is not set
# CONFIG\_HFS\_FS is not set
# CONFIG\_HFSPLUS\_FS is not set
# CONFIG\_BEFS\_FS is not set
# CONFIG\_BFS\_FS is not set
# CONFIG\_EFS\_FS is not set
# CONFIG\_CRAMFS is not set
# CONFIG\_SQUASHFS is not set
# CONFIG\_VXFS\_FS is not set
# CONFIG\_HPFS\_FS is not set
# CONFIG\_QNX4FS\_FS is not set
# CONFIG\_SYSV\_FS is not set
# CONFIG\_UFS\_FS is not set

#
# Network File Systems
#
# CONFIG\_NFS\_FS is not set
# CONFIG\_NFSD is not set
CONFIG\_SMB\_FS=m
# CONFIG\_SMB\_NLS\_DEFAULT is not set
CONFIG\_CIFS=y
CONFIG\_CIFS\_STATS=y
# CONFIG\_CIFS\_STATS2 is not set
# CONFIG\_CIFS\_WEAK\_PW\_HASH is not set
CONFIG\_CIFS\_XATTR=y
# CONFIG\_CIFS\_POSIX is not set
# CONFIG\_CIFS\_DEBUG2 is not set
# CONFIG\_CIFS\_EXPERIMENTAL is not set
# CONFIG\_NCP\_FS is not set
# CONFIG\_CODA\_FS is not set
# CONFIG\_AFS\_FS is not set
# CONFIG\_9P\_FS is not set

#
# Partition Types
#
CONFIG\_PARTITION\_ADVANCED=y
# CONFIG\_ACORN\_PARTITION is not set
# CONFIG\_OSF\_PARTITION is not set
# CONFIG\_AMIGA\_PARTITION is not set
# CONFIG\_ATARI\_PARTITION is not set
# CONFIG\_MAC\_PARTITION is not set
CONFIG\_MSDOS\_PARTITION=y
# CONFIG\_BSD\_DISKLABEL is not set
# CONFIG\_MINIX\_SUBPARTITION is not set
# CONFIG\_SOLARIS\_X86\_PARTITION is not set
# CONFIG\_UNIXWARE\_DISKLABEL is not set
# CONFIG\_LDM\_PARTITION is not set
# CONFIG\_SGI\_PARTITION is not set
# CONFIG\_ULTRIX\_PARTITION is not set
# CONFIG\_SUN\_PARTITION is not set
# CONFIG\_KARMA\_PARTITION is not set
# CONFIG\_EFI\_PARTITION is not set

#
# Native Language Support
#
CONFIG\_NLS=y
CONFIG\_NLS\_DEFAULT="iso8859-15"
# CONFIG\_NLS\_CODEPAGE\_437 is not set
# CONFIG\_NLS\_CODEPAGE\_737 is not set
# CONFIG\_NLS\_CODEPAGE\_775 is not set
CONFIG\_NLS\_CODEPAGE\_850=y
# CONFIG\_NLS\_CODEPAGE\_852 is not set
# CONFIG\_NLS\_CODEPAGE\_855 is not set
# CONFIG\_NLS\_CODEPAGE\_857 is not set
# CONFIG\_NLS\_CODEPAGE\_860 is not set
# CONFIG\_NLS\_CODEPAGE\_861 is not set
# CONFIG\_NLS\_CODEPAGE\_862 is not set
# CONFIG\_NLS\_CODEPAGE\_863 is not set
# CONFIG\_NLS\_CODEPAGE\_864 is not set
# CONFIG\_NLS\_CODEPAGE\_865 is not set
# CONFIG\_NLS\_CODEPAGE\_866 is not set
# CONFIG\_NLS\_CODEPAGE\_869 is not set
# CONFIG\_NLS\_CODEPAGE\_936 is not set
# CONFIG\_NLS\_CODEPAGE\_950 is not set
# CONFIG\_NLS\_CODEPAGE\_932 is not set
# CONFIG\_NLS\_CODEPAGE\_949 is not set
# CONFIG\_NLS\_CODEPAGE\_874 is not set
# CONFIG\_NLS\_ISO8859\_8 is not set
# CONFIG\_NLS\_CODEPAGE\_1250 is not set
# CONFIG\_NLS\_CODEPAGE\_1251 is not set
# CONFIG\_NLS\_ASCII is not set
CONFIG\_NLS\_ISO8859\_1=y
# CONFIG\_NLS\_ISO8859\_2 is not set
# CONFIG\_NLS\_ISO8859\_3 is not set
# CONFIG\_NLS\_ISO8859\_4 is not set
# CONFIG\_NLS\_ISO8859\_5 is not set
# CONFIG\_NLS\_ISO8859\_6 is not set
# CONFIG\_NLS\_ISO8859\_7 is not set
# CONFIG\_NLS\_ISO8859\_9 is not set
# CONFIG\_NLS\_ISO8859\_13 is not set
# CONFIG\_NLS\_ISO8859\_14 is not set
CONFIG\_NLS\_ISO8859\_15=y
# CONFIG\_NLS\_KOI8\_R is not set
# CONFIG\_NLS\_KOI8\_U is not set
CONFIG\_NLS\_UTF8=y

#
# Distributed Lock Manager
#
# CONFIG\_DLM is not set

#
# Instrumentation Support
#
# CONFIG\_PROFILING is not set
# CONFIG\_KPROBES is not set

#
# Kernel hacking
#
CONFIG\_TRACE\_IRQFLAGS\_SUPPORT=y
# CONFIG\_PRINTK\_TIME is not set
CONFIG\_ENABLE\_MUST\_CHECK=y
CONFIG\_MAGIC\_SYSRQ=y
CONFIG\_UNUSED\_SYMBOLS=y
# CONFIG\_DEBUG\_FS is not set
# CONFIG\_HEADERS\_CHECK is not set
# CONFIG\_DEBUG\_KERNEL is not set
CONFIG\_LOG\_BUF\_SHIFT=14
CONFIG\_DEBUG\_BUGVERBOSE=y
CONFIG\_EARLY\_PRINTK=y
CONFIG\_X86\_FIND\_SMP\_CONFIG=y
CONFIG\_X86\_MPPARSE=y
CONFIG\_DOUBLEFAULT=y

#
# Security options
#
# CONFIG\_KEYS is not set
# CONFIG\_SECURITY is not set

#
# Cryptographic options
#
# CONFIG\_CRYPTO is not set

#
# Library routines
#
CONFIG\_BITREVERSE=y
# CONFIG\_CRC\_CCITT is not set
# CONFIG\_CRC16 is not set
CONFIG\_CRC32=y
# CONFIG\_LIBCRC32C is not set
CONFIG\_ZLIB\_INFLATE=y
CONFIG\_TEXTSEARCH=y
CONFIG\_TEXTSEARCH\_KMP=m
CONFIG\_TEXTSEARCH\_BM=m
CONFIG\_TEXTSEARCH\_FSM=m
CONFIG\_PLIST=y
CONFIG\_IOMAP\_COPY=y
CONFIG\_GENERIC\_HARDIRQS=y
CONFIG\_GENERIC\_IRQ\_PROBE=y
CONFIG\_X86\_BIOS\_REBOOT=y
CONFIG\_KTIME\_SCALAR=y

```



Retrieved from "[http://wiki.soekris.info/Configuration\_for\_Gentoo](Configuration_for_Gentoo.html)"
[Categories](https://web.archive.org/web/20180610231459/http://wiki.soekris.info/Special:Categories "Special:Categories"): [Operating Systems](https://web.archive.org/web/20180610231459/http://wiki.soekris.info/Category:Operating_Systems "Category:Operating Systems") | [HowTo](https://web.archive.org/web/20180610231459/http://wiki.soekris.info/Category:HowTo "Category:HowTo")

 

