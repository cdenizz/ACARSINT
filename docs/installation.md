# Installation

ACARSINT is available as private Windows x64 and native Linux x86_64 packages for authorized holders. This documentation repository contains no binaries and has no download link. Obtain the package through an owner-authorized private channel and compare its SHA-256 before extraction.

## Windows x64

Package: `ACARSINT-Core-v0.10.0-rc5.1-private-cold-photo-ui-20261015-win-x64.zip`

SHA-256: `dd6635d8eab6955ff2c103645b612486e73ab6f0223d6a06db6c48ddca38fe7e`

From PowerShell in the directory containing the authorized archive:

```powershell
Get-FileHash .\ACARSINT-Core-v0.10.0-rc5.1-private-cold-photo-ui-20261015-win-x64.zip -Algorithm SHA256
Expand-Archive -LiteralPath .\ACARSINT-Core-v0.10.0-rc5.1-private-cold-photo-ui-20261015-win-x64.zip -DestinationPath .\ACARSINT-RC5.1
Set-Location .\ACARSINT-RC5.1
.\ACARSINT.exe
```

Use a new extraction directory. The archive contains `ACARSINT.exe` at its root. Compare the displayed checksum with the value above before starting it.

1. Extract the ZIP into a new folder.
2. Run `ACARSINT.exe`. The application includes its Python runtime and required Python dependencies.
3. On first run, use the one-time token stored under `%LOCALAPPDATA%\ACARS Intelligence\run\initial-setup-token.txt`, then complete the browser Setup Wizard and create the administrator account. No default password is shipped.
4. Open Receiver Settings, select the intended SDR by serial when possible, then start the desired ACARS, VDL2 or configured Dump1090 ADS-B profile. The package does not install or change Windows USB drivers; install a compatible RTL-SDR driver separately if the device is not detected. The Dump1090 profile requires a verified device-index mapping and its own loopback HTTP port.
5. To stop the application, open **Settings**, select **Overview** and use **Shut down platform safely**. Wait for shutdown to finish before closing the runtime or powering down.

The default Windows data/configuration directory is `%LOCALAPPDATA%\ACARS Intelligence`. `ACARS_RUNTIME_ROOT` and `ACARS_CONFIG` can point to another writable location. Keep the runtime directory separate from the extracted application folder when managing an upgrade; preserve and back up its SQLite files.

The default browser interface is `http://127.0.0.1:8080/web/setup.html` for setup and `http://127.0.0.1:8080` afterward. If the selected runtime changes the API port, use that configured port.

The final Windows receiver bundle includes `acarsdec` 4.6, `dumpvdl2` 2.7.0, `libacars` 2.2.1, RTL-SDR 2.0.3 utilities and Dump1090 from pinned commit `8b5b46d8fe5b3ca1cb7d50f8aa4da25cb546a7a9` with the loopback listener patch. Its managed Dump1090/JSON path is present in the frozen receiver service and ADS-B ingester; the older receiver README is stale on that point. This guide does not claim a new RF test.

## Native Linux x86_64

Package: `ACARSINT-Core-v0.10.0-rc5.1-linux-x86_64.tar.gz`

SHA-256: `108cc332a84a650b7f3d35f05449a38f8ab131f07beb2ce53ee01bc36c754670`

The verified platform is Debian 12 x86_64 with glibc 2.36. Other glibc distributions have not been accepted; musl and ARM are not claimed. Python 3.12.14, application dependencies, `acarsdec`, `dumpvdl2`, `readsb` and RTL-SDR components are bundled. A browser is not bundled.

```sh
sha256sum ACARSINT-Core-v0.10.0-rc5.1-linux-x86_64.tar.gz
tar -xzf ACARSINT-Core-v0.10.0-rc5.1-linux-x86_64.tar.gz
cd ACARSINT-Core-v0.10.0-rc5.1-linux-x86_64
./acarsint doctor
./acarsint
```

Open `http://127.0.0.1:8080/web/setup.html`. Use the one-time token printed by the launcher or stored as `run/initial-setup-token.txt` under the runtime directory. Complete first-run setup and create the administrator account.

For managed shutdown:

```sh
./acarsint stop
```

`Ctrl+C` also requests managed shutdown. Avoid force-killing a process while it writes SQLite files.

The default Linux data directory is `$XDG_DATA_HOME/acars-intelligence`, or `~/.local/share/acars-intelligence` if `XDG_DATA_HOME` is unset. `ACARS_RUNTIME_ROOT` and `ACARS_CONFIG` can select separate paths. Preserve this runtime across upgrades, and back up databases with the application stopped.

### RTL-SDR USB access

The UI starts without an SDR and without administrator privileges. An administrator may need to install the bundled `udev/99-acarsint-rtl-sdr.rules`, reload udev, reconnect the device and grant the operator account USB access (often through `plugdev`). Resolve a DVB-driver conflict if the host kernel claims the receiver. Do not run the complete application as root to work around permissions. Select stable device serials in receiver profiles; device indexes can change.

From the extracted Linux package directory, the host administrator can install the bundled rule with:

```sh
sudo install -m 644 udev/99-acarsint-rtl-sdr.rules /etc/udev/rules.d/99-acarsint-rtl-sdr.rules
sudo udevadm control --reload-rules
```

Reconnect the receiver afterward. If group membership is changed, sign out and back in before starting the application. `./acarsint doctor` checks the packaged environment; a successful probe does not establish physical RF reception.

### Offline and optional photo lookup

Offline Mode is on in first-run configuration. Fresh photo discovery is opt-in. Online discovery and external image display require enabling online use in the selected runtime. Planespotters lookup requires a genuine operator contact set in the process environment variable `ACARS_PLANESPOTTERS_CONTACT`; do not put personal contact data in source or a distributed package. Existing local photo catalogs can be transferred with the photo-only exporter/importer after stopping the target application. Windows includes the tools under `tools/`; Linux exposes their help through `./acarsint python tools/export_aircraft_photo_metadata.py --help` and `./acarsint python tools/import_aircraft_photo_metadata.py --help`. Follow their disposable-database safeguards and never use an original archive as the import target.
