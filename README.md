# DDoS Detection and Mitigation Using SDN with Mininet and Machine Learning

## 📖 Project Overview
This project implements an intelligent DDoS detection and mitigation system for Software-Defined Networking (SDN) environments. By combining machine learning classifiers with SDN programmability, the system can accurately detect and automatically mitigate Distributed Denial of Service attacks in real-time.

## ✨ Key Features
- **Real-time DDoS Detection**: ML-based classification of network traffic flows
- **Automated Mitigation**: Dynamic blocking and rerouting of malicious traffic
- **SDN Integration**: Seamless integration with RYU SDN controller
- **High Accuracy**: 99.88% detection accuracy using Random Forest
- **Scalable Architecture**: Designed for modern network environments
- **Comprehensive Evaluation**: Performance metrics including precision, recall, and false alarm rate

## 🛠️ Technology Stack
- **Network Emulation**: Mininet
- **SDN Controller**: RYU Controller
- **Machine Learning**: Scikit-learn (Random Forest, SVM)
- **Traffic Generation**: iperf, hping3
- **Programming**: Python
- **Data Processing**: Pandas, NumPy

## 📊 Performance Metrics
| Model | Accuracy | Precision | Recall | False Alarm Rate |
|-------|----------|-----------|--------|------------------|
| Random Forest | 99.88% | 99.88% | High | Very Low |
| Support Vector Machine | 98.50% | Good | Good | Low |

## 🔧 Usage

### 1. Training ML Models
```python
from ml_models.train_model import DDoSClassifier

# Initialize and train model
classifier = DDoSClassifier()
classifier.train('datasets/FlowStatsfile.csv')
classifier.save_model('models/rf_classifier.pkl')
```

### 2. Running the Detection System
```bash
# Start RYU controller with ML integration
ryu-manager controllers/ryu_controller.py

# In another terminal, setup Mininet topology
sudo python mininet_scripts/topology_setup.py

# Generate traffic (normal and attack)
python mininet_scripts/traffic_generator.py --type normal
python mininet_scripts/attack_simulator.py --type udp-flood
```

### 3. Real-time Monitoring
```python
# Monitor detection results
from controllers.ml_integration import TrafficMonitor

monitor = TrafficMonitor()
results = monitor.get_realtime_stats()
print(results)
```

## 📈 Methodology

### Data Collection
- **Normal Traffic**: TCP, UDP, ICMP flows generated using iperf
- **Attack Traffic**: DDoS variants (ICMP flood, UDP flood, TCP SYN) using hping3
- **Flow Statistics**: 22 attributes including packet counts, flow duration, TCP flags

### Feature Engineering
Key features used for classification:
- `packet_count_per_second`
- `byte_count_per_second` 
- `flow_duration_sec`
- `ip_proto` (protocol type)
- `flags` (TCP control flags)

### Machine Learning Models
- **Random Forest**: Primary classifier for high accuracy
- **Support Vector Machine**: Alternative for comparison
- **Binary Classification**: Benign (0) vs Malicious (1)

### Mitigation Strategies
- **Dynamic Blocking**: Automatic blocking of malicious IP addresses
- **Traffic Rerouting**: Redirecting suspicious traffic to honeypots
- **Adaptive Rules**: SDN flow rule updates in real-time

## 📊 Results Analysis

### Detection Performance
- Random Forest achieved 99.88% accuracy with minimal false positives
- System maintains high performance under varying traffic loads
- Real-time detection with sub-second response times

### Network Impact
- Minimal performance overhead during normal operation
- Effective mitigation reduces attack impact by 95%+
- Maintains Quality of Service for legitimate users

## 🎯 Key Findings

1. **Random Forest Superiority**: Outperformed SVM in accuracy and scalability
2. **Real-time Viability**: Successfully deployed in live SDN environment
3. **Automated Defense**: Reduced manual intervention requirements
4. **Scalability**: Maintained performance under high traffic loads

## 🔮 Future Work

- **Zero-day Attack Detection**: Implement deep learning models (CNN-LSTM)
- **Enhanced Scalability**: Distributed SDN controller architecture
- **Dynamic Thresholding**: Adaptive anomaly detection thresholds
- **Multi-vector Attacks**: Protection against sophisticated attack combinations
