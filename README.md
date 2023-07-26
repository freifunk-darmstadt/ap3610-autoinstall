# Flash Tool
- Make sure the `expect` interpreter is installed.
- Set the IP-Address of your computer to 192.168.1.66 (TFTP Server IP).
- Download [https://downloads.openwrt.org/releases/22.03.5/targets/ath79/generic/openwrt-22.03.5-ath79-generic-siemens_ws-ap3610-initramfs-kernel.bin](openwrt-ap3610-ramboot.bin) and place it in the tftp server dir.
- Download [https://downloads.openwrt.org/releases/22.03.5/targets/ath79/generic/openwrt-22.03.5-ath79-generic-siemens_ws-ap3610-squashfs-sysupgrade.bin](openwrt-ap3610-sysupgrade.bin) and place it the http server dir.
- export DEVICE=/dev/ttyUSB0
- export HOSTIP=192.168.1.66 (HTTP Server IP)
- `./flash3610.exo`
- Follow the instructions.

## NixOS
```
  services.atftpd = {
    enable = true;
    root = "/var/tftp";
  };

  services.nginx = {
    enable = true;
    virtualHosts."fe80::changme" = {
      root = "/var/tftp";
    };
  };
```