# Houji standalone touch modules

Source: onelots/android_kernel_xiaomi_sm8650-modules, commit
`dee2cc21e4e522f9d0ba1cb13ff491160ca54151` (lineage-24.0).
The houji Kbuild profile enables Synaptics TCM2, Xiaomi THP and FOD support.
It builds synaptics_tcm2.ko and xiaomi_touch.ko together using one symbol table.

The module-local include/linux/xiaomi_touch.h is the GPL UAPI from
onelots/android_kernel_xiaomi_sm8650, commit
`a97ae5488e013a9083aff05564ebd53e8cae342a`, path
include/uapi/linux/xiaomi_touch.h. Keep it module-local so standalone builds
do not require changes to the core kernel UAPI. Kbuild adds this include path.

This import passed compile, modpost, link and BTF against the MiCode 6.1.25
product kernel with CONFIG_ARCH_PINEAPPLE=y and CONFIG_TARGET_PRODUCT_HOUJI=y.
Ordinary userdebug with the 105-module early ramdisk, SELinux enforcing and
secure ADB boots and processes the CN raw frames through the existing vendor
algorithm. Physical DOWN/MOVE/UP events were captured and the user confirmed
working clicks and scrolling. Advanced gestures and FOD remain unverified.
Keep kernel CRC, CFI and module version checks enabled.
