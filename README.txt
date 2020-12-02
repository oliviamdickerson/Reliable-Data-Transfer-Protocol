A_output: For this function, I took the message that was received from layer 5, created a new packet, and set the packet payload to a byte object of the message data. Then I calculated the checksum by adding all the bytes of the sequence number, the ack number, and the payload data. I then sent this packet to the B side of layer 3, then started the timer. 

A_input: For this function, I calculated the checksum for the packet that was received and if it matched the checksum inside the packet and the acknum was correct (matched the seqnum of the packet that was sent to the B side), stopped the A timer and printed that the ACK packet received from the B side was not corrupted. If the checksum didn’t match and the packet was corrupted, wait for timeout and retransmission. 

A_timerinterrupt: For this function, when a timer interrupt occurs, the original message that was sent from layer 5 to the A side is resent to the B side because some error occurred, wether it was packet loss or corruption.

A_init: I did not add any code to this function.

B_input: When a packet is received on the B side, I recalculate the checksum to see if it matches the checksum included in the packet. If the checksums are not equal this means the packet was corrupted, the method does nothing and waits until the A side times out for retransmission. If the checksums do match and the seqnum is correct, I create and send an ack packet with the correct ack number to the A side.

B_init: I did not add any code to this function.