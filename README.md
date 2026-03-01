# Overview

I built this hybrid Windows–Linux lab to simulate a small business enterprise environment using Windows Server 2022 and Ubuntu Server inside VirtualBox.

The goal was to deploy a working domain controller, configure DNS correctly, join a Linux server to Active Directory, validate Kerberos authentication, and troubleshoot real networking and identity issues along the way.

This lab required diagnosing problems across multiple layers including routing, DNS resolution, domain discovery, and authentication flow.

# Lab Architecture

# Virtualization

- Platform: Oracle VirtualBox
- Network Model:
  - Adapter 1: NAT (Internet access)
  - Adapter 2: Internal Network (intnet-lab)

# Domain Controller

- VM Name: WIN-DC
- OS: Windows Server 2022
- IP Address: 192.168.100.10
- Subnet: 255.255.255.0
- DNS: Self (192.168.100.10)
- Roles Installed:
  - Active Directory Domain Services
  - DNS Server

# Domain

- Domain Name: bmits.local
- Forest Functional Level: Windows Server 2022
- DNS Forwarders Configured
- Security Groups Created for Linux Access Control

# Linux Member Server

- OS: Ubuntu Server
- Joined to Domain: bmits.local
- Authentication: Kerberos
- Identity Integration: SSSD
- Access Controlled via AD Security Groups

# Authentication Workflow

1. User initiates login on Ubuntu server.
2. DNS resolves the domain controller.
3. Kerberos ticket request is sent to Active Directory.
4. AD validates credentials.
5. SSSD maps domain identity to Linux UID and GID.
6. Group membership determines login and sudo permissions.

# Troubleshooting

- DNS forwarder misconfiguration
- NAT vs NAT Network adapter conflicts
- Internal routing issues
- SSSD identity resolution failures
- Kerberos authentication errors
- Group-based access control conflicts
