This repository contains a dual stack APN Apple Configuration Profile (`.mobileconfig`) for the EE (UK) cellular network.

## Overview

Modern "Carrier Bundle" updates from EE often provision devices with an IPv6-only connection. This profile overrides the default settings to force a **Dual-Stack (IPv4 and IPv6)** connection. This configuration resolves compatibility issues with legacy applications, certain VPN services, and specific gaming platforms that still require IPv4 connectivity (eg hotspotting PSP).

Whilst all other profiles I have seen fully disable IPv6, this runs both the newer IPv6 and older IPv4 at once.

It also includes a robust configuration for Multimedia Messaging Service (MMS).

## Configuration Details

This profile configures the `com.apple.cellular` payload with the following settings:

### 1. Cellular Data (APNs) & LTE Attach (AttachAPN)

Forces a Dual-Stack connection for both general data and the initial network attach by using EE's legacy authentication.

*   **APN Name:** `everywhere`
*   **Username:** `eesecure`
*   **Password:** `secure`
*   **Protocol Masks (Default, Roaming):** `3` (Enables both IPv4 and IPv6)

### 2. Picture Messaging (MMSAPN)

Configures settings required for sending and receiving picture messages (MMS).

*   **APN Name:** `eezone`
*   **MMSC URL:** `http://mms/`
*   **MMS Proxy:** `149.254.201.135:8080`
*   **Authentication:** Uses `eesecure`/`secure`.

*   **MMS User Agent Profile (`MMSUaprof`)**:
    *   **Value:** `https://www.apple.com/mms/uaprof.rdf`
    *   **Purpose:** This setting provides the carrier's MMS server with a "User Agent Profile" (UAProf). This profile tells the server exactly what the device (an iPhone) is capable of, such as screen size and supported image formats. This ensures that picture messages are reliably delivered and correctly formatted. The URL used is Apple's official standard.

## Installation

1.  Download the 'EEdualstackAPN.mobileconfig' file. 
2.  Open the file from the Files app on your iOS/iPadOS device.
3.  Go to **Settings > General > VPN & Device Management** to install the profile.

## Compatibility

*   **Network:** EE (UK).

**Note:** This profile is removable. To uninstall, go to **Settings > General > VPN & Device Management**.
