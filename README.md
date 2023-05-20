# Reliable-UDP-Protocol-Networks
Sender:
This code implements a Reliable UDP (User Datagram Protocol) protocol for transmitting a file from a sender to a receiver over a network. The code first defines a function to plot the packet transmission times, and another function to divide the file into packets. It then defines the main function `send`, which takes the file path, receiver IP address, and receiver port as input.

Inside the `send` function, the code creates a UDP socket and sets a timeout interval for receiving acknowledgments. It then divides the file into packets and initializes variables for maintaining the sending window, congestion control, and retransmission counts. The code then enters a loop that sends packets and receives acknowledgments until all packets have been acknowledged.

The loop sends packets at an accelerating rate as long as there is no timeout error or loss. The congestion control is implemented using the slow-start algorithm and the congestion avoidance algorithm. The code records the sent packets and their transmission times, and also records the acknowledged packets and their acknowledgment times. It then updates the sending window and repeats the process until all packets have been acknowledged.

If a timeout error occurs or loss is detected, the code resets the congestion control variables and retransmits the unacknowledged packets. The code continues to retransmit until all packets have been acknowledged.

Finally, the code calculates and prints the transfer statistics, including the transfer start and end times, elapsed time, number of packets, number of bytes, number of retransmissions, average transfer rate, and lossrate. It also calls the `plot_packet_times` function to plot the packet transmission times.

Receiver: 
The UDP receiver receives data packets from a sender and stores them in a buffer until all packets for a file have been received. Once all packets for a file have been received, the receiver combines the packets to create the original file and saves it to disk. The code uses the socket library to create a UDP socket and bind it to a specified IP address and port number.

The `unpack_packet()` function takes a packet as input and unpacks it into its constituent parts: packet ID, file ID, application data, and trailer value. The function returns these values as separate variables.

The `pack_ack_packet()` function takes a packet ID and file ID as input and packs them into an acknowledgement packet.

The `receiver()` function is the main function that listens for incoming packets and processes them. It initializes variables for the expected packet ID, file ID, and data buffer. The function continuously receives packets until it receives the last packet for a file (indicated by a trailer value of 0xFFFF). For each received packet, the function first unpacks the packet using the `unpack_packet()` function. If the packet ID matches the expected packet ID and the file ID is not -1, the function adds the packet data to the data buffer and sends an acknowledgement packet to the sender with the last correctly received packet ID. If the trailer value is 0xFFFF, the function combines the packets in the data buffer to create the original file and saves it to disk.Note that the code still needs some additional implementation to handle colored images and to handle cases where the data buffer size exceeds 10 MiB. Additionally, the code includes commented-out code for discarding packets and sending an acknowledgement for the last correctly received packet if the received packet ID does not match the expected packet ID.
