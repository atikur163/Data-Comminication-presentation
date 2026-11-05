Real-time Transport Protocol (RTP)

A presentation-oriented guide to understanding how the Real-time
Transport Protocol (RTP) uses the User Datagram Protocol (UDP) to
deliver real-time audio and video over IP networks.
Main idea: RTP commonly runs directly over UDP. UDP transports RTP
packets across the network, while RTP adds information needed to
reconstruct and play real-time media, such as sequence numbers,
timestamps, and payload-type identifiers.

Table of Contents
- 1. Introduction
- 2. What Is RTP?
- 3. What Is UDP?
- 4. RTP and UDP Relationship
- 5. Protocol Architecture
- 6. How RTP Works Over UDP
- 7. Important RTP Header Fields
- 8. Responsibilities of RTP and
  UDP
- 9. Why Is UDP Preferred for RTP?
- 10. Limitations and Important
  Considerations
- 11. Real-World Applications
- 12. RTP, UDP, and IP: A Simple
  Example
- 13. Key Points for Presentation
- 14. Conclusion
- 15. References
1. Introduction
Modern communication systems frequently transmit audio and video in real
time. Examples include video conferencing, internet telephony, live
streaming, and online meetings.

These applications need to deliver media with very little delay. The
Real-time Transport Protocol (RTP) helps by carrying real-time media
and providing information that allows the receiver to identify, order,
and time media packets.

RTP commonly uses UDP as its underlying transport protocol. UDP
provides a lightweight way to send packets without establishing a
connection or waiting for retransmission of lost packets.

This relationship is important because real-time applications often
prefer timely delivery over waiting for every missing packet to be
recovered.
2. What Is RTP?
RTP (Real-time Transport Protocol) is a protocol designed to carry
real-time audio, video, and other time-sensitive data over IP networks.

RTP is commonly treated as an application-layer protocol. It works
closely with transport-layer protocols, especially UDP.
Main functions of RTP
- Sequence numbering: Helps the receiver detect missing packets
  and restore packet order.
- Timestamping: Identifies the sampling time of media data and
  helps with playback timing and synchronization.
- Payload identification: Indicates the type of media encoding
  carried in a packet.
- Source identification: Uses a Synchronization Source Identifier
  (SSRC) to identify the RTP stream source.
- Media synchronization: Works with RTCP information to support
  synchronization between related media streams, such as audio and
  video.
Important: RTP does not itself guarantee packet delivery, prevent
packet loss, or reserve network bandwidth.
3. What Is UDP?
UDP (User Datagram Protocol) is a connectionless transport-layer
protocol. It sends independent datagrams from one application endpoint
to another.

Unlike TCP, UDP does not establish a connection before sending data and
does not provide built-in retransmission or in-order delivery.
Main features of UDP
- Connectionless communication.
- Low protocol overhead.
- No built-in retransmission of lost packets.
- No guarantee that packets will arrive in order.
- Uses port numbers to identify application endpoints.
- Includes an optional error-checking mechanism through its checksum
  field (the checksum is mandatory in IPv6, subject to defined
  exceptions).
UDP is useful for applications where low delay is important, including
real-time voice and video communication.
4. RTP and UDP Relationship
RTP commonly operates directly on top of UDP.

When an application sends real-time media:
1. The media application creates audio or video data.
2. RTP adds a header containing information such as a sequence number,
   timestamp, and payload type.
3. UDP adds its own header, including source and destination port
   numbers.
4. IP adds the information needed to route the packet across the
   network.
