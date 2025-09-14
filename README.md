# abr_image_transport_interfaces

`abr_image_transport_interfaces` defines the **ROS 2 interfaces** (messages and services) used by the [`abr_image_transport`](../abr_image_transport) package.  
These interfaces allow nodes to exchange adaptive bitrate (ABR) video data and control parameters within the ROS 2 ecosystem.

---

## 📦 Overview

This package contains:

- **Messages** for transmitting compressed video frames with ABR metadata  
- **Services** for runtime configuration of encoder bitrate  

By separating interfaces into a standalone package, we ensure modularity and reusability across different ROS 2 nodes.

---

## Messages

### `AbrImage.msg`

A standalone, compact message for adaptive-bitrate compressed image frames.

```ros
# Standard ROS header
std_msgs/Header header

# Original image resolution
uint32 original_width
uint32 original_height

# Codec used for compression (e.g., "h264", "hevc")
string encoding

# Compressed image data (AVPacket)
uint8[] compressed_data
```

This message is the primary format for publishing ABR video frames.

#### Field Descriptions

- **`header`** — Standard ROS header (timestamp, frame_id)  
- **`original_width` / `original_height`** — Width and height of the source image in pixels  
- **`encoding`** — Codec identifier for `compressed_data` (e.g., `"h264"`, `"hevc"`)  
- **`compressed_data`** — Encoded video frame bytes (AVPacket-like)  


---

## Services

### `AbrParams.srv`

Allows dynamic adjustment of the encoder bitrate at runtime.

```ros
# Request
int32 bitrate

---
# Response
bool success
string message
```

#### Service Usage

- **`bitrate`** — Desired encoder bitrate in kbps  
- **`success`** — Indicates if the new bitrate was applied successfully  
- **`message`** — Additional information or error message  

> This service allows ABR video streams to adapt to changing network conditions on the fly.
