# Limitations and release boundaries

ACARSINT RC5.1 is frozen. The packages are private, and this repository does not distribute Core source or binaries.

## Platform and hardware

- **Native Linux:** packaged acceptance passed on Debian 12 x86_64 / glibc 2.36. ARM, musl and other Linux distributions are not claimed as tested.
- **Linux SDR:** physical RTL-SDR reception, simultaneous physical multi-SDR use, hot-unplug and RF gain/PPM calibration were not tested on Linux. Linux acceptance used decoder probes and labeled synthetic fixtures; neither is physical RF evidence.
- **Windows ADS-B:** the packaged receiver service supports the Dump1090 engine and its loopback JSON ingestion. An older receiver README conflicts with that implementation; the third-party receiver notice describes the adapter and patch. The final photo acceptance did not repeat its physical RF test. Linux uses `readsb`.
- **Windows/Linux parity:** check the private package acceptance notes before assuming receiver paths and adapters are available on both systems.

## Historical archive

The analyzed archive has 125,050 message rows, including 73,407 native `acarsdec` records and 51,643 VDL2 bridge rows. Its separate VDL2 database contains 18,772 frames. A bridge row can be the same VDL2-carried ACARS reception represented in another table; it must not be added as an independent reception.

The supplied ADS-B database has no aircraft-state, track-point or Comm-B observations. Its large snapshot counter is a polling count, not decoded aircraft or messages. The supplied historical files therefore do not prove a three-protocol ACARS/VDL2/ADS-B fusion result. Datalink observation tables are also empty.

Native-decoder JSON, timestamps and available signal/FEC fields support decoder-origin provenance. The work did not independently audit every historical reception against IQ or an acquisition log. The absence of an explicit synthetic/replay marker cannot rule out an unmarked import.

## Interpretations and maps

Decoder output, heuristic classifications, model predictions and derived events are distinct evidence. The preserved maintenance message names components; it does not prove a confirmed failure, cause or repair. A classifier score is not a calibrated probability. The free-text example is readable, although stored classifier fields disagree and the author is not independently known.

The application renders recorded historical positions with their source context. The current tour visibly loaded genuine OpenStreetMap tiles through the application proxy and retained ACARS positions. Publication captures hide the exact marker, coordinates and timing. A drawn connection between retained points is not continuous surveillance; ACARS/ADS-C positions must not be described as ADS-B observations.

Photo discovery is optional. Offline/privacy settings govern remote lookups and image display, and providers can deny access. Frozen package acceptance covered legacy JetPhotos display and fresh Planespotters discovery; the latter supplied 200-pixel thumbnails. This historical tour used existing exact-registration catalog metadata with fresh discovery disabled.

## Screenshots and aircraft photography

Published screenshots are authentic application captures with identities, exact timing, precise positions, private endpoints and sensitive payload spans permanently masked. A few views are cropped to keep the relevant workspace in frame without empty catalog-photo panels; no underlying records or decoder results were changed.

The local legacy photo catalog remains supported, but third-party photographs are not included in this repository because reuse permission for the selected images has not been obtained. JetPhotos’ terms describe site use as personal and non-commercial and state that photos remain the property of their photographer or other rights holder ([terms](https://www.jetphotos.com/terms.php)). Access to a photo page does not grant permission to republish its image.
## Licensing

This presentation repository has no `LICENSE` file and grants no license to use ACARSINT Core. The private release notices identify GPL decoders and other third-party components. The final acceptance report leaves Core license selection and complete third-party redistribution/corresponding-source review unresolved. The private software packages are not cleared for public redistribution, and no binaries are attached here. Individual upstream components retain their own licenses.
