# debugging interface

- challenge description

![image.png](images/HTB/Hardware/debug_interface_images/image.png)

- after downloading the file , it’s

![image.png](images/HTB/Hardware/debug_interface_images/image%201.png)

- searching for `.sal` files i found that

![image.png](images/HTB/Hardware/debug_interface_images/image%202.png)

- so it’s logic analyzer let’s download the program.
- as we are working `usart` , we have to determine the baud rate , now the usart starts with `one bit`

![image.png](images/HTB/Hardware/debug_interface_images/image%203.png)

- at first it’s stream of ones that indicates that no data was sent and the first bit of frame indicates the start of transmission.
- now it’s Manchester encoding  , we will take the duration of short pulse as it have higher bit rate so if we took long pulse with lower bit rate we will miss data as the data will be faster than the observer.

![image.png](images/HTB/Hardware/debug_interface_images/image%204.png)

- let’s configure the analyzer

![image.png](images/HTB/Hardware/debug_interface_images/image%205.png)

- and bingo

![image.png](images/HTB/Hardware/debug_interface_images/image%206.png)

- `HTB{d38u991n9_1n732f4c35_c4n_83_f0und_1n_41m057_3v32y_3m83dd3d_d3v1c3!!52}`
