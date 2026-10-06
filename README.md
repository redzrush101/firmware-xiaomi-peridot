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

ADSP, CDSP and WPSS firmware is not included: it is loaded from the phone's own
`modem` partition by msm-firmware-loader.
