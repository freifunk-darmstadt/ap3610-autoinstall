# Flash Tool
- Make sure the `expect` tool is installed.
- Set the IP-Address of your computer to 192.168.1.66 (TFTP Server IP) connect to the AP.
- Download openwrt-ap3610-ramboot.bin and place it in the tftp server dir.
- Download openwrt-ap3610-sysupgrade.bin and place it the http server dir.
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