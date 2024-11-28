# OpenAirInterface-5G-Core-Network-with-MEC-Integration
## **Mentor**
**Dr. Bhupendra Kumar**

## **Team Members**
- **Mohit Ritwik Yernena** (202251071)
- **Rohit Lokhande** (202251068)
- **Narendra Deshmukh** (202251036)
- **Susmit Kumar Bharati** (202251138)

## **Project Overview**
This project demonstrates the setup and deployment of a 5G Core Network using **OpenAirInterface (OAI)** with Docker containers. The architecture integrates essential 5G core network functions, including AMF, SMF, UPF, NRF, UDM, and UDR, alongside **Multi-access Edge Computing (MEC)**. By leveraging tools such as **UERANSIM** for UE and gNB simulation, the project showcases edge computing's ability to enhance latency-sensitive applications like video streaming, AR/VR, IoT, and real-time analytics.

This implementation enables a **controlled, repeatable, and extensible simulation environment**, making it ideal for validating the effectiveness of 5G technologies in reducing latency and improving throughput through MEC.

---

## **Key Features**
- **Containerized Deployment**: All 5G Core components (AMF, SMF, UPF, NRF, UDM, AUSF, and UDR) are deployed as Docker containers, ensuring scalability, ease of use, and modularity.
- **UERANSIM Integration**: Simulates User Equipment (UE) and gNodeB (gNB) to test the behavior and performance of the 5G core network.
- **MEC Offloading**: Demonstrates traffic offloading to MEC servers for real-time, low-latency data processing and edge computing.
- **Traffic Inspection and Analysis**: Captures NAS, NGAP, SCTP, and GTP traffic using **Wireshark**, enabling real-time monitoring and troubleshooting of network interactions.
- **Latency and Throughput Validation**: Performance testing with tools like `iperf3` to compare results with and without MEC integration.
- **Video Streaming Testbed**: Real-time video streaming over a simulated 5G network, showcasing reduced buffering and improved quality using MEC.

---

## **Architecture**
The system architecture is designed with modularity and extensibility in mind.

### **1. Core Network Functions**:
- **AMF (Access and Mobility Management Function)**: Handles registration, connection management, and mobility procedures.
- **SMF (Session Management Function)**: Manages PDU session establishment, modification, and release.
- **UPF (User Plane Function)**: Routes and forwards user traffic, supports MEC integration for local breakout.
- **NRF (Network Repository Function)**: Supports service-based architecture by allowing network functions to discover one another.
- **UDM/UDR (Unified Data Management/Repository)**: Manages subscriber data and supports authentication.

### **2. MEC Integration**:
- Edge servers placed close to the UPF to ensure minimal latency.
- Offloads video streaming, analytics, or compute-intensive tasks to the edge for optimized performance.

### **3. Simulation**:
- **UERANSIM**: Simulates the UE and gNB, providing an end-to-end testing environment to validate 5G core functionalities.

### **4. Traffic Analysis**:
- Tools like **Wireshark** and **Tcpdump** capture and analyze SCTP, GTP, and NGAP traffic for troubleshooting and validation.

---

## **Demonstration: Video Streaming**
### **Setup**:
1. **Install and Configure a Video Server** on the MEC:
   - Use a lightweight video streaming server like **NGINX RTMP** or **GStreamer**.
   - Configure the MEC to host the video server:
     ```bash
     apt install nginx
     # Enable RTMP module in the nginx.conf file for streaming
     ```
2. **Stream a Video** from the MEC to the simulated UE:
   - Host a video file on the MEC server.
   - Use VLC Media Player or a browser on the UE simulation to stream the video.

3. **Test Latency and Quality**:
   - Perform streaming tests with and without MEC offloading.
   - Use `iperf3` and Wireshark to measure reduced latency and improved throughput with MEC integration.

---

## **Getting Started**
### **Prerequisites**:
- **Docker & Docker Compose**: Ensure Docker is installed for containerized deployment.
- **Wireshark**: For network traffic analysis.
- **Basic Networking Knowledge**: Familiarity with 5G protocols like NAS, NGAP, and GTP is recommended.

### **Installation**:
1. **Clone the Repository**:
   ```bash
   git@gitlab.eurecom.fr:oai/cn5g/oai-cn5g-fed.git
   cd oai-cn5g-fed-master
   ```
2. **Deploy the 5G Core with Docker Compose**:
   ```bash
   docker-compose -f docker-compose-basic-vpp-nrf.yaml up -d
   ```
3. **UERANSIM deploy** to simulate UE and gNB behavior:
   ```bash
   docker-compose -f docker-compose-ueransim-vpp.yaml up -d
   ```

4. **Run UERANSIM** to simulate UE and gNB behavior:
   ```bash
   docker run -it --network host --name ueransim ueransim:latest
   ```

---

## Network Testing in UE Simulation Environment

This section describes how to test network connectivity, monitor traffic, and measure bandwidth within the UE simulation environment.

## **1. Ping Test**

The `ping` command checks connectivity between the UE interface and an external server (e.g., google.com).

### **Command**:
```bash
docker exec -it ueransim ping -c 3 -I uesimtun0 google.com
```

## **Traffic Monitoring and Testing**
1. **Monitor Network Interfaces**:
   - Open Wireshark and select an appropriate interface (e.g., `cn5g-access` or `uesimtun0`).
   - Use protocol filters like `ngap`, `gtp`, or `sctp` to inspect specific traffic flows.

2. **Latency and Throughput Testing**:
   - Use `iperf3` to measure performance between the UE and MEC:
     ```bash
     iperf3 -c <MEC_Server_IP> -t 10
     ```
   - Analyze metrics for latency reduction and throughput improvements.

---

## **Use Cases**
- **Real-Time Video Streaming**: Leverage MEC for buffer-free, low-latency video streaming.
- **AR/VR Applications**: Optimize AR/VR experiences by processing data close to the user.
- **IoT**: Enhance IoT device interactions with reliable, low-latency communication.
- **Content Delivery**: Use edge caching to reduce core network load and improve content delivery.

---

## **Contributing**
We welcome contributions to this project! You can:
- Open issues for bugs or feature requests.
- Submit pull requests for new features or enhancements.

---

## **Acknowledgments**
Special thanks to:
- The **OpenAirInterface Community** for their 5G core solutions.
- The **UERANSIM Team** for providing an excellent simulation tool.
- Developers of tools like **Wireshark**, which make traffic analysis seamless.

---

## **Contact**
For queries or support, feel free to reach out at:
- **Email**: 202251071@iiitvadodara.ac.in
