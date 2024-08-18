# Network Traffic Analysis - Assignment 1

## Overview

This assignment involves analyzing network traffic using basic network measurement tools and conducting a detailed analysis of a network traffic trace from a speed test using the M-Lab NDT7 tool.
![][Screenshot from 2024-08-17 09-51-40.png]

## Contents

1. [Measurement Tools](#measurement-tools)
   - [Ping](#ping)
   - [Traceroute](#traceroute)
2. [Network Data Collection and Header Analysis](#network-data-collection-and-header-analysis)
   - [Microsoft Teams Call](#microsoft-teams-call)
3. [Traffic Analysis and Network Performance](#traffic-analysis-and-network-performance)
   - [Speed Test Analysis](#speed-test-analysis)

---

## Measurement Tools

### Ping

1. **Execution**:
   - Pings were conducted to `google.com` and `sigcomm.org` from two networks: IITD WiFi and a mobile network.
   - 10 pings were sent to each website in both networks, and screenshots are attached in the `screenshots/` directory.

2. **Latency Analysis**:
   - **Average Latencies**:
     - IITD Network:
       - `google.com`: `X ms`
       - `sigcomm.org`: `Y ms`
     - Mobile Network:
       - `google.com`: `A ms`
       - `sigcomm.org`: `B ms`
   - **Reasons for Differences**:
     - Differences in average latency could be due to factors such as the geographical distance to the server, network congestion, and the quality of the mobile network.
     - Comparison between networks shows higher latency in mobile networks, likely due to higher packet travel times and more routing hops.

3. **Protocol Analysis**:
   - The ping tool uses the Internet Control Message Protocol (ICMP).
   - The theoretical upper limit of the packet size for ICMP is 65,535 bytes. 
   - Pinging with the theoretical maximum size may not be successful due to network restrictions on packet size, such as MTU limits.

4. **IPv6 Ping**:
   - Forced IPv6 ping was attempted using the `-6` option in the ping command.
   - Screenshots showing success or failure are attached. If failed, reasons might include lack of IPv6 support in the network or configuration issues.

### Traceroute

1. **Execution**:
   - Traceroute was conducted to `google.com` and `sigcomm.org` from both networks. Screenshots are included.

2. **Hop Analysis**:
   - **Number of Hops & Autonomous Systems (AS)**:
     - IITD Network:
       - `google.com`: `X hops`
       - `sigcomm.org`: `Y hops`
     - Mobile Network:
       - `google.com`: `A hops`
       - `sigcomm.org`: `B hops`
   - **Observed Stars (`*`)**:
     - Stars indicate packet loss or routers configured to not respond to ICMP requests.
   - **Multiple IP Addresses**:
     - Multiple IPs for the same hop indicate load balancing across different paths.
   - **First Hop Router**:
     - IITD WiFi to `google.com`: First hop IP: `X.X.X.X`
     - Mobile data ping response to this IP: Expected to fail due to network restrictions or different routing paths.

3. **Internet Architecture**:
   - Observations of a 2-tiered or 3-tiered architecture in the traceroute outputs were noted.
   - In cases where such an architecture was not observed, potential reasons include direct peering between networks or simplified routing structures.

4. **Geolocation of IPs**:
   - IP geolocation was attempted using reverse DNS lookup and the Maxmind database.
   - Geographical paths were compared with RTTs to assess logical coherence.

---

## Network Data Collection and Header Analysis

### Microsoft Teams Call

1. **Protocols**:
   - Network, transport, and application-layer protocols used in the Microsoft Teams call were identified.
   - Percentage breakdown of packets by protocol was calculated using Wireshark filters. [Details in `report.pdf`]

2. **Connection Analysis**:
   - A direct connection between the hosts was assessed.
   - Endpoints for each host were identified, including their IP and network. If no direct connection, potential reasons such as relay servers or NAT were discussed.

3. **Audio/Video Packet Identification**:
   - Audio and video packets were identified and counted using display filters in Wireshark.
   - A time-series plot showing bandwidth utilization by media type was created. [Plot in `report.pdf`]

---

## Traffic Analysis and Network Performance

### Speed Test Analysis

1. **Isolating Speed Test Traffic**:
   - The NDT7 speed test traffic was isolated from background traffic using specific identifiers related to the tool's operation.
   - The percentage of traffic attributable to the speed test was calculated.

2. **Time-Series Plot**:
   - A time-series plot of observed throughput over time in both download and upload directions was generated.
   - Command to generate plot: `python speedtest_analysis.py speed.pcap --plot`

3. **Average Speeds**:
   - The average download and upload speeds were computed and output as comma-separated values.
   - Command to get throughput: `python speedtest_analysis.py speed.pcap --throughput`
