# Enhanced Anomaly Detection in IoT Using FPGA

## Overview
This project implements a real-time anomaly detection system for IoT networks using FPGA hardware acceleration. The system utilizes a PYNQ Z2 FPGA board to detect potentially malicious network traffic patterns within microseconds, demonstrating the benefits of hardware acceleration for time-critical security applications.

![System Overview](https://github.com/YourUsername/FPGA-IoT-Anomaly-Detection/raw/main/images/system-overview.png)

## Key Features
- Real-time anomaly detection in IoT network traffic
- Hardware-accelerated neural network inference on FPGA
- GPU-based neural network training pipeline
- Python/PYNQ interface for data processing and FPGA control
- Visual indicator system (LED) for immediate anomaly alerts
- Microsecond detection speeds, significantly outperforming traditional processing approaches

## Technologies
- **Hardware**: PYNQ Z2 FPGA board (Zynq SoC platform)
- **Development Tools**: Vivado Design Suite (VHDL implementation)
- **Programming Languages**: Python, VHDL
- **Frameworks**: PYNQ, Jupyter Notebooks
- **Dataset**: IoT-23 (labeled dataset with malicious and benign IoT network traffic)
- **Machine Learning**: Artificial Neural Networks (ANN)

## Implementation Details

### Architecture
The system operates on a two-stage process:
1. **Training Phase**: GPU-based neural network model development using the IoT-23 dataset
2. **Inference Phase**: FPGA-accelerated anomaly detection using the trained model

The FPGA design includes:
- Input/output ports for clock, reset, data, and anomaly detection flags
- AXI-based interface for high-speed data transfer
- Hardware-optimized neural network implementation

### Dataset
The IoT-23 dataset contains over 325 million records of network traffic data with 18 features per record. The data is labeled into 16 categories grouped into 5 main classes:
- Command and Control (C&C) malware traffic
- DDoS attacks
- Benign traffic
- Okiru
- PartOfAHorizontalPortScan (PHPS)

### Data Flow
1. Python script reads binary data from SD card
2. Data is transmitted to FPGA via AXI interface
3. FPGA processes data through neural network implementation
4. Anomaly detection results trigger visual indicators (LEDs)

## Results
- Successfully detected anomalies within microseconds
- Hardware acceleration provided significant performance improvements over traditional processing
- The PYNQ framework provided a flexible development environment for rapid prototyping and testing

## Setup Instructions

### Prerequisites
- PYNQ Z2 FPGA board
- Vivado Design Suite (2021.1 or later)
- Python 3.8+
- Jupyter Notebook
- IoT-23 dataset (preprocessed)

### Installation
1. Clone this repository:
   ```
   git clone https://github.com/YourUsername/FPGA-IoT-Anomaly-Detection.git
   cd FPGA-IoT-Anomaly-Detection
   ```

2. Download and prepare the IoT-23 dataset:
   ```
   # Script to download and preprocess the dataset
   python scripts/prepare_dataset.py
   ```

3. Generate the FPGA bitstream:
   ```
   # Either use the provided bitstream or generate a new one using Vivado
   # Instructions in the documentation folder
   ```

4. Transfer the bitstream and Jupyter notebooks to the PYNQ Z2 board

### Running the Detection System
1. Connect to the PYNQ Z2 board via Jupyter Notebook interface
2. Open the `anomaly_detection.ipynb` notebook
3. Follow the instructions in the notebook to load the bitstream and run the detection system

## Code Sample
Here's a snippet of the Python code used for detecting anomalies:

```python
# Function to randomly check for attacks within the dataset
def random_check_for_attacks(df, num_checks=10):
    for _ in range(num_checks):
        # Randomly select an entry from the dataset
        random_entry = df.sample()
        print(f"Checking entry: {random_entry}")
        
        # Check if the randomly selected entry is labeled as 'Attack'
        if 'Attack' in random_entry['Label'].values[0]:
            print("Attack detected!")
            blink_led(0)  # Blink the first LED (LED 0)
            return  # Stop checking after detecting an attack
        else:
            print("No attack detected in this entry.")
            
    # If no attack is found after all checks
    blink_led(1, times=2, interval=1)  # Blink the second LED (LED 1) twice
```

## Project Structure
```
FPGA-IoT-Anomaly-Detection/
├── hardware/
│   ├── vivado/           # Vivado project files
│   ├── vhdl/             # VHDL source files
│   └── constraints/      # XDC constraint files
├── software/
│   ├── notebooks/        # Jupyter notebooks
│   └── python/           # Python source files
├── data/
│   └── preprocessed/     # Preprocessed IoT-23 dataset
├── docs/                 # Documentation
├── images/               # Images for documentation
└── README.md             # This file
```

## Future Improvements
- Implement more sophisticated neural network architectures
- Explore additional feature extraction methods
- Develop a more comprehensive alert system
- Optimize FPGA resource utilization
- Extend the system to handle multiple IoT protocols

## Team
- Sai Prudvi Ela - Software Implementation
- Aparna Peddireddy Nadipolla - Data preparation and model training
- Ajay Tammuluri - Hardware Implementation
- Chaturta Papajjagari - Hardware Implementation
- Harshitha Juvvala - Data preparation and model training

## References
1. Stratosphere Laboratory. (2021). A labeled dataset with malicious and benign IoT network traffic.
2. Chen, Y., & Luo, Y. (2019). FPGA-based implementation for real-time anomaly detection using machine learning.
3. Wang, B., & Srinivasan, R. (2018). A review of anomaly detection systems in cloud networks and IoT using machine learning techniques.

## License
This project is licensed under the MIT License - see the LICENSE file for details.
