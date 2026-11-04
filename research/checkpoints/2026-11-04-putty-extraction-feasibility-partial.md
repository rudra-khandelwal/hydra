# PuTTY 0.85 embedded-help extraction feasibility — partial result

**Date:** 4 November 2026  
**Research stream:** Direct official-publisher artifact analysis. This is not a Hydra-mediated download test.  
**Target:** Official PuTTY 0.85 64-bit x86 standalone `putty.exe`.  
**Status:** Partial feasibility assessment only. The requested report `embedded-help-extraction-feasibility.txt` was not completed or saved.

## Confirmed directory mapping for the default topic

The preceding `#SYSTEM` metadata inspection established that `/index.html` is the default help topic (record code 2, NUL-terminated UTF-8 value `index.html`).

The latest read-only inspection now reports the CHM directory entry for `/index.html` as:

- Section: **1**
- Compression: **MSCompressed/LZX**
- Logical uncompressed section offset: **0x0**
- Declared uncompressed length: **15,673 bytes**
- Independent raw executable file offset: **not provided by the directory entry**

This means the topic is not a section-0 uncompressed file and cannot be mapped to a raw file offset by simply adding its logical offset to the CHM data base.

## What remains unresolved

The read-only metadata command failed with a PowerShell parser error before returning validated reset-table values or a local-tool inventory.

Although existing reports identify the CHM structures/entries named `ResetTable`, `ControlData`, `SpanInfo`, and compressed `Content`, their payloads were **not validated in this step**.

The existing `#SYSTEM` and embedded-help parsers are raw-byte metadata parsers; they do not implement LZX decompression. Whether the 15,673-byte topic can be retrieved without processing preceding compressed data depends on the validated reset-table and compression-stream mapping. The current evidence does not settle that question.

CHM format documentation describes the relevant structures, but the documentation alone is not evidence of this particular archive's reset-table values or independent extraction feasibility.

## Failed step and evidence limits

- The intended feasibility-assessment command failed before producing the required reset-table values and local-tool inventory.
- No extraction or decompression occurred.
- No HTML, CSS, image, or other help content was read, rendered, or executed.
- No local feasibility report was saved.
- No new before/after executable hash was collected in this step. The prior checkpoint hash remains historical evidence, not a fresh verification for this step.
- The command failure was reported not to have modified the executable; however, a new integrity check remains outstanding.

References supplied for format context:
- https://www.nongnu.org/chmspec/latest/Internal.html
- https://github.com/wine-mirror/wine/blob/master/dlls/itss/chm_lib.c

## Current conclusion

**Extraction feasibility is undetermined.** The only confirmed new result is that `/index.html` is at logical offset `0x0` in the MSCompressed/LZX section, with declared uncompressed length 15,673 bytes. No claim is made about independent decompression, reset-table layout, or available local tools.

## Next permitted action

Retry only the metadata feasibility assessment using a corrected, minimal read-only PowerShell command. First inspect the exact parser error and existing parser/report structure. Validate the reset-table, ControlData, SpanInfo, and Content mapping against the bounded CHM resource before drawing conclusions. Inventory only tools already installed. Record size and SHA-256 before and after.

Do not decompress or extract anything; do not render help content; do not launch, load, or install PuTTY; do not install tools; do not modify Hydra or its configured sources. Any actual extraction requires a separate explicit approval after feasibility has been established.

## Project boundary

The Hydra download-path experiment remains blocked because no exact existing configured source entry has been verified to point to an official release or explicitly authorized distributor. PuTTY was downloaded directly from its official publisher and does not satisfy or count as a Hydra download-path test.
