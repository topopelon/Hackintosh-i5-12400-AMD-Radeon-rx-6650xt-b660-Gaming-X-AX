# Hackintosh-i5-12400-AMD-Radeon-rx-6650xt-b660-Gaming-X-AX

# Specs

- CPU: Intel i5-12400
- GPU: AMD Radeon rx 6650xt
- Motherboard: Gigabyte B660 Gaming X AX DDR4
- RAM: 16GB
- SSD m.2 (MacOS): 500GB
- SSD m.2 (Windows): 1TB

# What works

- [x] iServices
- [x] Audio
- [x] Ethernet
- [x] USBs (I didn't need to map usb ports but I did it anyway)
- [x] DRM
- [x] HDMI (no audio - I use a DP to HDMI adapter and it works)
- [x] Hardware Acceleration

# What doesn't work

- [ ] Wifi and Bluetooth (I use a TPLink T2U AC600 USB adapter and it works)
- [ ] Sleep (it works but randomly wakes up - the monitor stop working but the pc is still on)

# What I did

I used [this guide](https://www.reddit.com/r/hackintosh/comments/sp1zgv/opencore_alder_lake_12thgen_intel_hackintosh/) to install MacOS. Both Intel Alder Lake 12th Gen and AMD Radeon RX 6650 XT are not supported out of the box. In order to bypass this, we have to spoof both components.

Boot args:

```
keepsyms=1 debug=0x100 agdpmod=pikera -wegnoigpu alcid=66
```

It is important to disable the iGPU for the sake of compatibility `-wegnoigpu`. Also, as the gpu is an AMD Radeon we have to include `-agdpmod=pikera` and `-alcid=66` to make the audio work flawlessly.

My MacOS is installed in the 500gb m.2 SSD. I have a 1TB m.2 SSD with Windows installed. I have to disable the Secure Boot in the BIOS in order to make the Windows bootable USB work. This way, both OS can coexist in the same computer without any problem.

# Problems

- I was stucked at the first boot screen. I had to disable and enable all the features in the BIOS (like VT-d, CSM, etc) and then it worked. Specially, disable the **Resizable BAR** feature.

- HDMI audio doesn't work. I read in some random and hidden forum that it's a problem with the HDMI port. I use a DP to HDMI adapter and it works. Maybe the solution has to pass through patching some pins or something like that.

- My motherbase wifi antenna is not compatible with MacOS. I had a TPLink T2U AC600 USB adapter and it worked out of the box. Something that you have to be aware of is that **I had to disable SIP** and make it work with [this link](https://github.com/chris1111/Wireless-USB-Adapter) or [this one](https://github.com/chris1111/D-LinkUtility-Package). I don't remember which one I used.

- In order to use my AMD Radeon rx 6650xt, I had to spoof it as a Radeon RX 6600xt. I directly copied the the custom ACPI file from [this repo](https://github.com/corot2a/Hackintosh-12700KF-B660M-MORTAR-6650XT/blob/main/EFI/OC/ACPI/SSDT-6650XT.aml) (Go give him some love).

- To make the external monitor have HiDPI, I had to use [this app](https://github.com/usr-sse2/RDM) and to control the brightness without the OSD controls, I had to use [this app](https://github.com/MonitorControl/MonitorControl).

- Sleep doesn't work. It works but randomly wakes up. The monitor stop working but the pc is still on. I don't know how to fix it.

- When it boots for the first time, if I did not add the `NVMeFix.kext` to the `EFI/OC/Kexts` folder, it doesn't recognize the storage, so add it if needed.

.
.
.

COMPLETE GUIDE...
