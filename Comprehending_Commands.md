# Comprehending Commands

## cat : not the pet, but the command

One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files.
`cat` will concatenate (hence the name) multiple files if provided multiple arguments.
<br>
In this challenge, the flag is stored in the `flag` path in the home directory.
Calling that path, will return the flag.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{UmoVbbL8Hyqsp5xADzgDiuoq1YJ.dFzN1QDLyETO0czW}
```

Note: If you give no arguments at all, cat will read from the terminal input and output it.

## catting absolute paths

Unlike the last challenge, in this one the flag is stored in the absolute path `/flag`.
Calling that path, will return the flag.
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{gfkpFMpIgRB0oAjVozjCZ_Lk56k.dlTM5QDLyETO0czW}
```

Fun fact : `/flag` is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## More catting practice

In this challenge, we must retrieve the flag by using the absolute path of the directory as an argument to `cat`.
```
You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/include/asm-generic/flag. Go cat it out **without** cding into
that directory!
hacker@commands~more-catting-practice:~$ cat  /usr/include/asm-generic/flag
pwn.college{QezrZjY53d_Ph0GlwXeuHx-ZMxL.dBjM5QDLyETO0czW}
```
Things we learnt : You can specify all sorts of paths as arguments to commands.

## Grepping for a needle in a haystack

