# update-vagrant-win64

A robust, production-ready bash script for downloading and verifying HashiCorp Vagrant for Windows systems.

## Features

- **Secure Downloads**: HTTPS downloads with SHA256 checksum verification
- **Retry Logic**: Automatic retry on network failures with exponential backoff
- **Input Validation**: Semantic version validation and command injection prevention
- **Backup Management**: Automatic backup creation with timestamp
- **Error Handling**: Comprehensive error handling with logging and rollback
- **Signal Handling**: Graceful cleanup on interruption
- **API Integration**: Uses HashiCorp API for version discovery

## Requirements

- `curl` - for downloading files
- `sha256sum` - for checksum verification
- Bash 4.0+ with `set -euo pipefail` support

## Usage

### Download a specific version
```bash
./update-vagrant-win64.sh 2.2.19
```

### Show available versions
```bash
./update-vagrant-win64.sh
```

### Show help
```bash
./update-vagrant-win64.sh --help
```

### Beta versions
```bash
./update-vagrant-win64.sh 2.3.0-beta1
```

## How it works

1. **Validation**: Validates version format and checks if version exists
2. **Download**: Downloads MSI and SHA256SUMS files from HashiCorp releases
3. **Verification**: Verifies SHA256 checksum for integrity
4. **Backup**: Creates timestamped backup of existing `vagrant.msi`
5. **Installation**: Copies verified MSI to `vagrant.msi` for manual installation

## Output Files

- `vagrant.msi` - The downloaded Vagrant MSI installer
- `vagrant.msi.backup.YYYYMMDD_HHMMSS` - Backup of previous MSI (if exists)
- `/tmp/vagrant-update.log` - Detailed operation log

## Security

- Uses HTTPS with proper certificate verification
- Sanitizes input to prevent command injection
- Verifies SHA256 checksums before installation
- Creates backups with automatic rollback on failure

## Manual Installation

After the script completes successfully, manually install the MSI file on your Windows system:

1. Transfer `vagrant.msi` to your Windows machine
2. Run the MSI installer as Administrator
3. Verify installation with `vagrant --version`

## Error Recovery

If the script fails or is interrupted:
- Temporary files are automatically cleaned up
- Backups are restored if available
- Detailed error information is logged to `/tmp/vagrant-update.log`

## License

MIT License - See LICENSE file for details.