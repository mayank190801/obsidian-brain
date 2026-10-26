
2024-06-27 18:51
Status: #child
Tags: [[4 - Tags/system design|system design]] [[networks]]

# TCP vs UDP

- **TCP** is a connection-oriented protocol that ensures reliable, ordered, and error-checked delivery of a stream of bytes between applications.
- **UDP** is a connectionless protocol that sends messages, called datagrams, without establishing a prior connection and without guaranteeing reliability or order.

TCP (Transmission Control Protocol)
- **Reliability**: TCP ensures that data is delivered accurately and in order, retransmitting lost or corrupted packets.
- **Connection-Oriented**: Establishes a connection between sender and receiver before transmitting data.
- **Flow Control**: Manages data transmission rate to prevent network congestion.
- **Congestion Control**: Adjusts the transmission rate based on network traffic conditions.
- **Acknowledgements and Retransmissions**: Uses acknowledgments to confirm receipt of data and retransmits if necessary.
- Applications where reliability and order are critical, like web browsing (HTTP/HTTPS), email (SMTP, POP3, IMAP), and file transfers (FTP).

UDP (User Datagram Protocol)
- **Low Overhead**: Does not establish a connection, leading to lower overhead and latency.
- **Unreliable Delivery**: Does not guarantee message delivery, order, or error checking.
- **Speed**: Faster than TCP due to its simplicity and lack of retransmission mechanisms.
- **No Congestion Control**: Does not reduce transmission rates under network congestion.
- Applications that require speed and can tolerate some loss of data, like streaming video or audio, online gaming, or VoIP (Voice over Internet Protocol).

###### Key Differences
- Reliability - (accurately and in order, maybe lost or arrive out of order)
- Connection - (establishes a connection, without establishing a connection)
- Speed - (slower due to handshake, retransmission and congestion control, no overhead just fast)
- Data Integrity - (high data integrity, lower data integrity)
- Use case - (data accuracy, speed is more critical)






# **References**