# BACnet Device Discovery and Environmental Sensor Simulator

A Python-based BACnet implementation for device discovery, control operations, and environmental sensor simulation.

## Features

### BACnet Device Discovery & Control System
- **Device Discovery**: Automatic BACnet device discovery using Who-Is requests
- **Object Operations**: Read/write operations for analogInput, analogValue, binaryValue objects
- **Async Support**: Non-blocking network operations
- **Error Handling**: Comprehensive error management

### Environmental Sensor Simulator
- **Sensors**: Frequency (Hz), Barometric pressure (Pa), Humidity (%), Temperature (°C), Gas resistance (Ω)
- **Heating Control**: Binary outputs for 2-room heating system
- **Real-time Updates**: Continuous sensor value simulation with realistic variations
- **Status Monitoring**: Binary inputs for radiator state feedback

## Installation

### Prerequisites
- Python 3.7+
- Network access to BACnet devices

### Install Dependencies
```bash
pip install BAC0 netifaces
```

### BACnet Simulator Setup

#### Option 1: YABE (Yet Another BACnet Explorer)
1. Download from: https://sourceforge.net/projects/yetanotherbacnetexplorer/
2. Extract and run `Yabe.exe`
3. Configure: Device ID: 1234, IP: 192.168.1.9, Port: 47808

#### Option 2: BACnet Stack Simulator
```bash
git clone https://github.com/bacnet-stack/bacnet-stack.git
cd bacnet-stack
make
./bin/bacserv 1234
```

#### Option 3: Use Provided Python Simulator
```python
python bacnet_simulator.py
```

## Usage

### Jupyter Notebook

#### Cell 1: Device Discovery & Control
```python
# Paste content from paste.txt
# Run complete example
await complete_example()
```

#### Cell 2: Environmental Simulator
```python
# Paste content from paste-2.txt
# Runs continuously, press Ctrl+C to stop
```

### Python Scripts
```bash
# Device discovery and control
python bacnet_discovery.py

# Environmental simulator
python bacnet_simulator.py
```

### Code Examples

#### Device Discovery
```python
bacnet = initialize_bacnet_connection("192.168.1.9/24")
devices = await discover_bacnet_devices(bacnet)
```

#### Read Object
```python
value = await read_object_property(bacnet, "192.168.1.9:47808", "analogInput", 40, "presentValue")
```

#### Write Object
```python
await write_object_value(bacnet, "192.168.1.9:47808", "analogValue", 0, 25.0)
```

## Configuration

### Network Settings
```python
IP_ADDRESS = "192.168.1.9/24"
DEVICE_PORT = 47808
DEVICE_ID = 3056486
```

### Simulator Objects

| Instance | Type | Name | Description |
|----------|------|------|-------------|
| 10 | analogInput | Frequency | AC power frequency (49.5-50.5 Hz) |
| 20 | analogInput | Barometer | Atmospheric pressure (99-103 kPa) |
| 30 | analogInput | Humidity | Relative humidity (30-70%) |
| 40 | analogInput | Temperature | Ambient temperature (18-26°C) |
| 50 | analogInput | GasResistance | Air quality sensor (40-80 kΩ) |
| 10 | binaryOutput | RoomOneHeatingEnabled | Room 1 heating control |
| 20 | binaryOutput | RoomTwoHeatingEnabled | Room 2 heating control |
| 10 | binaryInput | RoomOneRadiatorState | Room 1 radiator status |
| 20 | binaryInput | RoomTwoRadiatorState | Room 2 radiator status |

## API Reference

### Core Functions

#### `initialize_bacnet_connection(ip_address)`
Initialize BACnet network connection
- **Parameters**: `ip_address` (str) - IP with subnet mask
- **Returns**: BAC0 connection object

#### `discover_bacnet_devices(bacnet)`
Discover devices using Who-Is request
- **Parameters**: `bacnet` - BAC0 connection object
- **Returns**: List of discovered devices

#### `read_object_property(bacnet, device_address, object_type, instance, property)`
Read specific property from BACnet object
- **Returns**: Property value or None

#### `write_object_value(bacnet, device_address, object_type, instance, value)`
Write value to BACnet object
- **Returns**: Boolean success status

### Supported Object Types
- `analogInput` - Read-only analog values (sensors)
- `analogValue` - Read-write analog values (setpoints)
- `binaryInput` - Read-only binary values (switches)
- `binaryOutput` - Binary output control (relays)

## Troubleshooting

### Common Issues
- **Connection Errors**: Check network connectivity and firewall (UDP port 47808)
- **Device Discovery Fails**: Verify BACnet devices are running and on same subnet
- **Read/Write Errors**: Check object existence and instance numbers

### Network Requirements
- Allow UDP traffic on port 47808
- Ensure devices are on same subnet
- Administrator privileges may be required

### Debug Mode
```python
import logging
logging.basicConfig(level=logging.DEBUG)
```
