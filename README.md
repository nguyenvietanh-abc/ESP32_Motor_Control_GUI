# ESP32_Motor_Control_GUI
# ESP32 Motor Speed Monitor - Qt GUI Application

## Tổng quan dự án
Ứng dụng GUI Qt 5.15 cross-platform trên Linux để điều khiển và giám sát motor DC thông qua ESP32. Hệ thống cung cấp giao diện trực quan cho real-time motor speed control với encoder feedback monitoring.

## Kiến trúc GUI

### 1. **Connection Management Panel**
- **Serial Port Detection**: Auto-detect available COM ports với refresh functionality
- **Baud Rate Selection**: Configurable từ 9600 đến 115200 bps (default: 115200)
- **Connection Control**: Connect/Disconnect buttons với real-time status indicator
- **Status Display**: Visual connection status (Green: Connected, Red: Disconnected)

### 2. **Motor Speed Control Interface**
- **Interactive Slider**: Horizontal QSlider (0-100%) với tick marks mỗi 10%
- **Precision Input**: QSpinBox đồng bộ với slider cho precise value entry
- **Command Transmission**: Send button gửi PWM command format `SPEED:{value}` qua UART
- **Visual Feedback**: Real-time speed percentage display với styled label

### 3. **Real-time Motor Status Dashboard**
- **RPM Display**: QLCDNumber với digital style (black background, lime color) hiển thị current RPM
- **Progress Visualization**: QProgressBar mapping RPM to percentage (max 5000 RPM)
- **Statistical Analysis**: Auto-calculated Min/Max/Average speed tracking
- **Performance Metrics**: Continuous monitoring với rolling window statistics

### 4. **Time-series Data Visualization**
- **QChart Integration**: Professional charting với QLineSeries plotting
- **Real-time Plotting**: Live RPM data với QDateTimeAxis (hh:mm:ss format)
- **Data Management**: Sliding window với maximum 100 data points
- **Auto-scaling**: Dynamic axis adjustment theo incoming data range
- **Theme**: BlueCerulean theme với orange plot line (RGB: 255,100,0)

### 5. **Communication & Logging System**
- **UART Protocol**: Bidirectional serial communication với ESP32
- **Data Parsing**: Protocol handler cho `RPM:{value}` response format
- **Timestamped Logging**: QTextEdit với auto-scroll displaying sent commands và received data
- **Error Handling**: Comprehensive serial port error detection và user notification
- **Log Management**: Clear log functionality với persistent session data

## Technical Implementation
- **Framework**: Qt 5.15 với QtCharts module
- **Architecture**: Model-View pattern với centralized data management
- **Threading**: QTimer-based updates (100ms intervals) cho smooth real-time performance
- **Memory Management**: Efficient data structure với circular buffer implementation
- **Cross-platform**: Linux-optimized build với portable codebase
