# Flash Tool
- Make sure the `expect` interpreter is installed.
- Set the IP-Address of your computer to 192.168.1.66 (TFTP Server IP).
- Download [https://downloads.openwrt.org/releases/22.03.5/targets/ath79/generic/openwrt-22.03.5-ath79-generic-siemens_ws-ap3610-initramfs-kernel.bin](openwrt-ap3610-ramboot.bin)
- Download [https://downloads.openwrt.org/releases/22.03.5/targets/ath79/generic/openwrt-22.03.5-ath79-generic-siemens_ws-ap3610-squashfs-sysupgrade.bin](openwrt-ap3610-sysupgrade.bin)
- Rename the files to `openwrt-ap3610-ramboot.bin` and `openwrt-ap3610-sysupgrade.bin`.
- To setup an http server execute in the folder, in which the `openwrt-ap3610-sysupgrade.bin` file is located, `python3 -m http.server`. (Make sure that this folder does not contain any private information, the whole content will be available over http.)
- To setup an tftp server install tftpd-hpa. `systemctl start tftpd-hpa.service`. Move the `openwrt-ap3610-ramboot.bin` to `/srv/tftp/`.
- export DEVICE=/dev/ttyUSB0
- export HOSTIP=192.168.1.66 (HTTP Server IP)
- export APIP=192.168.1.101 (Change this if you flash multiple APs at the same time.)
- Connect the serial adapter, and leave it conected.
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