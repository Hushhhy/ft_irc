# ft_irc - Internet Relay Chat Server

*This project has been created as part of the 42 curriculum by acarpent and pgrellie.*

<p align="center">
  <img src="assets/badge.png" alt="Badge">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-C%2B%2B98-blue" alt="Language">
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen" alt="Status">
</p>

---

## 📋 Description

**ft_irc** is a comprehensive IRC (Internet Relay Chat) server implementation created as part of the 42 curriculum. This project involves building a fully functional IRC server from scratch in C++ 98, capable of handling real-time text-based communication between multiple clients.

The Internet Relay Chat protocol is a foundational internet standard that enables real-time messaging. This implementation demonstrates deep understanding of network programming, socket handling, multi-client management, and the IRC protocol itself.

### Project Goals

- **Network Programming Mastery**: Understand TCP/IP sockets and non-blocking I/O operations
- **Concurrent Client Handling**: Manage multiple simultaneous connections without threading or forking
- **IRC Protocol Implementation**: Properly implement core IRC features and commands
- **Robust Error Handling**: Create a stable server that never crashes unexpectedly
- **C++ Best Practices**: Write clean, well-structured code following C++ 98 standards
- **Advanced I/O Management**: Master poll() and non-blocking file descriptors

---

## 🛠️ Instructions

### Compilation

To compile the IRC server:

```bash
make
```

### Available Make Rules

```bash
make              # Compile the server (creates ircserv executable)
make all          # Same as make
make clean        # Remove object files (.o)
make fclean       # Remove object files and the executable
make re           # Recompile everything (fclean + all)
```

### Running the Server

Once compiled, start the IRC server with:

```bash
./ircserv <port> <password>
```

**Arguments:**
- `<port>`: The port number on which the server listens for incoming connections (e.g., 6667 for standard IRC)
- `<password>`: The connection password required by IRC clients to authenticate

**Example:**
```bash
./ircserv 6667 mySecurePassword
```

### Connecting with an IRC Client

After the server is running, connect using any standard IRC client:

```bash
# Using netcat for basic testing
nc -C 127.0.0.1 6667

# Using a full IRC client (e.g., irssi, WeeChat, etc.)
irssi -c 127.0.0.1 -p 6667 -w mySecurePassword
```

### Testing

The server should handle partial data reception correctly:

```bash
# Test with fragmented commands using netcat
nc -C 127.0.0.1 6667
com^Dman^Dd
```

Use `Ctrl+D` to send data in fragments. The server must properly reassemble and process the command.

---

## 🎯 Core Features

### Authentication & User Management

- User authentication with server password
- Nickname (NICK) and username (USER) registration
- User connection/disconnection handling
- Unique user identification within the server

### Channel Management

- Create and join IRC channels
- Channel operators and regular users distinction
- User listing in channels
- Part and leave channel functionality

### Messaging

- **Public Messages**: Send messages to entire channels
- **Private Messages**: Direct user-to-user messaging
- **Channel Forwarding**: Messages automatically forwarded to all channel members
- **Message Broadcasting**: Proper message delivery to connected clients

### Channel Operator Commands

Channel operators have exclusive access to these commands:

| Command | Description |
|---------|-------------|
| **KICK** | Eject a user from the channel |
| **INVITE** | Invite a user to the channel |
| **TOPIC** | View or change the channel topic |
| **MODE** | Manage channel modes and settings |

### Channel Modes

- **i** - Invite-only channel (requires INVITE to join)
- **t** - Topic restriction (only operators can change topic)
- **k** - Channel key/password protection
- **o** - Grant/revoke operator privileges
- **l** - User limit (maximum users in channel)

---

## 🔧 Technical Specifications

### Compilation Requirements

- **Language**: C++ 98 standard
- **Compiler**: `c++` with flags `-Wall -Wextra -Werror`
- **Command**: Should compile correctly with `-std=c++98` flag
- **No external libraries or Boost allowed**

### Architecture & Requirements

- **Multi-client Support**: Handle multiple simultaneous connections
- **Non-blocking I/O**: All file descriptors operate in non-blocking mode
- **Single Poll Loop**: Only one poll() (or equivalent: select, kqueue, epoll) for all operations
- **No Forking**: Concurrent handling without child processes
- **Stability**: Server must never crash, even under error conditions
- **Protocol**: TCP/IP (IPv4 or IPv6)

### Reference IRC Client

The server implementation supports standard IRC clients and has been tested with reference IRC clients to ensure protocol compliance.

### Allowed External Functions

