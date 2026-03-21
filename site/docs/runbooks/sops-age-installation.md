# SOPS + age Installation Runbook (Debian)

This runbook installs:
- `sops` (Secrets OPerationS)
- `age` (encryption tool used by sops)

This is intended for Docker hosts managing encrypted `.env` files.

---

## Purpose

- Encrypt sensitive configuration files (e.g. `.env`)
- Store encrypted secrets safely in Git
- Decrypt only when needed at runtime or manually

---

## Prerequisites

- Debian-based system
- `curl` installed
- `tar` installed
- Root or sudo access

---

## Installation

### 1. Install SOPS

Download the binary:

```bash
curl -LO https://github.com/getsops/sops/releases/download/v3.11.0/sops-v3.11.0.linux.amd64
```

Move to `/usr/local/bin` and make executable:

```bash
mv sops-v3.11.0.linux.amd64 /usr/local/bin/sops
chmod +x /usr/local/bin/sops
```

Verify:

```bash
sops --version
```

---

### 2. Install age

Download:

```bash
curl -LO https://github.com/FiloSottile/age/releases/download/v1.2.1/age-v1.2.1-linux-amd64.tar.gz
```

Extract:

```bash
tar xf age-v1.2.1-linux-amd64.tar.gz
```

Move binaries:

```bash
mv age/age /usr/local/bin
mv age/age-keygen /usr/local/bin
```

Cleanup extracted files:

```bash
rm -r ./age
```

Make executable:

```bash
chmod +x /usr/local/bin/age
chmod +x /usr/local/bin/age-keygen
```

Verify:

```bash
age --version
```

---

## Key Management

### 3. Create SOPS age directory

```bash
mkdir -p ~/.config/sops/age
cd ~/.config/sops/age
```

---

### 4. Create or Import age Key

#### Option A — Use Existing Key

```bash
vi keys.txt
```

Paste your existing key exactly as originally generated.

**IMPORTANT:**
- Do not modify formatting
- Ensure both public + private key are intact

---

#### Option B — Generate New Key

```bash
age-keygen -o ./keys.txt
```

This will output:
- Public key → used for encryption
- Private key → stored in `keys.txt`

---

## Usage

### 1. Encrypt a File

```bash
sops -e --in-place .env
```

---

### 2. Decrypt a File

```bash
sops -d .env > .env.dec
```

---

### 3. Cleanup Decrypted Files

```bash
shred -u .env.dec 2>/dev/null || rm -f .env.dec
```

---

## Notes

- Never commit `.env.dec` files
- Only commit encrypted files (e.g. `.env`)
- Keep `keys.txt` secure and backed up
- Loss of `keys.txt` = permanent data loss

---

## Recommended Next Steps (Optional)

- Add `.env.dec` to `.gitignore`
- Use `sops` with `.sops.yaml` for automation
- Integrate with Docker Compose using decrypted env files at runtime
- Consider using `sops exec-env` for safer workflows (no plaintext files)