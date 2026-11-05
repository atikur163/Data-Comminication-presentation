# Real-Time Transport Protocol (RTP)

### 1. Introduction
Real-Time Transport Protocol (RTP) enables the transmission of audio and video over IP networks. It is widely used in video conferencing, VoIP, and online meetings.

RTP commonly operates over UDP to support low-latency communication.

### 2. What Is RTP?
RTP is a protocol designed for delivering real-time multimedia data.

**Key Functions:**
- **Sequence Number:** Detects packet loss and maintains packet order.
- **Timestamp:** Supports correct media playback timing.
- **Payload Type:** Identifies the media format.
- **SSRC:** Identifies the source of an RTP stream.

### 3. What Is UDP?
User Datagram Protocol (UDP) is a connectionless transport-layer protocol.

**Key Features:**
- Low transmission overhead.
- No connection establishment.
- No built-in retransmission.
- No guaranteed packet delivery or ordering.
- Uses port numbers for communication.

### 4. Relationship Between RTP and UDP
RTP commonly uses UDP as its underlying transport protocol.

**Data Encapsulation:**

IP Header → UDP Header → RTP Header → Audio/Video Data

- RTP adds media-related information.
- UDP transports RTP packets.
- IP handles addressing and routing.

### 5. How RTP Works Over UDP
1. A microphone or camera captures media.
2. The application encodes the media.
3. The media is divided into packets.
4. RTP adds sequence numbers and timestamps.
5. UDP encapsulates the RTP packets.
6. IP delivers packets to the destination.
7. The receiver processes and plays the media.

### 6. Important RTP Header Fields
The standard RTP header has a minimum size of **12 bytes**.

| Field | Function |
|---|---|
| Version | Identifies RTP version |
| Payload Type | Specifies media format |
| Sequence Number | Detects packet loss and ordering |
| Timestamp | Maintains playback timing |
| SSRC | Identifies the media source |
| Marker | Indicates a profile-defined event |

### 7. Why Is UDP Preferred?
UDP is commonly preferred for RTP because it offers:

- Low protocol overhead.
- Faster transmission without connection setup.
- No automatic retransmission delays.
- Efficient support for continuous media.
- Flexibility for application-level media management.

### 8. Limitations of RTP over UDP
- Packet loss may occur.
- Packets may arrive out of order.
- Network delay variation (jitter) can affect playback.
- Delivery is not guaranteed.
- Additional security and congestion-control mechanisms may be required.

**RTCP (RTP Control Protocol)** provides monitoring, reception statistics, and feedback.

### 9. Real-World Applications
RTP over UDP is commonly used in:
- Video conferencing.
- Voice over IP (VoIP).
- Online meetings.
- Live audio and video communication.
- Real-time multimedia applications.

### 10. Conclusion
RTP and UDP work together to enable efficient real-time multimedia communication.

RTP provides sequencing, timing, and media identification, while UDP delivers packets with low overhead.

**In simple terms: RTP organizes the media; UDP transports it.**

### References
1. RFC 3550 – RTP: A Transport Protocol for Real-Time Applications.
2. RFC 768 – User Datagram Protocol.
3. RFC 3551 – RTP Profile for Audio and Video Conferences.
4. RFC 3711 – Secure Real-time Transport Protocol (SRTP).