5. The receiving device processes the packet in the reverse order.
Encapsulation
+--------------------------------------+
|              IP Header               |
+--------------------------------------+
|              UDP Header              |
+--------------------------------------+
|              RTP Header              |
+--------------------------------------+
|            Media Payload             |
|          (Audio or Video)            |
+--------------------------------------+
The complete RTP packet is carried as the payload of a UDP datagram. The
UDP datagram is then carried inside an IP packet.
5. Protocol Architecture
A simplified Internet protocol stack for RTP-based communication is:
+--------------------------------------+
|       Application (Voice/Video)      |
+--------------------------------------+
|                 RTP                  |
+--------------------------------------+
|                 UDP                  |
+--------------------------------------+
|                  IP                  |
+--------------------------------------+
|       Link Layer (Wi-Fi/Ethernet)    |
+--------------------------------------+
|              Physical                |
+--------------------------------------+
RTP is an application-level media transport protocol that uses services
provided by lower layers. UDP is the transport-layer protocol commonly
used beneath RTP, while IP provides addressing and routing.
6. How RTP Works Over UDP
The following steps describe a typical RTP-over-UDP communication
process:
1. Media capture: A microphone or camera captures audio or video.
2. Encoding: The application encodes the captured media using a
   suitable codec.
3. Packetization: The encoded media is divided into smaller units
   for transmission.
4. RTP header creation: RTP adds sequence numbers, timestamps,
   payload-type information, and a source identifier.
5. UDP encapsulation: UDP places the RTP packet inside a datagram
   and adds port information.
6. IP transmission: IP routes the packet toward the destination.
7. Reception: The destination receives the packet and passes its
   payload to UDP and then RTP.
8. Media reconstruction: The receiving application uses RTP
   information to detect packet order, handle timing, and prepare the
   media for playback.
A receiver may use a jitter buffer to smooth variations in packet
arrival time before playing the media.
7. Important RTP Header Fields
The standard RTP header has a minimum size of 12 bytes, before any
optional CSRC entries, header extensions, or payload data.
  Field                                         Size Purpose
  Version (V)                                 2 bits Identifies the RTP
version.

  Padding (P)                                  1 bit Indicates whether
padding is present.

  Extension (X)                                1 bit Indicates whether a
header extension
follows the fixed
header.

  CSRC Count (CC)                             4 bits Indicates the number
of CSRC identifiers.

  Marker (M)                                   1 bit Provides a
profile-defined
marker, often used to
indicate an important
event in a media
stream.

  Payload Type (PT)                           7 bits Identifies the media
payload format.

  Sequence Number                            16 bits Helps detect packet
loss and restore
packet order.

  Timestamp                                  32 bits Represents the
sampling instant of
the media data.
SSRC                                       32 bits Identifies the
synchronization
source.
Why are sequence numbers and timestamps important?
- Sequence numbers help the receiver identify missing packets and
  arrange received packets in their intended order.
- Timestamps help the receiver determine when media should be
  played and support synchronization.
These fields are especially useful because UDP does not guarantee packet
ordering or delivery.
8. Responsibilities of RTP and UDP
RTP and UDP have different but complementary responsibilities.
  RTP                                 UDP
  Adds media-specific information.    Provides transport of datagrams.

  Uses sequence numbers.              Does not guarantee packet order.

  Provides timestamps.                Does not provide media timing.

  Identifies payload formats.         Uses port numbers for application
endpoints.

  Identifies synchronization sources. Provides a lightweight,
connectionless transport service.
Helps the receiver interpret        Carries RTP packets across the
real-time media packets.            network.
In short: UDP transports the data, while RTP explains how the
real-time media data should be interpreted and timed.
9. Why Is UDP Preferred for RTP?
UDP is commonly preferred for RTP because real-time communication is
highly sensitive to delay.
1. Low overhead
UDP has an 8-byte header, which keeps transport overhead relatively
small.
2. No connection establishment
UDP does not require a connection handshake before sending data. This
helps avoid connection setup delay.
3. No built-in retransmission delay
If a packet is lost, UDP does not automatically wait for retransmission.
For live audio or video, a late packet may be less useful than a packet
that arrives on time.
4. Supports continuous media transmission
UDP can carry a continuous stream of independent datagrams, making it
suitable for packetized audio and video.
5. Application-level control
RTP-based applications can use sequence numbers, timestamps, jitter
buffers, and feedback mechanisms to manage media delivery.
10. Limitations and Important Considerations
Although RTP over UDP is suitable for real-time communication, it has
limitations:
- Packet loss: UDP does not automatically retransmit lost
  datagrams.
