
# AWS VPC Peering & Network Isolation Project

##  Architecture Overview
This project establishes secure communication and security isolation testing between two separate Virtual Private Clouds (VPCs) in AWS:
* **VPC A (`ewb-vpc-a`)**: Range `10.10.0.0/16` containing `ewb-bastion` in the public subnet (`10.10.1.0/24`) and `ewb-app-a` (`10.10.2.10`) in the private subnet (`10.10.2.0/24`).
* **VPC B (`ewb-vpc-b`)**: Range `10.20.0.0/16` containing `ewb-app-b` (`10.20.1.10`) in the private subnet (`10.20.1.0/24`).
* **Peering Connection (`ewb-a-b-peer`)**: Connects both VPCs with route table updates enabling private IP communication.

---

## Verification & Testing Evidence

| Test Case | Description | Expected Result | Evidence (Screenshot) |
| :--- | :--- | :--- | :--- |
| **Test 01: Peering Setup** | Active VPC Peering connection status | Active[cite: 7] | `Screenshots/01-vpc-peering-active.png` |
| **Test 02: Forward Path** | Ping test from App-A to App-B | 0% Packet Loss[cite: 11] | `Screenshots/02-forward-path-success.png` |
| **Test 03: Reverse Path** | Ping test from App-B back to App-A | 0% Packet Loss | `Screenshots/03-reverse-path-success.png` |
| **Test 04: Private SSH** | Secure shell access via Bastion ProxyJump | Successful Login | `Screenshots/04-private-ssh-proxyjump.png` |
| **Test 05: Isolation Test** | Inbound ICMP rule removed on App-B SG | 100% Packet Loss | `Screenshots/05-security-group-failure.png` |
| **Test 06: Recovery Test** | Inbound ICMP rule restored on App-B SG | 0% Packet Loss[cite: 12] | `screenshots/06-security-group-recovery.png` |
