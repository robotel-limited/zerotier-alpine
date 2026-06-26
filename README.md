# ZeroTier One for Alpine Linux 🚀

ZeroTier One compiled and tested on **Alpine Linux v3.21**. This repository contains the full source code with build instructions for Alpine Linux.

## Why Alpine?

Alpine Linux is lightweight and secure, but the `zerotier-one` package is not available in the default repositories (even in edge/testing). This repo provides the source code and build instructions to compile ZeroTier One from source on Alpine.

## Build Instructions

### Prerequisites

```bash
apk add build-base linux-headers git openssl-dev
```

### Compile from Source

```bash
git clone https://github.com/robotel-limited/zerotier-alpine.git
cd zerotier-alpine
make ZT_SSO_SUPPORTED=0
make install
```

> **Note:** `ZT_SSO_SUPPORTED=0` disables the Rust/SSO component, which is not needed for standard operation and avoids the Rust toolchain dependency.

### Service Setup (OpenRC)

```bash
cp debian/zerotier-one.initd /etc/init.d/zerotier-one
chmod +x /etc/init.d/zerotier-one
rc-service zerotier-one start
rc-update add zerotier-one default
```

### Verify Installation

```bash
zerotier-cli info
```

Expected output:
```
200 info 5e6e37a95d 1.16.2 ONLINE
```

## Join a Network

```bash
zerotier-cli join <NETWORK_ID>
zerotier-cli listnetworks
```

## Files

| File | Description |
|------|-------------|
| `/usr/sbin/zerotier-one` | Compiled binary |
| `/var/lib/zerotier-one/` | Configuration directory (identity, authtoken, planet) |
| `/etc/init.d/zerotier-one` | OpenRC init script |

## License

This project is based on [ZeroTierOne](https://github.com/zerotier/ZeroTierOne) by ZeroTier, Inc., licensed under the BSL-1.1 license.
