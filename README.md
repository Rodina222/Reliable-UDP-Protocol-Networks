# Reliable-UDP-Protocol-Networks
This code implements a Reliable UDP (User Datagram Protocol) protocol for transmitting a file from a sender to a receiver over a network. The code first defines a function to plot the packet transmission times, and another function to divide the file into packets. It then defines the main function `send`, which takes the file path, receiver IP address, and receiver port as input.

Inside the `send` function, the code creates a UDP socket and sets a timeout interval for receiving acknowledgments. It then divides the file into packets and initializes variables for maintaining the sending window, congestion control, and retransmission counts. The code then enters a loop that sends packets and receives acknowledgments until all packets have been acknowledged.

The loop sends packets at an accelerating rate as long as there is no timeout error or loss. The congestion control is implemented using the slow-start algorithm and the congestion avoidance algorithm. The code records the sent packets and their transmission times, and also records the acknowledged packets and their acknowledgment times. It then updates the sending window and repeats the process until all packets have been acknowledged.

If a timeout error occurs or loss is detected, the code resets the congestion control variables and retransmits the unacknowledged packets. The code continues to retransmit until all packets have been acknowledged.

Finally, the code calculates and prints the transfer statistics, including the transfer start and end times, elapsed time, number of packets, number of bytes, number of retransmissions, average transfer rate, and lossrate. It also calls the `plot_packet_times` function to plot the packet transmission times.
