# Xiaomi POCO F6 (peridot) firmware

Non-free firmware for running mainline Linux on the Xiaomi POCO F6 / Redmi
Turbo 3 (SM8635), laid out as under `/lib/firmware`. The zap shader is signed
for Xiaomi's secure boot keys; the Qualcomm reference (QRD) blobs do not load.

Source: LineageOS 23.2 peridot nightly 20261002
(`lineage-23.2-20261002-nightly-peridot-signed.zip`, SHA-256
d2cf79e6b4a29529f8dbd3d96afaad73ef83e9333c95a1f34b114387655cd03d).

| File | Image path |
| --- | --- |
| `qcom/gen71100_sqe.fw` | vendor `/firmware/gen71100_sqe.fw` |
| `qcom/gen71100_gmu.bin` | vendor `/firmware/gen71100_gmu.bin` |
| `qcom/palawan/xiaomi/peridot/gen71100_zap.mbn` | odm `/firmware/gen71100_zap.mbn` |
| `qcom/palawan/xiaomi/peridot/vpu30_2v.mbn` | odm `/firmware/vpu30_2v.mbn` |
| `qcom/palawan/xiaomi/peridot/aw88261_acf.bin` | odm `/firmware/aw882xx_acf.bin` |
| `qcom/palawan/Xiaomi-Peridot-tplg.bin` | built, see below |

`Xiaomi-Peridot-tplg.bin` is the AudioReach topology (BSD-3-Clause) built
with `alsatplg` from `Xiaomi-Peridot.m4` on the
[`peridot` branch of audioreach-topology](https://github.com/redzrush101/audioreach-topology/tree/peridot).
The TDM endpoint macros and board topology are pending upstream review.

The current binary was built from commit
`69f76efe886f0fc38edc371327c5a4fb928f8185`. The cleaned topology branch at
`6c3a5c2` reproduces it byte-for-byte after separating reusable TDM support
from the board topology. It provides MultiMedia1 speaker
playback through QUINARY_TDM_RX_0 and MultiMedia2 microphone capture through
TX_CODEC_DMA_TX_3. Both use S16_LE at 48 kHz; capture supports one or two
channels. Mixer routing uses the
[Xiaomi/peridot UCM profile](https://github.com/redzrush101/alsa-ucm-conf/tree/peridot/bringup/ucm2/Xiaomi/peridot),
packaged by postmarketOS as `device-xiaomi-peridot-ucm`.

To rebuild from that source checkout:

```sh
m4 -I . Xiaomi-Peridot.m4 > Xiaomi-Peridot.conf
alsatplg -c Xiaomi-Peridot.conf -o Xiaomi-Peridot-tplg.bin
```

ADSP, CDSP and WPSS firmware is not included: it is loaded from the phone's own
`modem` partition by msm-firmware-loader.