All standard C++ socket and system functions are permitted:
```
socket, close, setsockopt, getsockname, getprotobyname, 
gethostbyname, getaddrinfo, freeaddrinfo, bind, connect, 
listen, accept, htons, htonl, ntohs, ntohl, inet_addr, 
inet_ntoa, inet_ntop, send, recv, signal, sigaction, 
sigemptyset, sigfillset, sigaddset, sigdelset, sigismember, 
lseek, fstat, fcntl, poll
```

---

## 📚 Project Structure

```
ft_irc/
├── Makefile                    # Build configuration
├── README.md                   # This file
├── ircserv                     # Compiled executable
├── headers/
│   ├── Server.hpp             # Main server class
│   ├── Clients.hpp            # Client connection management
│   ├── Channels.hpp           # Channel management
│   ├── CommandHandler.hpp     # IRC command processing
│   └── Messages.hpp           # Message handling
├── srcs/
│   ├── main.cpp              # Entry point
│   ├── Server.cpp            # Server implementation
│   ├── Clients.cpp           # Client implementation
│   ├── Channels.cpp          # Channel implementation
│   ├── CommandHandler.cpp    # Command processing
│   └── Messages.cpp          # Message processing
└── assets/                    # Project resources
```

---

## 📖 Resources

### IRC Protocol Documentation
- [RFC 1459 - Internet Relay Chat Protocol](https://tools.ietf.org/html/rfc1459) - Official IRC protocol specification
- [RFC 2812 - Internet Relay Chat Protocol (Updated)](https://tools.ietf.org/html/rfc2812) - Modern IRC protocol updates
- [IRC Concepts](https://en.wikipedia.org/wiki/Internet_Relay_Chat) - Overview of IRC architecture and concepts

### Network Programming
- [Socket Programming in C++](https://www.geeksforgeeks.org/socket-programming-cc/) - Comprehensive socket guide
- [Berkeley Sockets API](https://en.wikipedia.org/wiki/Berkeley_sockets) - Standard socket interface documentation
- [Non-blocking I/O](https://linux.die.net/man/7/socket) - Non-blocking socket operations
- [poll() System Call](https://man7.org/linux/man-pages/man2/poll.2.html) - Multiplexed I/O documentation

### C++ 98 Standards
- [C++ 98 Reference](https://en.cppreference.com/w/cpp) - cppreference C++ documentation
- [Linux man pages](https://man7.org/linux/man-pages/) - System call and library function documentation

### IRC Clients for Testing
- [Irssi](https://irssi.org/) - Terminal-based IRC client
- [WeeChat](https://weechat.org/) - Modern terminal IRC client
- [HexChat](https://hexchat.github.io/) - GUI-based IRC client

### 42 School Resources
- [42 Norm](https://github.com/42School/42cursus) - 42 coding standards and guidelines
- [42 Intranet](https://intra.42.fr) - Official project specifications

### How AI Was Used

AI was utilized for **documentation, project structure guidance, and protocol research purposes only**:
- Organizing the README structure following professional standards
- Gathering and structuring IRC protocol information
- Creating clear technical specifications and feature lists
- Providing documentation best practices and formatting

**AI was NOT used for**:
- Implementing the IRC server core logic
- Writing socket and networking code
- IRC command processing and protocol handling
- Problem-solving for architectural decisions

All implementation work was completed independently, with peer review and collaborative debugging. This approach ensures deep understanding of network programming concepts and the IRC protocol.

---

## 🚀 Getting Started

### Step 1: Build the Server
```bash
cd ft_irc
make
```

### Step 2: Start the Server
```bash
./ircserv 6667 password123
```

### Step 3: Connect with a Client
In a new terminal:
```bash
irssi -c 127.0.0.1 -p 6667 -w password123
```

### Step 4: Test IRC Commands

Once connected:
```
/join #general        # Join a channel
/privmsg user Hello   # Send private message
/list                 # List available channels
/nick NewNickname     # Change your nickname
/quit                 # Disconnect
```

---

## ✅ Evaluation Criteria

- ✓ Server handles multiple simultaneous connections
- ✓ All I/O operations are non-blocking
- ✓ Single poll() loop manages all operations
- ✓ Standard IRC client connects and functions properly
- ✓ Public and private messaging work correctly
- ✓ Channel operations and modes implemented
- ✓ Channel operator commands functional
- ✓ Server never crashes unexpectedly
- ✓ Code follows C++ 98 standard and 42 Norm
- ✓ Makefile properly configured

---

## 📝 Additional Notes

- **Mandatory Part Only**: This implementation focuses on core IRC server functionality
- **Error Handling**: All edge cases are handled gracefully without crashes
- **Protocol Compliance**: Implementation follows RFC 1459/2812 standards
- **Performance**: Efficient handling of multiple concurrent connections
- **Code Quality**: Clean, well-documented, and maintainable codebase

---

*Last updated: May 2026*
