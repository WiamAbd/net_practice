*This project has been created as part of the 42 curriculum by wiam.*

# NetPractice

## Description

NetPractice is a practical introduction to computer networking. The project consists of 10 simulated network levels in which incorrect or incomplete configurations must be corrected so that the requested hosts and interfaces can communicate.

The exercises develop an understanding of how IPv4 networks operate, including:

- IPv4 addressing and CIDR notation
- Subnet masks, network addresses, usable host ranges, and broadcast addresses
- Communication inside one subnet
- Routers, switches, and network interfaces
- Default gateways and next hops
- Static routes and routing tables
- Forward and return paths
- Public, private, loopback, and other reserved addresses
- The relationship between the TCP/IP and OSI models

No software is implemented for this project. The work consists of analysing each topology, calculating valid subnets, configuring interfaces and routes, testing connectivity, and exporting the successful configuration for every level.

## Instructions

### Requirements

- A Unix-like shell (Linux, macOS, or WSL)
- A modern web browser
- Python 3 as a fallback local web server

### Running the training interface

1. Download and extract the NetPractice archive supplied on the project page.
2. Open a terminal in the extracted directory.
3. Start the local server:

```bash
./run.sh
```

4. Open the URL printed in the terminal, for example:

```text
http://localhost:49152
```

Keep the terminal open while using the interface. Press `Ctrl+C` when you want to stop the server.

If `run.sh` does not work, start a server manually:

```bash
python3 -m http.server 49242
```

Then open:

```text
http://localhost:49242
```

### Solving a level

1. Enter your 42 login to load your personal configuration, or use the evaluation tab for a random configuration.
2. Read every communication goal shown at the top of the page.
3. Modify only the unshaded fields.
4. Check that interfaces connected to the same link belong to the same subnet.
5. Ensure that different links use distinct, non-overlapping subnets.
6. Verify that no interface uses a network or broadcast address.
7. Configure gateways and routes for both the forward and return paths.
8. Click **Check again** and use the logs at the bottom of the page to diagnose errors.
9. Once the level succeeds, click **Get my config** before proceeding.

### Submission

The repository root must contain:

- This `README.md`
- Exactly 10 exported configuration files, one for each level

Only files committed to the Git repository are evaluated. Check all filenames and confirm that every level was exported using your login.

During the peer evaluation, three random levels must be completed within a limited time. External tools are forbidden during the evaluation; only a simple calculator such as `bc` is tolerated.

## Key networking ideas

### IP address and subnet mask

An IPv4 address identifies a network interface. Its subnet mask separates the network part from the host part. For example, `192.168.1.10/24` belongs to the network `192.168.1.0/24`.

### Network and broadcast addresses

The first address of a traditional IPv4 subnet identifies the network, while the last address is its broadcast address. Neither is normally assigned to a host.

### Switch

A switch connects devices within the same local network. It does not route packets between different IP networks.

### Router and gateway

A router connects different networks. Each router interface has an address in the network attached to that interface. A host's default gateway is normally the address of the router interface within the host's own subnet.

### Routes

A route has a destination network and a next hop. If several routes match a destination, the most specific route (the longest prefix) is selected. A default route, `0.0.0.0/0`, is used when no more specific route exists.

Successful communication generally requires both a forward path and a return path.

## Useful checks

For a prefix `/n`:

```text
Total addresses = 2^(32 - n)
```

For traditional IPv4 subnets up to `/30`:

```text
Usable hosts = 2^(32 - n) - 2
```

Before validating a configuration, check:

- Are directly connected interfaces in the same subnet?
- Do separate links use non-overlapping subnets?
- Are all addresses valid host addresses?
- Is each gateway directly reachable from the device using it?
- Does every router know how to reach remote networks?
- Is there a valid return route?
- Are private or reserved addresses being incorrectly routed through the simulated Internet?

## Resources

### References

- [RFC 791 - Internet Protocol](https://www.rfc-editor.org/rfc/rfc791)
- [RFC 4632 - Classless Inter-domain Routing (CIDR)](https://www.rfc-editor.org/rfc/rfc4632)
- [RFC 1918 - Address Allocation for Private Internets](https://www.rfc-editor.org/rfc/rfc1918)
- [Cisco: IP Addressing and Subnetting for New Users](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)
- [Cloudflare: What is the OSI model?](https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/)
- The official NetPractice subject and the logs provided by the training interface

These resources were used to study TCP/IP addressing, subnet masks, CIDR, network and broadcast addresses, default gateways, routing tables, routers, switches, private address ranges, and the OSI layers.

### Use of AI

AI was used as a learning and documentation assistant to:

- Clarify networking terminology with beginner-friendly explanations
- Check subnet calculations and identify overlapping networks
- Explain forward routes, return routes, gateways, and next hops
- Help structure and review this README

Every proposed configuration was tested in the NetPractice interface. AI output was reviewed rather than accepted blindly, and the final configurations remain the author's responsibility.

