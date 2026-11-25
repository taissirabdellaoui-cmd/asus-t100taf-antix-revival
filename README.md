# Reviving an ASUS Transformer Book T100TAF with antiX-26.1 (64-bit)

A systems engineering case study documenting the bare-metal installation and kernel/network debugging of a 64-bit Linux distribution (**antiX-26.1**) on legacy Intel Bay Trail 2-in-1 hardware (**ASUS Transformer Book T100TAF**).

## Hardware & Software Stack
* **Target Hardware:** ASUS Transformer Book T100TAF (Intel Atom Bay Trail SoC, 32-bit UEFI firmware, 32 GB eMMC `mmcblk1`, Broadcom `BCM43340/2` Wi-Fi)
* **Operating System:** antiX-26.1 Full (64-bit) with Linux Kernel `5.10` (`sysVinit` / `runit`)
* **Network & Audio Subsystems:** ConnMan (`cmst`) + `wpa_supplicant`, `brcmfmac` FullMAC driver, ALSA `bytcr-rt5640`

## Key Technical Challenges & Solutions
1. **32-Bit Mixed-Mode UEFI Boot on 64-Bit Linux:** Partitioned the internal eMMC (`mmcblk1`) with a dedicated 32-bit EFI System Partition (`bootia32.efi`) and GRUB bootloader so the 32-bit firmware could hand off execution to a 64-bit Linux kernel.
2. **Bay Trail Audio & Input Localization:** Verified native `bytcr-rt5640` I2S audio routing on kernel `5.10`, locked landscape screen rotation, and configured French AZERTY (`fr`) keymap persistence.
3. **Broadcom `brcmfmac` & IEEE 802.11w (PMF) Handshake Failure:** Resolved repeated WPA authentication rejections by isolating Protected Management Frames (PMF) incompatibility in WPA2/WPA3 mixed mode, switching the access point to pure `WPA2-PSK` (AES), purging stale ConnMan service caches (`/var/lib/connman/`), and re-registering the `cmst` D-Bus agent.

## Full Technical Write-Up
* [ASUS T100TAF & antiX-26.1 Systems Engineering & Troubleshooting Reference (PDF)](./ASUS%20T100TAF%20%26%20antiX-26.1%20Systems%20Engineering%20%26%20Troubleshooting%20Reference.pdf)
