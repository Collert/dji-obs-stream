# DJI-OBS-Stream – Docker

This Docker image packages NGINX for RTMP streaming from a DJI drone (or any RTMP-capable device) so you can easily set up a streaming endpoint without manually configuring NGINX.

Prebuilt images are available on [Docker Hub](https://hub.docker.com/r/prochac/dji-obs-stream/tags) for both:

- `amd64` (most desktop/server machines)
- `arm64` (Raspberry Pi, Apple Silicon Macs, etc.)

---

## Image Variants

| Tag      | Base Image | Size (approx.) |
|----------|------------|----------------|
| `latest` | `ubuntu`   | 581 MB          |
| `alpine` | `alpine`   | 149 MB          |

If you’re unsure which to use, start with `alpine` for smaller size, unless you need Ubuntu-specific tooling.

---

## Quick Start

1. **Pull the image** (replace `<tag>` with `latest` or `alpine`):

   ```bash
   docker pull prochac/dji-obs-stream:<tag>
   ```

2. **Run the container** (basic example):

   ```bash
   docker run -d \
     --name dji-obs-stream \
     -p 1935:1935 \
     prochac/dji-obs-stream:<tag>
   ```

3. **Stream to it from your DJI drone** by setting the RTMP URL in your DJI app to:

   ```url
   rtmp://<your-server-ip>/live/stream
   ```

4. **View the stream in OBS**:
   - Add a **Media Source** or **RTMP Source** in OBS.
   - Use the same RTMP URL above.

---

## Building Locally (Optional)

If you want to customize the configuration, clone the repo and build your own image:

```bash
git clone https://github.com/<repo>.git
cd DJI-OBS-Stream/Docker
docker build -t my-dji-obs-stream .
```

---

## Notes

- Make sure port `1935` is open in your firewall if streaming over the internet.
- `latest` and `alpine` images are **built** for both `amd64` and `arm64` architectures.
