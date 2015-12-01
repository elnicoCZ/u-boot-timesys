To build u-boot for SQM4-VF6 for use with MfgTool, do the following:

1) Set the path to the ARM toolchain:
   $ export PATH=$PATH:<your_arm_toolchain/bin>
   e.g.
   $ export PATH=$PATH:/opt/poky-eb/1.7/sysroots/x86_64-pokysdk-linux/usr/bin/arm-poky-linux-gnueabi

2) Set the toolchain binaries' prefix:
   $ export CROSS_COMPILE=<prefix>
   e.g.
   $ export CROSS_COMPILE=arm-poky-linux-gnueabi-

3) Set the build configuration for SQM4-VF6-EasyBoard:
   $ make sqm4vf6eb_config
   (for SD/QSPI) or
   $ make sqm4vf6eb_nand_config
   (for NAND)

4) Build the u-boot:
   $ make u-boot.imx

5a) (SD/QSPI) Change the name of the output to reflect the target name:
   $ cp u-boot.imx u-boot.sqm4vf6eb

5b) (NAND) Pad by 1024 bytes (NAND start address is 0x400):
   $ dd if=/dev/zero of=pad1024 bs=1024 count=1
   $ cat pad1024 u-boot.imx > u-boot-nand.sqm4vf6eb

6) Copy the file to <MfgTool_directory>\Profiles\Vybrid Update\OS Firmware

7) Update the <MfgTool_directory>\Profiles\Vybrid Update\OS Firmware\ucl2.xml file to use the new file

