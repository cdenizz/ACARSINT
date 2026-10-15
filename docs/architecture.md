# Architecture

ACARSINT keeps signal demodulation in the upstream receiver programs. The application manages device profiles, receives decoder output, stores it locally and presents the retained evidence through a browser interface.

```mermaid
flowchart LR
    SDR[RTL-SDR and receiver profiles] --> AC[acarsdec]
    SDR --> VDL[dumpvdl2]
    SDR --> ADSB[readsb, Linux bundle]
    AC --> ING[Protocol-specific ingestion]
    VDL --> ING
    ADSB --> ING
    ING --> ADB[(ACARS and message SQLite)]
    ING --> VDB[(VDL2 SQLite)]
    ING --> SDB[(ADS-B SQLite)]
    ADB --> API[FastAPI on loopback]
    VDB --> API
    SDB --> API
    ADB --> DER[Decoders and derived analysis]
    VDB --> DER
    DER --> ADB
    API --> UI[JavaScript browser interface]
```

The final Windows receiver package provides `acarsdec` and `dumpvdl2`; its receiver notice says the included Dump1090 helper is not integrated as an ACARSINT ADS-B adapter. The native Linux package includes `readsb` integration. The diagram shows the Linux ADS-B path and is not a parity claim for Windows.

## Evidence layers

A retained source payload, deterministic parser fields, heuristic classification and derived event are different things. ACARSINT can display them together so a user can compare an interpretation with the original message. Historical classifier versions may disagree; current UI labels such as `Unknown`, `Observation` or `System fault` should be described as software output, not ground truth.

Some source archives contain a VDL2 frame and a corresponding ACARS application-message row. Those rows can represent the same reception. Registration/time overlap does not by itself prove a same-flight fusion. ADS-C positions transported in ACARS over VDL2 are not ADS-B observations.

SQLite stores are local and distinct for ACARS/messages, VDL2 and ADS-B observations. The UI reads through the local API. The historical databases used for this presentation contain no ADS-B track/state observations, so they do not substantiate a three-source historical example.
