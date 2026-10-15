# Limitations and release boundaries

ACARSINT RC5.1 is frozen. The packages are private, and this repository does not distribute Core source or binaries.

## Platform and hardware

- **Native Linux:** packaged acceptance passed on Debian 12 x86_64 / glibc 2.36. ARM, musl and other Linux distributions are not claimed as tested.
- **Linux SDR:** physical RTL-SDR reception, simultaneous physical multi-SDR use, hot-unplug and RF gain/PPM calibration were not tested on Linux. Linux acceptance used decoder probes and labeled synthetic fixtures; neither is physical RF evidence.
- **Windows ADS-B:** the final Windows candidate bundles a Dump1090 helper executable, but the accompanying receiver documentation says there is no integrated ACARSINT ADS-B/readsb adapter in that candidate. The native Linux distribution includes `readsb` ingestion.
- **Windows/Linux parity:** check the private package acceptance notes before assuming receiver paths and adapters are available on both systems.

## Historical archive

The analyzed archive has 125,050 message rows, including 73,407 native `acarsdec` records and 51,643 VDL2 bridge rows. A bridge row can be the same VDL2-carried ACARS reception represented in another table; it must not be added as an independent reception.

The supplied ADS-B database has no aircraft-state, track-point or Comm-B observations. Its large snapshot counter is a polling count, not decoded aircraft or messages. The supplied historical files therefore do not prove a three-protocol ACARS/VDL2/ADS-B fusion result. Datalink observation tables are also empty.

Native-decoder JSON, timestamps and available signal/FEC fields support decoder-origin provenance. The work did not independently audit every historical reception against IQ or an acquisition log. The absence of an explicit synthetic/replay marker cannot rule out an unmarked import.

## Interpretations and maps

Decoder output, heuristic classifications, model predictions and derived events are distinct evidence. The preserved maintenance message names components; it does not prove a confirmed failure, cause or repair. A classifier score is not a calibrated probability. The free-text example is readable, although stored classifier fields disagree and the author is not independently known.

The application can render recorded historical positions, but a configured basemap or local tile pack is needed for map tiles. This repository omits a map screenshot because the available private capture had no basemap and showed a precise historic track. Position paths should not be described as continuous surveillance or ADS-B when their source is ACARS/ADS-C.

Photo discovery is optional. Offline and privacy settings govern remote lookups and image display. Provider access can be denied; no screenshot here contains aircraft photos or claims a photo provider worked.

## Licensing

This presentation repository has no `LICENSE` file and grants no license to use ACARSINT Core. The private release notices identify GPL decoders and other third-party components. The final acceptance report leaves Core license selection and complete third-party redistribution/corresponding-source review unresolved. The private software packages are not cleared for public redistribution, and no binaries are attached here. Individual upstream components retain their own licenses.
