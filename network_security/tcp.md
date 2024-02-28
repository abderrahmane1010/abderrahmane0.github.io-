# Transmission Control Protocol TCP:

TCP protocol operations may be divided into three phases :

1. Connection establishment
   1. SYN (Client -> Server) : (Sequence number : A) (Acknowledgment number : 0) 
   2. SYN-ACK (Server -> Client) : (Sequence number : B) (Acknowledgment number : A+1) 
   3. ACK (Client -> Server) : (Sequence number : A+1) (Acknowledgment number : B+1) 
2. Data transfer phase
3. Connection termination

