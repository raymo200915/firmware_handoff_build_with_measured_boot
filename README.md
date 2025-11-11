# Firmware Handoff Build and Run

## Use case A - Device Tree handoff through BL2/BL31/BL32/BL33

To build and run for Firmware Handoff across TF-A / OP-TEE / U-Boot:

```
# Export your toolchains
# export CROSS_COMPILE=<toolchain64-prefix>-
# export CROSS_COMPILE32=<toolchain32-prefix>-
# export CROSS_COMPILE64=<toolchain64-prefix>-
# optional for Clang
# export USECLANG=HOSTCC=clang CC="clang -target <toolchain64-prefix>"

# For example:
export CROSS_COMPILE=aarch64-none-linux-gnu-
export CROSS_COMPILE32=arm-none-linux-gnueabihf-
export CROSS_COMPILE64=aarch64-none-linux-gnu-
# optional for Clang
export USECLANG=HOSTCC=clang CC="clang -target aarch64-none-linux-gnu"
```

Followed by:

```
make -f Makefile.tl_dt_has_bl32 all
make -f Makefile.tl_dt_has_bl32 run-only
```

Or just:

```
make -f Makefile.tl_dt_has_bl32 run
```

In U-Boot console, explore the bloblist (Aka. Transfer List) via:

```
bloblist info
bloblist list
```

## Use case B - Event Log handoff through BL2/BL33

To build and run for Firmware Handoff with Measured Boot enabled across TF-A / U-Boot:

```
# Export your toolchains
# export CROSS_COMPILE=<toolchain64-prefix>-
# optional for Clang
# export USECLANG=HOSTCC=clang CC="clang -target <toolchain64-prefix>"
#
# For example:
export CROSS_COMPILE=aarch64-none-linux-gnu-
# optional for Clang
export USECLANG=HOSTCC=clang CC="clang -target aarch64-none-linux-gnu"
# activate PCR bank of SWTPM, multiple banks separated by commas, e.g. PCR_BANKS=sha1,sha256,sha512
export PCR_BANKS=sha256
```

Followed by:

```
make -f Makefile.tl_tpm_no_bl32 all
make -f Makefile.tl_tpm_no_bl32 run-only
```

Or just:

```
make -f Makefile.tl_tpm_no_bl32 run
```

In Linux console, explore Event Log via:

```
sudo tpm2_eventlog /sys/kernel/security/tpm0/binary_bios_measurements
```

## Use case C - Event Log handoff through BL2/BL31/BL32/BL33

To build and run for Firmware Handoff with Measured Boot enabled across TF-A / OP-TEE / U-Boot:

```
# Export your toolchains
# export CROSS_COMPILE=<toolchain64-prefix>-
# export CROSS_COMPILE32=<toolchain32-prefix>-
# export CROSS_COMPILE64=<toolchain64-prefix>-
# optional for Clang
# export USECLANG=HOSTCC=clang CC="clang -target <toolchain64-prefix>"
#
# For example:
export CROSS_COMPILE=aarch64-none-linux-gnu-
export CROSS_COMPILE32=arm-none-linux-gnueabihf-
export CROSS_COMPILE64=aarch64-none-linux-gnu-
# optional for Clang
export USECLANG=HOSTCC=clang CC="clang -target aarch64-none-linux-gnu"
# activate PCR bank of SWTPM, multiple banks separated by commas, e.g. PCR_BANKS=sha1,sha256,sha512
export PCR_BANKS=sha256
```

Followed by:

```
make -f Makefile.tl_tpm_has_bl32 all
make -f Makefile.tl_tpm_has_bl32 run-only
```

Or just:

```
make -f Makefile.tl_tpm_has_bl32 run
```

In Linux console, explore Event Log via:

```
sudo tpm2_eventlog /sys/kernel/security/tpm0/binary_bios_measurements
```
