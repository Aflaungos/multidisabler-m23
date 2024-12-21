## multidisabler for Samsung Galaxy M23

Enables write access to / (system partition), /product and /vendor, converts / (system) file system to ext4
(otherwise you may hit a bootloop after modifying / because f2fs refuses to mount r/o with dirty journal),
disables encryption of /data, disables stock recovery restoration and disables other Samsung lockup
anti-features usually disabled by other multidisablers: Vaultkeeper, proca, TLC HDM/ICCC/KG, CASS, WSM, FRP.

Instructions:

- Unlock bootloader
- Install TWRP
- Boot into recovery WITHOUT first rebooting to system, otherwise the stock firmware will remove TWRP and restore stock Recovery.
  To do it, reboot the phone with a connected USB cable and volume up and power keys pressed right after Download Mode.
- IF TWRP doesn't mount your /data (if you don't see your files from the internal flash) - wipe data partition: Wipe > Format Data
- Then EITHER take [multidisabler-a73-v5.zip](multidisabler-a73-v5.zip) (it just contains the [multidisabler](multidisabler) script as `META-INF/com/google/android/update-binary`), copy it to TWRP and install it
- OR copy [multidisabler](multidisabler) to TWRP and just run it in the console. You can use TWRP's terminal or even adb shell to TWRP from your PC:
  ```
  adb push multidisabler /tmp/
  adb shell
  sh /tmp/multidisabler
  ```
- IF you didn't wipe data at the step 4, then wipe it: Wipe > Format Data
- Reboot into system
- If something goes wrong you can restore TWRP backup or just flash with Odin (or Heimdall in Linux: https://git.sr.ht/~grimler/Heimdall)
- After that you'll be able to remount FS to R/W with `mount -o remount,rw /` (or /vendor, /product) under root.

If you hit a
bootloop, you should copy `/proc/last_kmsg` from TWRP after an unsuccessful boot PLUS collect `adb logcat`
during boot and send both to me (@Aflaungos in telegram).