Sometimes, the files that you might cat out are too big.
The grep command to search for the contents we need.
<br>
Syntax : `hacker@dojo:~$ grep SEARCH_STRING /path/to/file`
<br>
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{0YU-DU8Bkb9gwlTmxGDEYQQna-2.ddTM4QDLyETO0czW}
```

In this challenge, we use the `grep` command to search for the flag in the hundreds of lines of text.
Hint : The flag always contains the string `pwn.college`.

## Listing files

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.
In this challenge we need to access the path of the directory by running the path containing the flag after finding it in the listed files under the `/challenge` directory.

```
hacker@commands~listing-files:~$ ls /challenge
8247-renamed-run-5536  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/8247-renamed-run-5536
Yahaha, you found me! Here is your flag:
pwn.college{sxRPbecriwKzwzJadHLtiKcf4-1.dhjM4QDLyETO0czW}
```

## Touching files

You can create a new, blank file by *touching* it with the `touch` command.
```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$  /challenge/run
Success! Here is your flag:
pwn.college{ws1ihCTYc3xIwZJAhdkHCaKi2C5.dBzM4QDLyETO0czW}
```
In this challenge, we need to create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get the flag.

## Removing files

In Linux, you remove files with the `rm` command.

```
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{kdHDxm7vif0Q3OXfQW0vse89JWs.dZTOwUDLyETO0czW}
```

In this challenge, we need to delete the `delete_me` file in the home directory.
And then run `/challenge/check`, which will check the deletion.
If removed successfully it will return the flag.

## Hidden files

`ls` doesn't list all the files by default.
Linux has a convention where files that start with a `.` don't show up by default in `ls` and in a few other contexts.
To view them with `ls`, you need to invoke `ls` with the `-a` flag.

```
hacker@commands~hidden-files:~$ ls
'~'
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls
bin  boot  challenge  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv          bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-217717274319  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat /.flag-217717274319
pwn.college{keqKKczPwAqQc-nbNxu6AZlN2Rn.dBTN4QDLyETO0czW}
```

In this challenge, we had to find the flag in a dot prepended hidden file in a file in the `/` directory.

## An Epic Filesystem Quest

In this challenge, the hidden flag has to be retrieved through following the breadcrumbs.
Using the `cd`, `ls` and `cat` functions.

```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
SPOILER  bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@commands~an-epic-filesystem-quest:/$ cat SPOILER
Great sleuthing!
The next clue is in: /usr/include/linux

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/$ /$ ls/usr/include/linux
ssh-entrypoint: /$: No such file or directory
hacker@commands~an-epic-filesystem-quest:/$ ls/usr/include/linux
ssh-entrypoint: ls/usr/include/linux: No such file or directory
hacker@commands~an-epic-filesystem-quest:/$ ls /usr/include/linux
WHISPER-TRAPPED    cn_proc.h             hsr_netlink.h        kcov.h               nfc.h              rtc.h                udp.h
a.out.h            coda.h                hw_breakpoint.h      kd.h                 nfs.h              rtnetlink.h          uhid.h
acct.h             coff.h                hyperv.h             kdev_t.h             nfs2.h             rxrpc.h              uinput.h
adb.h              connector.h           hysdn_if.h           kernel-page-flags.h  nfs3.h             scc.h                uio.h
adfs_fs.h          const.h               i2c-dev.h            kernel.h             nfs4.h             sched                uleds.h
affs_hardblocks.h  coresight-stm.h       i2c.h                kernelcapi.h         nfs4_mount.h       sched.h              ultrasound.h
agpgart.h          cramfs_fs.h           i2o-dev.h            kexec.h              nfs_fs.h           scif_ioctl.h         un.h
aio_abi.h          cryptouser.h          i8k.h                keyboard.h           nfs_idmap.h        screen_info.h        unistd.h
am437x-vpfe.h      cuda.h                icmp.h               keyctl.h             nfs_mount.h        sctp.h               unix_diag.h
android            cyclades.h            icmpv6.h             kfd_ioctl.h          nfsacl.h           sdla.h               usb
apm_bios.h         cycx_cfm.h            if.h                 kvm.h                nfsd               seccomp.h            usbdevice_fs.h
arcfb.h            dcbnl.h               if_addr.h            kvm_para.h           nilfs2_api.h       securebits.h         usbip.h
arm_sdei.h         dccp.h                if_addrlabel.h       l2tp.h               nilfs2_ondisk.h    sed-opal.h           userfaultfd.h
aspeed-lpc-ctrl.h  devlink.h             if_alg.h             libc-compat.h        nl80211.h          seg6.h               userio.h
aspeed-p2a-ctrl.h  dlm.h                 if_arcnet.h          lightnvm.h           nsfs.h             seg6_genl.h          utime.h
atalk.h            dlm_device.h          if_arp.h             limits.h             nubus.h            seg6_hmac.h          utsname.h
atm.h              dlm_netlink.h         if_bonding.h         lirc.h               nvme_ioctl.h       seg6_iptunnel.h      uuid.h
atm_eni.h          dlm_plock.h           if_bridge.h          llc.h                nvram.h            seg6_local.h         uvcvideo.h
atm_he.h           dlmconstants.h        if_cablemodem.h      loop.h               omap3isp.h         selinux_netlink.h    v4l2-common.h
atm_idt77105.h     dm-ioctl.h            if_eql.h             lp.h                 omapfb.h           sem.h                v4l2-controls.h
atm_nicstar.h      dm-log-userspace.h    if_ether.h           lwtunnel.h           oom.h              serial.h             v4l2-dv-timings.h
atm_tcp.h          dma-buf.h             if_fc.h              magic.h              openvswitch.h      serial_core.h        v4l2-mediabus.h
atm_zatm.h         dns_resolver.h        if_fddi.h            major.h              packet_diag.h      serial_reg.h         v4l2-subdev.h
atmapi.h           dqblk_xfs.h           if_frad.h            map_to_7segment.h    param.h            serio.h              vbox_err.h
atmarp.h           dvb                   if_hippi.h           matroxfb.h           parport.h          shm.h                vbox_vmmdev_types.h
atmbr2684.h        edd.h                 if_infiniband.h      max2175.h            patchkey.h         signal.h             vboxguest.h
atmclip.h          efs_fs_sb.h           if_link.h            mdio.h               pci.h              signalfd.h           version.h
atmdev.h           elf-em.h              if_ltalk.h           media-bus-format.h   pci_regs.h         smc.h                veth.h
atmioc.h           elf-fdpic.h           if_macsec.h          media.h              pcitest.h          smc_diag.h           vfio.h
atmlec.h           elf.h                 if_packet.h          mei.h                perf_event.h       smiapp.h             vfio_ccw.h
atmmpc.h           elfcore.h             if_phonet.h          membarrier.h         personality.h      snmp.h               vhost.h
atmppp.h           errno.h               if_plip.h            memfd.h              pfkeyv2.h          sock_diag.h          vhost_types.h
atmsap.h           errqueue.h            if_ppp.h             mempolicy.h          pg.h               socket.h             videodev2.h
atmsvc.h           erspan.h              if_pppol2tp.h        meye.h               phantom.h          sockios.h            virtio_9p.h
audit.h            ethtool.h             if_pppox.h           mic_common.h         phonet.h           sonet.h              virtio_balloon.h
aufs_type.h        eventpoll.h           if_slip.h            mic_ioctl.h          pkt_cls.h          sonypi.h             virtio_blk.h
auto_dev-ioctl.h   fadvise.h             if_team.h            mii.h                pkt_sched.h        sound.h              virtio_config.h
auto_fs.h          falloc.h              if_tun.h             minix_fs.h           pktcdvd.h          soundcard.h          virtio_console.h
auto_fs4.h         fanotify.h            if_tunnel.h          mman.h               pmu.h              spi                  virtio_crypto.h
auxvec.h           fb.h                  if_vlan.h            mmc                  poll.h             stat.h               virtio_fs.h
ax25.h             fcntl.h               if_x25.h             mmtimer.h            posix_acl.h        stddef.h             virtio_gpu.h
b1lli.h            fd.h                  if_xdp.h             module.h             posix_acl_xattr.h  stm.h                virtio_ids.h
batadv_packet.h    fdreg.h               ife.h                mount.h              posix_types.h      string.h             virtio_input.h
batman_adv.h       fib_rules.h           igmp.h               mpls.h               ppdev.h            sunrpc               virtio_iommu.h
baycom.h           fiemap.h              iio                  mpls_iptunnel.h      ppp-comp.h         suspend_ioctls.h     virtio_mmio.h
bcache.h           filter.h              ila.h                mqueue.h             ppp-ioctl.h        swab.h               virtio_net.h
bcm933xx_hcs.h     firewire-cdev.h       in.h                 mroute.h             ppp_defs.h         switchtec_ioctl.h    virtio_pci.h
bfs_fs.h           firewire-constants.h  in6.h                mroute6.h            pps.h              sync_file.h          virtio_pmem.h
binfmts.h          fou.h                 in_route.h           msdos_fs.h           pr.h               synclink.h           virtio_ring.h
blkpg.h            fpga-dfl.h            inet_diag.h          msg.h                prctl.h            sysctl.h             virtio_rng.h
blktrace_api.h     fs.h                  inotify.h            mtio.h               psample.h          sysinfo.h            virtio_scsi.h
blkzoned.h         fscrypt.h             input-event-codes.h  n_r3964.h            psci.h             target_core_user.h   virtio_types.h
bpf.h              fsi.h                 input.h              nbd-netlink.h        psp-sev.h          taskstats.h          virtio_vsock.h
bpf_common.h       fsl_hypervisor.h      io_uring.h           nbd.h                ptp_clock.h        tc_act               vm_sockets.h
bpf_perf_event.h   fsmap.h               ioctl.h              ncsi.h               ptrace.h           tc_ematch            vm_sockets_diag.h
bpfilter.h         fsverity.h            iommu.h              ndctl.h              qemu_fw_cfg.h      tcp.h                vmcore.h
bpqether.h         fuse.h                ip.h                 neighbour.h          qnx4_fs.h          tcp_metrics.h        vsockmon.h
bsg.h              futex.h               ip6_tunnel.h         net.h                qnxtypes.h         tee.h                vt.h
bt-bmc.h           gameport.h            ip_vs.h              net_dropmon.h        qrtr.h             termios.h            vtpm_proxy.h
btf.h              gen_stats.h           ipc.h                net_namespace.h      quota.h            thermal.h            wait.h
btrfs.h            genetlink.h           ipmi.h               net_tstamp.h         radeonfb.h         time.h               watch_queue.h
btrfs_tree.h       genwqe                ipmi_bmc.h           netconf.h            raid               time_types.h         watchdog.h
byteorder          gfs2_ondisk.h         ipmi_msgdefs.h       netdevice.h          random.h           timerfd.h            wimax
caif               gigaset_dev.h         ipsec.h              netfilter            raw.h              times.h              wimax.h
can                gpio.h                ipv6.h               netfilter.h          rds.h              timex.h              wireless.h
can.h              gsmmux.h              ipv6_route.h         netfilter_arp        reboot.h           tiocl.h              wmi.h
capability.h       gtp.h                 ipx.h                netfilter_arp.h      reiserfs_fs.h      tipc.h               x25.h
capi.h             hash_info.h           irqnr.h              netfilter_bridge     reiserfs_xattr.h   tipc_config.h        xattr.h
cciss_defs.h       hdlc                  isdn                 netfilter_bridge.h   resource.h         tipc_netlink.h       xdp_diag.h
cciss_ioctl.h      hdlc.h                iso_fs.h             netfilter_ipv4       rfkill.h           tipc_sockets_diag.h  xfrm.h
cdrom.h            hdlcdrv.h             isst_if.h            netfilter_ipv4.h     rio_cm_cdev.h      tls.h                xilinx-v4l2-controls.h
cec-funcs.h        hdreg.h               ivtv.h               netfilter_ipv6       rio_mport_cdev.h   toshiba.h            zorro.h
cec.h              hid.h                 ivtvfb.h             netfilter_ipv6.h     romfs_fs.h         tty.h                zorro_ids.h
cgroupstats.h      hiddev.h              jffs2.h              netlink.h            rose.h             tty_flags.h
chio.h             hidraw.h              joystick.h           netlink_diag.h       route.h            types.h
cifs               hpet.h                kcm.h                netrom.h             rpmsg.h            udf_fs_i.h
cm4000_cs.h        hsi                   kcmp.h               nexthop.h            rseq.h             udmabuf.h
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/include/linux/WHISPER-TRAPPED
Congratulations, you found the clue!
The next clue is in: /usr/share/locale/ko

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/$ ls /usr/share/locale/ko
DOSSIER-TRAPPED  LC_MESSAGES
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/share/locale/ko/DOSSIER-TRAPPED
Tubular find!
The next clue is in: /usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/third_party/2and3/chardet

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/third_party/2and3/chardet
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/third_party/2and3/chardet$ ls
MESSAGE       enums.pyi               langcyrillicmodel.pyi  langhebrewmodel.pyi     langthaimodel.pyi     universaldetector.pyi
__init__.pyi  langbulgarianmodel.pyi  langgreekmodel.pyi     langhungarianmodel.pyi  langturkishmodel.pyi  version.pyi
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/third_party/2and3/chardet$ cat MESSAGE
Tubular find!
The next clue is in: /usr/share/perl/5.30.0/I18N/LangTags

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/jedi/third_party/typeshed/third_party/2and3/chardet$ cd /usr/share/perl/5.30.0/I18N/LangTags
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/I18N/LangTags$ ls
Detect.pm  List.pm  NOTE
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/I18N/LangTags$ cat NOTE
Great sleuthing!
The next clue is in: /opt/aflplusplus/nyx_mode/QEMU-Nyx/hw/9pfs
hacker@commands~an-epic-filesystem-quest:/usr/share/perl/5.30.0/I18N/LangTags$ cd /opt/aflplusplus/nyx_mode/QEMU-Nyx/hw/9pfs
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/QEMU-Nyx/hw/9pfs$ ls
9p-local.c      9p-proxy.c  9p-synth.h  9p-xattr-user.c  9p.c     Makefile.objs  cofile.c  coth.h        virtio-9p-device.c  xen-9pfs.h
9p-local.h      9p-proxy.h  9p-util.c   9p-xattr.c       9p.h     REVELATION     cofs.c    coxattr.c     virtio-9p.h
9p-posix-acl.c  9p-synth.c  9p-util.h   9p-xattr.h       Kconfig  codir.c        coth.c    trace-events  xen-9p-backend.c
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/QEMU-Nyx/hw/9pfs$ cat REVELATION
Yahaha, you found me!
The next clue is in: /opt/radare2/shlr/gdb/src/gdbserver
hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/QEMU-Nyx/hw/9pfs$ cd /opt/radare2/shlr/gdb/src/gdbserver
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/gdb/src/gdbserver$ ls
README  core.c  core.d  core.o
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/gdb/src/gdbserver$ cat README
Congratulations, you found the clue!
The next clue is in: /opt/linux/linux-5.4/arch/mips/emma/markeins

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/gdb/src/gdbserver$ cat core.c
// Notes and useful links:
// This conversation (https://www.sourceware.org/ml/gdb/2009-02/msg00100.html) suggests GDB clients usually ignore error codes
// Useful, but not to be blindly trusted - http://www.embecosm.com/appnotes/ean4/embecosm-howto-rsp-server-ean4-issue-2.html
// https://github.com/llvm-mirror/lldb/blob/master/docs/lldb-gdb-remote.txt
// http://www.cygwin.com/ml/gdb/2008-05/msg00166.html

