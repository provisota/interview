# OSI Model

The OSI (Open Systems Interconnection) Model is a conceptual framework used to understand and standardize the functions
of a telecommunication or computing system without regard to its underlying internal structure and technology. Developed
by the International Organization for Standardization (ISO) in the 1980s, the OSI model is structured into seven layers,
each specifying particular network functions. Here are the technical details of each layer:

# Physical Layer (Layer 1)

- **Function**: Concerned with the transmission and reception of the unstructured raw bit stream over a physical medium.
- **Components**: Includes hardware like cables, switches, and network interface cards.
- **Responsibilities**: Modulation, data rate, synchronization, line coding, physical topologies, and transmission
  media.

# Data Link Layer (Layer 2)

- **Function**: Provides node-to-node data transfer—a link between two directly connected nodes.
- **Components**: Switches and bridges.
- **Responsibilities**: Framing, physical addressing (MAC & LLC), error detection and handling, and flow control.
- **Sublayers**:
    - **MAC (Media Access Control)**: Manages protocol access to the physical network medium.
    - **LLC (Logical Link Control)**: Responsible for identifying network protocols, encapsulation, and error checking.

# Network Layer (Layer 3)

- **Function**: Determines how data is transferred between network devices.
- **Components**: Routers and layer 3 switches.
- **Responsibilities**: Routing, logical addressing (IP addresses), subnetting, encapsulation, and decapsulation.
- **Protocols**: IP, ICMP, IGMP, etc.

# Transport Layer (Layer 4)

- **Function**: Provides reliable, transparent transfer of data between end systems.
- **Responsibilities**: End-to-end connections, port and socket management, segmentation and reassembly of data,
  reliability, flow control, and error correction.
- **Protocols**: TCP, UDP.

# Session Layer (Layer 5)

- **Function**: Manages sessions in a network (semi-permanent dialogues between applications).
- **Responsibilities**: Establishing, managing, and terminating connections (sessions) between applications.
- **Features**: Session checkpointing and recovery, which are not commonly used today.

# Presentation Layer (Layer 6)

- **Function**: Ensures that the data is in a usable format and is where data encryption occurs.
- **Responsibilities**: Translation, compression, encryption/decryption.
- **Examples**: Formats like JPEG, MPEG, MIDI, and encryption formats.

# Application Layer (Layer 7)

- **Function**: Closest to the end user, this layer interacts with software applications that implement a communicating
  component.
- **Responsibilities**: Identification of communication partners, resource availability, synchronization, and
  application services.
- **Examples**: HTTP, FTP, SMTP, POP3, DNS.

# Key Concepts of the OSI Model

- **Encapsulation**: As data moves down through the layers, headers and trailers are attached at each layer.
- **Decapsulation**: The reverse process occurs at the receiving side, where headers and trailers are removed at each
  layer.
- **Layer Independence**: Each layer serves a specific function and is independent of the others, which allows for
  flexibility and adaptability in development and troubleshooting.

# Practical Implications

- The OSI model is more theoretical and is used as a reference tool to understand and communicate how different network
  protocols interact and where they fit in the overall process of data communication.
- Many protocols and network operations are often explained and taught with reference to the OSI model, although
  real-world networking often follows the simpler four-layer TCP/IP model.

The OSI model provides a universal set of guidelines and is fundamental in the development of new networking
technologies and protocols. Understanding the OSI model helps in diagnosing network problems and designing efficient
network solutions.