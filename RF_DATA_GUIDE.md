# CardiffNav: Raw GNSS RF Data Usage Guide

## 1. Overview

This document provides a detailed guide for using the raw Radio Frequency (RF) signal data included in the CardiffNav dataset. This data was captured using a **Spirent GSS6450** RF recorder and has been converted from its proprietary binary format into the standard, accessible HDF5 (`.hdf5`) format.

Each HDF5 file encapsulates the raw In-phase and Quadrature (IQ) data, Automatic Gain Control (AGC) information, and all relevant metadata (such as center frequencies, bandwidths, and timestamps) into a single, self-describing file.

- **Example Dataset File:** `Dataset_250717135306.hdf5`

## 2. Recording Details

- **Recording Equipment:** Spirent GSS6450
- **Original Filename:** `250717135306`
- **Recording Date:** July 17, 2025
- **Recording Start Time (UTC):** 13:53:06
- **Number of Channels Recorded:** 2

## 3. HDF5 File Structure

All data within the file is organized under a top-level group named `RF Recorder`. Its internal structure is as follows:

- **📂 Group: `RF Recorder`**
  - **📄 Dataset: `IQ Data`**
    - **Description:** The core IQ RF signal data, arranged as an N x 4 matrix.
    - **Shape:** `(N, 4)`, where N is the total number of samples.
    - **Data Type:** `int8` (8-bit signed integer, range -8 to 7).
    - **Column Definition:** `[Channel 1 I, Channel 1 Q, Channel 2 I, Channel 2 Q]`

  - **📄 Dataset: `Automatic Gain Control`**
    - **Description:** The recorder's AGC output during the recording session.
    - **Shape:** `(M, 8)`, where M is the number of AGC log entries.
    - **Data Type:** `uint32`
    - **Column Definition:**
      1. XFER Count for FPGA A
      2. AGC Readback for Channel 1
      3. AGC Readback for Channel 2
      4. AGC Readback for Channel 3
      5. AGC Readback for Channel 4
      6. LNA Setting for RF1 Input
      7. LNA Setting for RF2 Input
      8. LNA Setting for RF3 Input

  - **📄 Dataset: `Channel Frequencies`**
    - **Description:** The center frequency for each recorded channel.
    - **Shape:** `(2,)`
    - **Data Type:** `float64`
    - **Unit:** Hertz (Hz)

  - **📄 Dataset: `Channel Bandwidths`**
    - **Description:** The bandwidth for each recorded channel, which is equivalent to its sampling rate.
    - **Shape:** `(2,)`
    - **Data Type:** `float64`
    - **Unit:** Hertz (Hz)

  - **📄 Dataset: `Recorder Times`**
    - **Description:** Unix timestamps for key recording events.
    - **Shape:** `(3,)`
    - **Data Type:** `float64`
    - **Order:** `[Start Time (UTC), Local Start Time, Local Stop Time]`

## 4. Data Characteristics

- **Bit Depth:** The original data was recorded at 4-bit resolution. In this HDF5 file, the samples have been unpacked and are stored as **8-bit signed integers (`int8`)** with a value range from -8 to 7.
- **Channel Configuration:**
  - **Channel 1 (L1 Band):** Center Freq 1575.420 MHz, Bandwidth/Sample Rate 10.0 MHz
  - **Channel 2 (L2 Band):** Center Freq 1227.600 MHz, Bandwidth/Sample Rate 30.0 MHz

## 5. How to Use

We recommend using Python with the `h5py` and `numpy` libraries to access and process the data.