# Installation

ACARSINT is available as private Windows x64 and native Linux x86_64 packages for authorized holders. This documentation repository contains no binaries and has no download link. Obtain the package through an owner-authorized private channel and compare its SHA-256 before extraction.

## Windows x64

Package: `ACARSINT-Core-v0.10.0-rc5.1-private-cold-photo-ui-20261015-win-x64.zip`

SHA-256: `dd6635d8eab6955ff2c103645b612486e73ab6f0223d6a06db6c48ddca38fe7e`

1. Extract the ZIP into a new folder.
2. Run `ACARSINT.exe`. The application includes its Python runtime and required Python dependencies.
3. On first run, use the one-time token stored under `%LOCALAPPDATA%\ACARS Intelligence\run\initial-setup-token.txt`, then complete the browser Setup Wizard and create the administrator account. No default password is shipped.
4. Open Receiver Settings, select the intended SDR by serial when possible, then start the desired ACARS or VDL2 profile. The package does not install or change Windows USB drivers; install a compatible RTL-SDR driver separately if the device is not detected.
5. To stop the application, open the Admin page from the **More** menu and use **Shut down platform safely**. Wait for shutdown to finish before closing the runtime or powering down.

The default Windows data/configuration directory is `%LOCALAPPDATA%\ACARS Intelligence`. `ACARS_RUNTIME_ROOT` and `ACARS_CONFIG` can point to another writable location. Keep the runtime directory separate from the extracted application folder when managing an upgrade; preserve and back up its SQLite files.

The final Windows receiver bundle includes `acarsdec` 4.6, `dumpvdl2` 2.7.0, `libacars` 2.2.1 and RTL-SDR 2.0.3 utilities. The final receiver notice does not claim a working ACARSINT ADS-B/readsb adapter for this Windows candidate.

## Native Linux x86_64

Package: `ACARSINT-Core-v0.10.0-rc5.1-linux-x86_64.tar.gz`

SHA-256: `108cc332a84a650b7f3d35f05449a38f8ab131f07beb2ce53ee01bc36c754670`

The verified platform is Debian 12 x86_64 with glibc 2.36. Other glibc distributions have not been accepted; musl and ARM are not claimed. Python 3.12.14, application dependencies, `acarsdec`, `dumpvdl2`, `readsb` and RTL-SDR components are bundled. A browser is not bundled.

```sh
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

### Offline and optional photo lookup

Offline Mode is on in first-run configuration. Fresh photo discovery is opt-in. Online discovery and external image display require enabling online use in the selected runtime. Planespotters lookup requires a genuine operator contact set in the process environment variable `ACARS_PLANESPOTTERS_CONTACT`; do not put personal contact data in source or a distributed package. Existing local photo catalogs can be transferred with the photo-only tools under `app/tools/` after stopping the target application. Follow their disposable-database safeguards and never use an original archive as the import target.
