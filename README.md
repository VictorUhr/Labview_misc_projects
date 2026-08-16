# LabVIEW Miscellaneous Projects

A collection of LabVIEW projects with Python integration, focusing on data acquisition, telemetry, and signal processing applications.

## 📋 Projects Overview

### 1. **Telemetry (Python → LabVIEW via Bluetooth)**
**Folder:** `Telemetry_python2LabVIEW_bluetooth_receiver/`

A Python-to-LabVIEW telemetry system that reads BLE (Bluetooth Low Energy) sensor data and streams it to LabVIEW via TCP framed JSON.

**Key Features:**
- BLE sensor data acquisition (supports 4 thermocouple devices)
- TCP socket server with framed JSON protocol
- LabVIEW Producer/Consumer design pattern implementation
- Supports multiple sensor indices with error code tracking
- ISO 8601 timestamp logging

**Tech Stack:**
- **Python:** Bleak (BLE library), asyncio, socket, struct, JSON
- **LabVIEW:** TCP communication, JSON parsing, type definitions
- **Data Format:** 4-byte big-endian length prefix + UTF-8 JSON payload

**Quick Start:**
```bash
# Install Python dependencies
pip install -r requirements.txt

# Run the Python telemetry receiver
python BLE_4TC_Receiver.py

# Then open and run Telemetry_project.lvproj in LabVIEW
```

**Documentation:** See `Telemetry_python2LabVIEW_bluetooth_receiver/labview/README.md` for detailed protocol specifications and troubleshooting.

---

### 2. **3D Accelerometer Plot (Cross-Time Analysis)**
**Folder:** `Accelerometer_3Dplot_crosstime/`

LabVIEW project for visualizing and analyzing 3D accelerometer data with cross-time plotting capabilities.

**Key Features:**
- Real-time 3D plot visualization
- FFT analysis of acceleration signals
- IEPE (Integrated Electronics Piezo-Electric) continuous input support
- Cross-time data analysis

**Components:**
- `IEPE - Continuous Input_tet.vi` — Continuous sensor input handler
- `FFTs.vi` — FFT processing and analysis
- Project files: `project_1.lvproj`, `project_1.lvlps`, `project_1.aliases`

---

### 3. **3-Vibration Sensors DAQ System**
**Folder:** `Labview_3vibrations_sensors_DAQ/`

Comprehensive LabVIEW DAQ system for 3-axis vibration monitoring with signal analysis and TDMS data logging.

**Key Features:**
- Multi-sensor DAQ (3 vibration sensors)
- FFT and envelope analysis
- TDMS file logging for long-term storage
- IEPE continuous input support
- Real-time signal visualization

**Components:**
- `IEPE - Continuous Input_tet.vi` — Continuous vibration acquisition
- `FFTs.vi` — Fast Fourier Transform analysis
- `Plot_FFT_Env.vi` — FFT and envelope plotting
- `save_tdms.vi` — TDMS data persistence
- Project files: `project_2.lvproj`, `project_2.lvlps`, `project_2.aliases`

---

## 🛠 Prerequisites

### Global Requirements
- **LabVIEW** (2018 or later recommended)
- **Python** 3.7 or higher (for telemetry project)
- **DAQ Hardware** (for accelerometer/vibration projects)
  - IEPE sensor support
  - National Instruments DAQ device (e.g., USB-6210, cDAQ)

### Python Environment (Telemetry Project)
```bash
pip install -r Telemetry_python2LabVIEW_bluetooth_receiver/requirements.txt
```

**Dependencies:**
- `bleak >= 0.20.2` — Bluetooth Low Energy client library

---

## 📁 Directory Structure

```
Labview_misc_projects/
├── README.md                                           # This file
├── Accelerometer_3Dplot_crosstime/                     # 3D accelerometer visualization
│   ├── FFTs.vi
│   ├── IEPE - Continuous Input_tet.vi
│   └── project_1.*
├── Labview_3vibrations_sensors_DAQ/                    # 3-sensor vibration DAQ system
│   ├── FFTs.vi
│   ├── IEPE - Continuous Input_tet.vi
│   ├── Plot_FFT_Env.vi
│   ├── save_tdms.vi
│   └── project_2.*
└── Telemetry_python2LabVIEW_bluetooth_receiver/        # Python BLE → LabVIEW telemetry
    ├── BLE_4TC_Receiver.py                             # Main Python script
    ├── requirements.txt
    ├── labview/                                        # LabVIEW VIs and type defs
    │   ├── Data_struct_from_py_telem.ctl
    │   ├── telemetry setup.ctl
    │   ├── Get data from ProducerTele.vi
    │   ├── TCP data from py script.vi
    │   ├── Telemetry_ProducerConsumer.vi
    │   ├── README.md                                   # Detailed telemetry documentation
    │   ├── labview version 2018/
    │   └── labview version 2020/
    ├── old/                                            # Legacy BLE examples
    └── tests/                                          # Unit tests
        └── test_BLE_4TC_Receiver.py
```

---

## 🚀 Getting Started

### For Telemetry Project
1. Ensure Python environment is set up with required dependencies
2. Configure sensor MAC addresses in `BLE_4TC_Receiver.py` if needed
3. Start the Python telemetry script
4. Open and run the LabVIEW project
5. Monitor incoming telemetry data in the LabVIEW UI

### For Accelerometer/Vibration Projects
1. Connect DAQ hardware and sensors
2. Open the respective LabVIEW project (`.lvproj`)
3. Configure IEPE settings as needed
4. Run the main VI to start acquisition and visualization

---

## 📖 Additional Documentation

- **Telemetry Protocol:** See `Telemetry_python2LabVIEW_bluetooth_receiver/labview/README.md` for:
  - TCP framing specification
  - JSON schema details
  - Troubleshooting guide
  - Example payloads

---

## ⚙️ Technical Notes

### Telemetry System
- **TCP Binding:** `localhost:8089` (configurable in Python script)
- **Data Format:** 4-byte big-endian length prefix + UTF-8 JSON
- **Telemetry Fields:** index, tc_values (6x floats), counter, timestamp, error_code
- **Latency:** Per-message connection model; optimize for persistent sockets if needed

### DAQ Systems
- **Signal Processing:** FFT and envelope analysis included
- **Data Persistence:** TDMS format for long-term storage and post-processing
- **Visualization:** Real-time 3D plotting with cross-time analysis

---

## 📝 Notes

- LabVIEW version compatibility: Projects available for both 2018 and 2020 versions (telemetry)
- Bluetooth devices require proper driver support on the host OS (Windows/Linux/macOS)
- For high-throughput applications, consider optimizing the Producer/Consumer queue depth
- TDMS files can be opened and analyzed using NI DIAdem or Python libraries

---

## 🔗 Related Resources

- [Bleak BLE Library](https://github.com/hbldh/bleak)
- [LabVIEW JSON Support](https://www.ni.com/en-us/support/documentation/supplemental/06/json-support-in-labview.html)
- [National Instruments DAQ Documentation](https://www.ni.com/en-us/support/documentation.html)


