---
title: "Secure Digital Challenge"
date: 2025-03-05 00:00:00
categories: [Hardware]
tags: [Hardware,Challenges,HackTheBox]
---

# secure digital

- challenge description

![image.png](images/HTB/Hardware/secure_digital/image.png)

- i found this article https://learn.sparkfun.com/tutorials/microsd-sniffer-hookup-guide/all
- after searching for micro sd card i found out that it’s using spi communication
- so we have to identify 4 pins

```jsx
1 - clock
2 - mosi
3 - miso
4 - chip select
```

- from the challenge discreption the key is stored on the microsd card so we transfer from it , so it’s `miso`
- i will use channel 3 as clock as it’s periodic

![image.png](images/HTB/Hardware/secure_digital/image%201.png)

- and channel 2 as select as it’s stay constant for long time so it means that it’s out turn to communicate and it also changes from the high to low before the data to be sent (it’s known from fluctuations)

![image.png](images/HTB/Hardware/secure_digital/image%202.png)

- for channel 0 and 1 it’s doesn’t matter what is mosi and what is miso as both send data.
- and the flag is

![image.png](images/HTB/Hardware/secure_digital/image%203.png)

- `HTB{unp2073c73d_532141_p2070c015_0n_53cu23_d3v1c35}`
