# RTS5129/RTS5139 [![Gitlab CI](https://gitlab.com/aurorafossorg/utils/rts5139/badges/master/pipeline.svg)](https://gitlab.com/aurorafossorg/utils/rts5139/pipelines) [![Codacy Badge](https://api.codacy.com/project/badge/Grade/95256f87488f4568815991fb8a379728)](https://www.codacy.com/app/aurorafossorg/rts5139)

## Overview

This is a temporary fix for RTS5129/RTS5139 USB MMC card reader on Linux 3.16+ kernels.

This ocurred during a transition from ```3.15``` to ```3.16``` kernel, as a result of the ```staging/rts5139``` driver (which worked with the RTS5129/RTS5139) being replaced by the newer ```rtsx``` driver (which does not work with the RTS5129/RTS5139). This project reverts back to the old drivers as a temporary measure to get things up and running again.

## Requirements

- make
- gcc
- linux-headers

## Building

1. Checkout, build and install the replacement driver.

```
cd /tmp
git clone https://github.com/aurorafossorg/rts5139.git
cd rts5139
make
sudo make install
```

2. Blacklist the problematic modules by adding `blacklist-rts5139.conf`, `blacklist-rts5139-dkms.conf`, or this to `/etc/modprobe.d/`:

```
blacklist rtsx_usb_sdmmc
blacklist rtsx_usb_ms
blacklist rtsx_usb
```

3. Then, make sure you generate modules.dep and map files.

```
sudo depmod -a
```

4. Finally, disable module autoloading (and, optionally, also in the initial RAM filesystem)

5. Blacklist rtsx mmc modules via kernel parameters.

6. If wanted/needed, update the initramfs.

7. Reboot, and check to see if the card reader works.

## License
GNU General Public License - Version 2, June 1991
