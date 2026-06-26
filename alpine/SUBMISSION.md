# ZeroTier One for Alpine Linux - Package Submission

## Overview
This directory contains the APKBUILD for building **ZeroTier One v1.16.2** as an Alpine Linux package.

## Maintainer
- **Name:** Robotel Limited
- **Email:** tech@robotel.top

## Package Details
- **Package:** zerotier-one
- **Version:** 1.16.2
- **License:** BSL-1.1
- **Description:** ZeroTier One - Smart Ethernet Switch for Earth

## How to Submit to Alpine Linux Aports

### Prerequisites
- GitLab account (https://gitlab.alpinelinux.org)
- Alpine Linux development environment with `abuild` installed

### Steps

1. **Fork the aports repository:**
   ```bash
   # Go to https://gitlab.alpinelinux.org/alpine/aports
   # Click "Fork" to create your own copy
   ```

2. **Clone your fork:**
   ```bash
   git clone git@gitlab.alpinelinux.org:YOUR_USERNAME/aports.git
   cd aports
   ```

3. **Create the package directory:**
   ```bash
   mkdir -p testing/zerotier-one
   ```

4. **Copy the APKBUILD:**
   ```bash
   cp /path/to/this/APKBUILD testing/zerotier-one/
   ```

5. **Generate checksums:**
   ```bash
   cd testing/zerotier-one
   abuild checksum
   ```

6. **Test the build:**
   ```bash
   abuild -r
   ```

7. **Commit and push:**
   ```bash
   git add testing/zerotier-one/
   git commit -m "testing/zerotier-one: new package v1.16.2"
   git push origin master
   ```

8. **Create Merge Request:**
   - Go to your fork on GitLab
   - Click "Create Merge Request"
   - Target: `alpine/aports` main branch
   - Title: `testing/zerotier-one: new package v1.16.2`
   - Description: Include package details and testing notes

## Build Notes
- `ZT_SSO_SUPPORTED=0` is used to skip the Rust/SSO component
- This avoids the need for Rust toolchain in the build process
- The package depends on: `libstdc++`
- Build dependencies: `build-base`, `linux-headers`, `openssl-dev`

## Verification
After successful build, verify the package:
```bash
apk add zerotier-one
rc-service zerotier-one start
zerotier-cli status
```
