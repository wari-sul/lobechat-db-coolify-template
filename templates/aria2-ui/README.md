# Aria2-UI - Complete Download Manager Stack

## Overview

This Docker Compose deploys **Aria2-UI**, an all-in-one download management solution that combines multiple tools into a single unified web interface. Perfect for managing downloads, file browsing, and cloud synchronization.

## What's Included

This template deploys a complete download management stack with:

- **Aria2**: High-performance download engine supporting HTTP/HTTPS, FTP, SFTP, BitTorrent, and Metalink
- **AriaNg**: Modern web UI for Aria2 with real-time download monitoring
- **File Browser**: Web-based file manager for browsing and managing downloaded files
- **Rclone**: Cloud storage sync tool for backing up downloads to cloud providers
- **Caddy**: Reverse proxy that unifies all services under a single domain

## Architecture

```
Single Container (aria2-ui):
├── Aria2 Engine (download manager)
├── AriaNg Web UI (port 8000)
├── File Browser (port 8000/files)
├── Rclone Web UI (port 8000/rclone)
└── Caddy Proxy (unifies all services)
```

## Access URLs

After deployment, access the services at:

- **Aria2 + AriaNg UI**: `http://yourip:8000` or your configured domain
- **File Server (Read Only)**: `http://yourip:8000/ro`
- **File Manager**: `http://yourip:8000/files`
- **Rclone Web UI**: `http://yourip:8000/rclone`

## Deployment Steps

### 1. Create New Service in Coolify

1. Navigate to your Coolify project
2. Click **New Resource** → **Docker Compose**
3. Paste the contents of `docker-compose.yaml`

### 2. Configure Environment Variables

All environment variables with their default values:

#### Required Variables (Must Set)

```bash
# CRITICAL: Set strong passwords for these
ARIA2_PASSWORD=your-strong-password-here
RPC_SECRET=your-rpc-secret-here
```

#### Optional Variables (With Defaults)

```bash
# Authentication
ENABLE_AUTH=true                    # Enable/disable authentication
ARIA2_USER=admin                    # Username for Aria2 and Rclone

# User permissions
PUID=1000                           # User ID for file ownership
PGID=1000                           # Group ID for file ownership

# Feature toggles
ENABLE_RCLONE=true                  # Enable Rclone integration
ENABLE_FILEBROWSER=true             # Enable File Browser
ENABLE_APP_CHECKER=false            # Enable application health checker

# Logging
CADDY_LOG_LEVEL=WARN               # Caddy log level (DEBUG, INFO, WARN, ERROR)

# Domain configuration (Coolify handles this)
DOMAIN=:80                          # Internal port binding
ARIA2_EXTERNAL_PORT=443             # External access port
ARIA2_SSL=false                     # SSL handled by Coolify proxy
```

### 3. Configure Domain in Coolify

1. In the Coolify service settings, go to **Domains**
2. Add your domain: `https://aria2.example.com`
3. Coolify will automatically handle SSL/TLS certificates

### 4. Deploy

Click **Deploy** and wait for the container to start.

## Initial Setup

### File Browser First Login

After deployment, you need to get the initial admin password:

1. Go to Coolify → Your aria2-ui service → **Logs**
2. Look for a line that says:
   ```
   User 'admin' initialized with randomly generated password: xxx
   ```
3. Copy the password shown
4. Navigate to `https://your-domain.com/files`
5. Login with:
   - **Username**: `admin`
   - **Password**: (the password from the logs)
6. **Important**: Change the password immediately after first login

### Rclone Login

Navigate to `https://your-domain.com/rclone` and login with:
- **Username**: Value of `ARIA2_USER` (default: `admin`)
- **Password**: Value of `ARIA2_PASSWORD`

## Volume Management

The template uses three persistent volumes:

| Volume | Purpose | Path |
|--------|---------|------|
| `aria2_data` | Downloaded files storage | `/data` |
| `aria2_cache` | Rclone config and Aria2 DHT cache | `/app/.cache` |
| `aria2_conf` | Configuration files (aria2.conf, aria2.session) | `/app/conf` |

## Usage Guide

### Downloading Files

1. Open Aria2 UI at your domain
2. Click **Add** button
3. Enter URL or upload .torrent file
4. Configure download options
5. Click **OK** to start download

### Managing Files