#include "gdbserver/core.h"
#include "gdbr_common.h"
#include "libgdbr.h"
#include "packet.h"
#include "utils.h"
#include <r_util.h>
hacker@commands~an-epic-filesystem-quest:/opt/radare2/shlr/gdb/src/gdbserver$ cd /opt/linux/linux-5.4/arch/mips/emma/markeins
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/emma/markeins$ ls -a
.  ..  .MEMO  Makefile  irq.c  led.c  platform.c  setup.c
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/emma/markeins$ cat .MEMO
Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/jedi/third_party/typeshed/stdlib/3/http

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/emma/markeins$ cd /usr/lib/python3/dist-packages/jedi/third_party/typeshed/stdlib/3/http
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/jedi/third_party/typeshed/stdlib/3/http$ ls -l
total 32
-rw-r--r-- 1 root root  144 Oct  8 17:09 INSIGHT
-rw-r--r-- 1 root root 1689 Dec 20  2019 __init__.pyi
-rw-r--r-- 1 root root 6269 Dec 20  2019 client.pyi
-rw-r--r-- 1 root root 4888 Dec 20  2019 cookiejar.pyi
-rw-r--r-- 1 root root 1280 Dec 20  2019 cookies.pyi
-rw-r--r-- 1 root root 3176 Dec 20  2019 server.pyi
hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/jedi/third_party/typeshed/stdlib/3/http$ cat INSIGHT
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{IWa6vXY9wH_5NYPDckn0VuWABXb.dljM4QDLyETO0czW}
```
## Making directories

Things we learnt : We can create directories using the `mkdir` command.
It uses the absolute path as its parameter.
```
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ cd
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{cRyQO3u4bYJNUBsYlzfoqGUzj-M.dFzM4QDLyETO0czW}
```
In this challenge, we need to `touch` the `college` file in the newly created `/tmp/pwn` directory.
Using `mkdir` command, and then running `/challenge/run` to retrieve the flag.

## Finding files

The `find` command takes optional arguments describing the search criteria and the search location.
If you don't specify a search criteria, `find` matches every file.
If you don't specify a search location, `find` uses the current working directory (.).
<br>
In this challenge, we need to find a file named `flag` which contains the flag.
Since multiple like named files exist, read them all using `cat` until you retrieve the flag.

```
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/8/task/8/fd’: Permission denied
find: ‘/proc/8/task/8/fdinfo’: Permission denied
find: ‘/proc/8/task/8/ns’: Permission denied
find: ‘/proc/8/fd’: Permission denied
find: ‘/proc/8/map_files’: Permission denied
find: ‘/proc/8/fdinfo’: Permission denied
find: ‘/proc/8/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.XvrUsDZh8M’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
/opt/linux/linux-5.4/arch/arm64/include/asm/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/local/share/radare2/5.9.5/flag
cat: /usr/local/share/radare2/5.9.5/flag: Is a directory
hacker@commands~finding-files:~$ cat /opt/aflplusplus/.git/hooks/flag
cat: /opt/aflplusplus/.git/hooks/flag: No such file or directory
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /opt/linux/linux-5.4/arch/arm64/include/asm/flag
pwn.college{4OBXPjQCu9e3NjqYYBTHyetW03s.dJzM4QDLyETO0czW}
```

Things we learnt : Syntax = `find / -name <file_name>`.
It searches the whole filesystem for the file named `<file_name>`.

## Linking files

Things we learnt : Symbolic links (also also known as symlinks) are created with the `ln` command with the `-s` argument.
<br>
Note : The original file path comes *before* the link path in the command!
<br>
Fun Fact : A symlink can be identified as such with a few methods. For example, the file command, which takes a filename and tells you what type of file it is.

```
hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{kUwos0SzS8r8RjYwzm5ttMF1lBV.dlTM1UDLyETO0czW}
```

In this challenge, we had to link the contents of `flag` to `~/not-the-flag`.
Since `/challenge/catflag` reads the contents of `~/not-the-flag`,
it will actually read the linked contents of `/flag`.  



