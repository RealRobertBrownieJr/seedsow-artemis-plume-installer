# Seedsow Artemis Installer — Plume USB Method

**Install the Artemis uploader into Seedsow Lullaby Demo using Plume USB and a modded Nintendo Switch 1 — without manually typing thousands of characters or needing a Raspberry Pi.**

This repository provides **117 numbered text files** containing a working Lua uploader, split into smaller chunks for transfer using Plume USB.

The goal is simple: save other people the time and frustration of manually entering the uploader through Seedsow Lua Editor V3.

> **IMPORTANT: Before transferring anything, edit `001.txt` to use your own PC's local IPv4 address. See the instructions below.**

## Requirements

### Nintendo Switch 2
- Seedsow Lullaby Demo installed
- Seedsow Lua Editor V3 installed in a Seedsow save slot
- Access to the Lua editor's text input

### Nintendo Switch 1
- A modded Switch 1 capable of running homebrew
- [Plume USB](https://github.com/MichelSama/plume-usb) installed
- A compatible USB cable/adapter to connect the Switch 1 to the Switch 2

### Windows PC
- Connected to the same local network as the Switch 2
- Access to PowerShell or Command Prompt
- The relevant Artemis installer files for completing the installation

## Step 1 — Find your PC's local IP address

**This step is essential. Do it before transferring `001.txt`.**

The uploader must know which PC to contact when sending its data.

1. On your Windows PC, press **Win + R**.
2. Type `cmd` and press Enter.
3. Run:

   ```powershell
   ipconfig
   ```

4. Look for the **IPv4 Address** of the network adapter you're using.

For example:

```text
Wireless LAN adapter Wi-Fi:

IPv4 Address . . . . . . . . . : 192.168.1.100
```

Your address will probably be different.

5. Open `001.txt` in Notepad or another plain-text editor.
6. Find the existing PC IP address.
7. Replace it with **your own local IPv4 address**.
8. Save the file.

**Do not remove quotation marks, brackets or other Lua syntax surrounding the address.**

Do not use your public internet IP address. The Switch 2 needs to reach your PC over the local network.


## Step 2 — Prepare Plume USB

1. Download and install [Plume USB](https://github.com/MichelSama/plume-usb) on your modded Switch 1.
2. Copy the **117 numbered text files** onto storage accessible to Plume.
3. Connect your Switch 1 to your Switch 2 using a compatible USB cable and adapter.
4. Launch Plume USB on the Switch 1.

Plume allows the Switch 1 to act as a USB keyboard and send text to another device.

This means you can enter the uploader into Seedsow without manually typing every character.

**Note:** USB compatibility can depend on your cable, adapter and hardware configuration.

## Step 3 — Open Seedsow Lua Editor V3

On your Switch 2:

1. Launch Seedsow Lullaby Demo.
2. Make sure you're using the correct Nintendo Switch user profile.
3. Load the Seedsow save containing **Lua Editor V3**.
4. Open the Lua editor's text input.
5. Make sure the input is ready to receive text from the connected USB keyboard.

Avoid entering extra characters before starting the transfer.

## Step 4 — Transfer all 117 files

Using Plume USB on your Switch 1:

1. Select `001.txt`, which should now contain your PC's correct local IP address.
2. Send its contents to the Seedsow Lua editor.
3. Continue with `002.txt`.
4. Repeat for every file in numerical order.
5. Finish with `117.txt`.

**The order matters.**

Do not skip, repeat or rearrange any chunks.

Each file contains part of the same Lua program, so even a small duplication or omission can break the uploader.

### Important transfer tips

- Start with `001.txt` and finish with `117.txt`.
- Make sure each chunk has finished transferring before sending the next.
- Avoid introducing extra line breaks or characters between chunks.
- If you're unsure whether a chunk transferred correctly, check before continuing rather than blindly sending it again.
- Verify the assembled script before saving it.

A duplicated chunk can be difficult to notice until you try to run the uploader.

## Step 5 — Save the completed uploader

Once all 117 files have been transferred:

1. Review the completed Lua script for obvious missing or duplicated text.
2. Save it to an available Seedsow slot.
3. Keep your original Lua Editor V3 save intact.

For the original tested setup, the uploader was saved in **slot 21**, with the Artemis launcher later installed in **slot 20**.

You can use different slots where supported, but make sure they match your installer configuration.

**Back up important saves before making changes.**

## Step 6 — Complete the Artemis installation

The Plume files handle the tedious text-entry portion of the setup.

For the remaining installation process, use the instructions and tools provided by the original developers:

- [Seedsow Lua Editor](https://github.com/DialingSpoon527/seedsow-lua-editor)
- [Artemis installer branch](https://github.com/DialingSpoon527/seedsow-lua-editor/tree/artemis-installer)
- [switch-artemis-launcher](https://github.com/alula/switch-artemis-launcher)

The Artemis installer must be configured with the correct PC IP address and destination save slot.

For example, the original tested configuration used:

| Setting | Tested configuration |
|---|---|
| Uploader save slot | `21` |
| Artemis launcher save slot | `20` |
| Installer sender port | `39000` |
| Artemis HTTP port | `8080` |

These are details from one working setup, not requirements for every installation.

Follow the upstream project's instructions if its configuration changes.

## Step 7 — Verify the HTTP launcher

After successfully installing the Artemis launcher:

1. Open its Seedsow save slot.
2. Press **Y** to start the HTTP server.
3. Make sure your Windows PC and Switch 2 can communicate over the local network.

You can test the connection from Windows PowerShell:

```powershell
curl.exe --max-time 5 http://SWITCH_IP:8080/status
```

Replace `SWITCH_IP` with the Switch 2's actual local IP address.

A working server should return a response identifying the Seedsow HTTP server.

**Security note:** The launcher exposes endpoints capable of executing Lua code. Only run it on a trusted local network, and do not expose port `8080` to the public internet.

## Troubleshooting

### The uploader cannot contact my PC

Check that:

- You edited `001.txt` before transferring it.
- The IP address belongs to your Windows PC.
- Your PC and Switch 2 can reach each other over the local network.
- The relevant installer is running and using the expected port.
- Windows Firewall isn't blocking the connection.

If your PC's IP changes, you may need to update the uploader configuration.

### The script has a syntax error

Possible causes include:

- A missing chunk
- A duplicated chunk
- Chunks transferred out of order
- Extra characters or line breaks
- Accidental modifications to the Lua code

Recheck the transfer sequence carefully.

### The completed script isn't exactly 3,668 characters

The tested version was 3,668 characters, but changing the IP address may change that number.

If the difference is larger than expected, check for missing or duplicated chunks.

### My Seedsow saves seem to have disappeared

Check that you launched Seedsow using the correct Switch user profile.

Saves are associated with individual user profiles, so selecting a different profile can make previously created slots appear unavailable.

### My Switch 1 isn't typing into the Switch 2

Check the USB cable and adapter, confirm Plume is running, and verify that the Lua editor's text field is active.

Not every USB connection or adapter will work as a keyboard connection.

## Credits

This method is built around the work of the original developers:

- **[MichelSama — Plume USB](https://github.com/MichelSama/plume-usb)** — USB keyboard functionality
- **[DialingSpoon527 — Seedsow Lua Editor](https://github.com/DialingSpoon527/seedsow-lua-editor)** — Lua editor and installer tools
- **[alula — switch-artemis-launcher](https://github.com/alula/switch-artemis-launcher)** — Artemis launcher

Full credit for the original software belongs to its respective authors and contributors.

This repository provides a community transfer method and documentation. It is not an official release of those projects.

## Disclaimer

This project is intended for homebrew research and experimentation on hardware you own.

It is **not affiliated with or endorsed by Nintendo**.

Experimental homebrew and exploit software can cause crashes, data loss or other unintended behaviour. Proceed at your own risk.

No Nintendo games, firmware, encryption keys or proprietary system files are intended to be distributed with this repository.

## Contributions

If you've tested this method with different hardware, USB adapters or software configurations, feedback is welcome.

Please report which setup worked for you, any problems you encountered, and any improvements that could make the transfer process easier for other users.

The aim is to make the Seedsow Artemis setup more accessible and less time-consuming for the community.
