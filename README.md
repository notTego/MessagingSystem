# UDP Client - TCP/UDP Messaging System

A versatile UDP/TCP environment for sending payloads to a server using various modes and configurations.

## Features

- Load payloads from a JSON file
- Customizable source IP and port
- Multiple sending modes (`all_once`, `manual`, `random`)
- Control the number of packets and delay between them

---

## Usage

```bash
python udp_client.py [OPTIONS] <server_ip> <server_port>
```

### Required Arguments

| Argument       | Description         |
|----------------|---------------------|
| `server_ip`    | IP address of the server to send messages to |
| `server_port`  | Port number of the server to send messages to |

---

### Optional Arguments

#### General
| Option           | Description |
|------------------|-------------|
| `-h, --help`     | Show help message and exit |

#### Input
| Option                  | Description |
|-------------------------|-------------|
| `--input_file FILE`     | Path to a JSON file containing payloads (default: `sample_payloads.json`) |

#### Source Address
| Option                         | Description |
|--------------------------------|-------------|
| `--source-address ADDRESS`     | Source IP address to bind the UDP client (default: unspecified) |
| `--source-port PORT`           | Source port to use (range: 1024–65535, default: random) |

#### Workload Configuration
| Option                       | Description |
|------------------------------|-------------|
| `--mode {all_once,manual,random}` | Choose the message sending mode:  |
|                              | - `all_once`: Send each payload once |
|                              | - `manual`: Manually select which payload to send |
|                              | - `random`: Send random payloads continuously |

#### Load Characteristics
| Option          | Description |
|-----------------|-------------|
| `--count COUNT` | Number of packets to send (only used in `random` mode, default: infinity) |
| `--delay DELAY` | Delay between messages in milliseconds (default: 0) |

---

## Examples

**Send all messages once to a server:**
```bash
python udp_client.py --mode all_once 192.168.1.100 8080
```

**Use a specific source IP and port:**
```bash
python udp_client.py --source-address 192.168.1.50 --source-port 12345 --mode random --count 100 --delay 500 192.168.1.100 8080
```

**Run in manual mode with a custom input file:**
```bash
python udp_client.py --input_file my_payloads.json --mode manual 127.0.0.1 9090
```
