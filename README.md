# QEMU virtio-snd guest-to-host escape exploit

The exploit works on qemu commit `ece408818d27f745ef1b05fb3cc99a1e7a5bf580` on glibc 2.43. Required QEMU devices are virtio-snd and virtio-9p.
```
-audiodev alsa,id=audio0,in.dev=default,out.dev=default
-device virtio-sound-pci,audiodev=audio0
-fsdev local,id=fsdev0,path="./",security_model=none
-device virtio-9p-pci,fsdev=fsdev0,mount_tag=mnt
```

The kernel should have `CONFIG_NET_9P_VIRTIO` and `CONFIG_SND_VIRTIO` disabled, otherwise those drivers will bind before the exploit module can claim the devices. If they are built as modules adding `modprobe.blacklist=9pnet_virtio,snd_virtio` to the kernel command line should work as well.

## Demo

<video src="demo.mp4" controls></video>
