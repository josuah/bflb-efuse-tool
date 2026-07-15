# bflb-efuse-tool

```
pip install bflb-efuse-tool
```

Dump and modify efuse files extracted from BouffaloLabs chips so they can be programmed back.

The files can be extracted using
[`BLFlashCommand`](https://github.com/bouffalolab/bouffalo_sdk/blob/master/tools/bflb_tools/bouffalo_flash_cube/BLFlashCommand-ubuntu):

For instance, after switching the chip to bootloader mode, extract an efuse file for bl616:

```
./BLFlashCommand-ubuntu --chipname bl616 --efuse --read --start 0x00 --end 0x200 --file efuse_bl616.bin
```

Then move JTAG from pins 0, 1, 2, 3 to pins 16 (TMS), 17 (TCK), 18 (TDO), 19 (TDI):

```
bflb-efuse-tool --chip bl616 --in-file efuse_bl616.bin --out-file efuse_bl616_modified.bin --set jtag_cfg=3
```

Then program the efuse file back:

```
./BLFlashCommand-ubuntu --chipname bl616 --efuse --write --start 0x00 --end 0x200 --efusefile efuse_bl616.bin
```
