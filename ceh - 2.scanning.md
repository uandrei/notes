Scope of scanning
- part 1 - host identification
- part 2 - listing services, open ports, OS detection and so forth

Protocols
- ICMP
    - uses 2 concepts: Message type and Message Response
- TCP
    - most used in this phase
    - connection oriented
    - reliable and good for resiliency
    - 3 way handshake responses
        - SYN ACK - port open
        - RS - port closed
        - No answer - host down or filtered
- UDP
    - no sequencing

- nmap
    - -sn - ping scan (no ports scanned)
- hping3

Host Discovering - ping (network) sweeps
- ARP ping scan
    - most reliable and accurate
    - useful for system discovery on large address spaces
    - !!! You need to be on the same subnet as target - Layer 2 protocol
    - nmap -sn -PR
- UDP ping scan
    - can detect systems behind firewalls with strict TCP filtering
    - nmap -sn -PU
- ICMP ping scan
    - ICMP echo ping
        - oldest and slowest
        - nmap -PE
        - ICMP echo ping sweep
            - can detect if ICMP message goes through a firewall
            - doesn't work on Windows based networks
            - nmap -PI
    - ICMP timestamp ping
        - alternative for ECHO requests
        - can be useful when ping replies are disabled
        - nmap -PP
    - ICMP address mask ping
        - alternative for ECHO requests
        - can be useful when ping replies are disabled
        - nmap -PM
- TCP ping scan
    - TCP syn ping
        - connection is not completed - can be stealthy
        - nmap -PS
    - TCP ack ping
        - maximizes chances to bypass firewall
        - nmap -PA
- IP Protocol ping scan
    - nmap -PO

Port scanning
- TCP connect - Full open scan
    - easy to detect
    - nmap -sT 
- TCP Stealth scan - Half open scan (no further comms after the SYN)
    - !!! can be detected by IDS
    - nmap -sS
- TCP Inverse TCP Flag
    - avoids many IDS and logging - highly stealthy
    - !!! works only on RFC 793 compliant systems
    - !!! unix only
    - !!! doesn't work against any Windows to date
    - FIN
        - nmap -sF
    - NULl (no flags set)
        - nmap -sN
    - Xmas (FIN+URG+PSH)
        - nmap -sX
- TCP Maimon
    - nmap -sM
- ACK flag probe (nmap -sA)
- TTL Based ACK flag probe scan (nmap -sA -ttl 100)
- Window based ACK flag probe scan (nmap -sA -sW)
    - can evade IDS
    - slow and only for old OS
- IDLE/IPID Header scan
    - requires zombie
    - nmap -Pn -p -sI
- UDP scan
    - nmap -sU

Service Version discovery - 34:25

- FOR EXAM - NMAP
    - scan type switches
    - timing options
    - host discovery
    - aggressive script scanning