1. Navigate to `/files` path
2. Browse downloaded files
3. Use File Browser features:
   - Upload/download files
   - Create folders
   - Move/copy/delete files
   - Share files with download links

### Cloud Sync with Rclone

1. Navigate to `/rclone` path
2. Configure remote storage (Google Drive, S3, Dropbox, etc.)
3. Set up sync tasks to backup downloads
4. Schedule automatic sync intervals

## Troubleshooting

### File Browser Password Not Found

**Issue**: Can't find the initial password in logs

**Solution**: 
1. Check logs from the very beginning of container startup
2. If password log entry is missing, restart the container and check immediately
3. Alternatively, exec into the container and reset password manually

### Downloads Not Starting

**Issue**: Aria2 shows connection error

**Solution**:
1. Verify `RPC_SECRET` is set correctly
2. Check that `ENABLE_AUTH=true` matches your authentication expectations
3. Review container logs for Aria2 errors

### Permission Denied on Downloads

**Issue**: Cannot write to download directory

**Solution**:
1. Check `PUID` and `PGID` match your host system user
2. Verify volume permissions in Coolify
3. May need to adjust folder ownership in the volume

### Rclone Configuration Not Saving

**Issue**: Rclone remote configurations disappear after restart

**Solution**:
1. Ensure `aria2_cache` volume is properly mounted
2. Verify volume persistence in Coolify
3. Check logs for Rclone configuration errors

### Cannot Access Web UI

**Issue**: Domain returns 502 or timeout

**Solution**:
1. Verify service is running in Coolify
2. Check that domain is correctly configured
3. Ensure `DOMAIN=:80` is set (not changed)
4. Review Caddy logs for proxy errors

## Security Considerations

### Password Requirements

- **Always** change default passwords
- Use strong, unique passwords for `ARIA2_PASSWORD` and `RPC_SECRET`
- Change File Browser admin password after first login

### Network Security

- This template exposes all services through a single domain
- Coolify automatically provides HTTPS
- Consider restricting access using Coolify's built-in authentication

### Download Safety

- Be cautious with BitTorrent downloads
- Verify file sources before downloading
- Use Aria2's built-in verification features (checksums)

## Performance Tips

### Download Speed Optimization

Edit aria2.conf (in `aria2_conf` volume) to tune:
```
max-concurrent-downloads=5
max-connection-per-server=16
min-split-size=10M
split=10
```

### Storage Management

- Monitor `aria2_data` volume size
- Set up automatic cleanup or Rclone sync to cloud storage
- Consider enabling seed limits for torrents

### Resource Usage

- Default configuration is suitable for most use cases
- For heavy torrent usage, consider increasing container resources
- Monitor CPU usage during active downloads

## Scaling Notes

This is a single-container deployment and cannot be horizontally scaled. For high-availability:

- Deploy multiple instances with separate domains
- Use external load balancer
- Share storage using NFS or similar

## Advanced Configuration

### Custom Aria2 Configuration

1. After first deployment, access the `aria2_conf` volume
2. Edit `aria2.conf` file
3. Restart container to apply changes

### Rclone Automation

Configure Rclone to automatically sync downloads:
1. Set up remote in Rclone UI
2. Create sync script in container
3. Use cron or systemd timer for scheduling

### Custom File Browser Settings

File Browser settings can be customized through its web UI under Settings.

## Useful Commands

### View Logs
```bash
# In Coolify UI: Service → Logs
```

### Check Running Processes
```bash
# Exec into container in Coolify
ps aux
```

### Manual Aria2 Control
```bash
# Check Aria2 status
aria2c --version
```

## Links and Resources

- [Aria2 Documentation](https://aria2.github.io/)
- [AriaNg GitHub](https://github.com/mayswind/AriaNg)
- [File Browser Documentation](https://filebrowser.org/)
- [Rclone Documentation](https://rclone.org/)
- [Docker Image Source](https://github.com/wahyd4/aria2-ariang-docker)

## Success Indicators

Your deployment is successful when:

- ✅ AriaNg UI loads at your domain
- ✅ Can add and start downloads
- ✅ File Browser accessible at `/files` with admin login
- ✅ Rclone UI loads at `/rclone`
- ✅ Downloads appear in File Browser
- ✅ All services respond without errors

---

**Support**: For issues specific to this template, open an issue in the Awesome-Coolify-Templates repository.