- Packet reordering: Packets may arrive in a different order from
  the order in which they were sent.
- Jitter: Packet arrival times may vary.
- No delivery guarantee: UDP does not guarantee that a datagram
  will reach its destination.
- No built-in congestion control: The application must use
  suitable congestion-control mechanisms to avoid overloading the
  network.
- Security: RTP alone does not provide encryption or
  authentication. Secure Real-time Transport Protocol (SRTP) can
  provide media confidentiality, authentication, and replay
  protection.
RTP also has an associated control protocol called RTCP (RTP Control
Protocol). RTCP provides monitoring and feedback information, such as
reception statistics, and can support synchronization between media
streams.
11. Real-World Applications
RTP over UDP is commonly used in:
- Video conferencing systems.
- Voice over IP (VoIP).
- Internet-based telephone services.
- Live audio and video communication.
- Online meetings and collaboration tools.
- Real-time media transmission and monitoring systems.
The exact transport and media architecture depends on the application.
RTP is commonly carried over UDP, but it is not limited to UDP in every
possible deployment.
12. RTP, UDP, and IP: A Simple Example
Imagine a person speaking during a video call.
1. The microphone captures the speaker's voice.
2. The application encodes the voice into digital audio.
3. RTP divides the media into packets and adds sequence numbers and
   timestamps.
4. UDP carries each RTP packet using the selected source and
   destination ports.
5. IP routes the packets to the receiver.
6. The receiver uses RTP information to organize and time the audio.
7. The speaker's voice is played through the receiver's speakers.
This process happens continuously, allowing people to communicate with
minimal delay.
13. Key Points for Presentation
- RTP stands for Real-time Transport Protocol.
- UDP stands for User Datagram Protocol.
- RTP is commonly carried directly over UDP.
- RTP adds sequence numbers, timestamps, payload-type information, and
  source identification.
- UDP provides lightweight, connectionless datagram transport.
- IP is responsible for addressing and routing packets.
- RTP does not guarantee delivery or eliminate packet loss.
- RTCP provides control and monitoring information associated with
  RTP.
- RTP over UDP is widely used for real-time audio and video
  applications.
One-line explanation
RTP organizes and identifies real-time media data, while UDP
transports that data quickly across an IP network.
14. Conclusion
RTP and UDP work together to support real-time multimedia communication.
RTP adds the information needed to interpret, sequence, and time audio
and video packets, while UDP provides a lightweight transport mechanism
with low overhead.

This combination is useful for voice calls, video conferencing, and
other time-sensitive applications where minimizing delay is important.

Therefore, the statement "RTP depends directly on UDP" describes the
common RTP-over-UDP architecture. More precisely, RTP commonly uses UDP
as its underlying transport protocol, although the RTP specification is
not restricted exclusively to UDP.
15. References
1. Schulzrinne, H., Casner, S., Frederick, R., and Jacobson, V. RFC
   3550: RTP: A Transport Protocol for Real-Time Applications.
   IETF, 2003. https://www.rfc-editor.org/rfc/rfc3550
2. Postel, J. RFC 768: User Datagram Protocol. IETF, 1980.
   https://www.rfc-editor.org/rfc/rfc768
3. Schulzrinne, H. and Casner, S. RFC 3551: RTP Profile for Audio and
   Video Conferences with Minimal Control. IETF, 2003.
   https://www.rfc-editor.org/rfc/rfc3551
4. Baugher, M., McGrew, D., Naslund, M., Carrara, E., and Norrman, K.
   RFC 3711: The Secure Real-time Transport Protocol (SRTP).
   IETF, 2004. https://www.rfc-editor.org/rfc/rfc3711
