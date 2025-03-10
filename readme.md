[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/atebqxQy)
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# Name : Jane Doe
# SID : 1234567
# CCID : jdoe
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

# Part 2 Questions

## Part 2 - 1
Q: What was the mean and standard deviation of webpage fetch time when using the reno TCP congestion
algorithm for a buffer size of 10 packets? How did this result change with a buffer size of 50 packets?
A:
Buffer size = 10 packets
    webpage fetch time, Mean: 5.538s, Standard Deviation: 0.562s
Buffer size = 50 packets
    webpage fetch time, Mean: 6.040s, Standard Deviation: 2.448s

When the buffer size went from 10 to 50 packets, 
the average time to fetch a webpage got slower by about 0.5 seconds (from 5.538s to 6.040s). 
The spread also grew a lot, meaning the times varied more with the bigger buffer.
Here is why: 
A bigger buffer lets more packets wait in line before being sent. 
This slows down the webpage fetch because packets take longer to get through. 
The bigger spread happens because sometimes the line moves fast, and sometimes it’s slow, 
depending on how full the buffer gets. With a small buffer, things move quicker and stay steadier.
## Part 2 - 2
Q: Looking once again at the reno congestion algorithm, how are RTT measurements impacted by buffer size?
Refer to the plots generated for the buffer size of 10 and 50.
Buffer size = 10 packets
    RTT, Mean: 125.334ms, Standard Deviation: 25.244s
Buffer size = 50 packets
    RTT, Mean: 428.049ms, Standard Deviation: 169.552ms

RTT is how long it takes a signal to go and come back. 
With a bigger buffer (50 packets), the average RTT jumped from 125.334 ms to 428.049 ms—about 300 ms slower. 
The spread also got much bigger, showing more ups and downs. The plots would show this big jump.

Here is Why:
With a small buffer, packets move fast because there’s not much room to wait. 
A bigger buffer holds more packets, so they sit around longer before moving. 
This waiting makes RTT longer. The bigger spread comes from the buffer filling up unevenly—sometimes it’s quick, 
sometimes it’s a long wait.

## Part 2 - 3
Q: How does the cubic congestion algorithm compare to reno in terms of webpage fetch time (a measure of
throughput) and ping RTT (a measure of latency)? Would your answer change if the link between the router
and h2 had much higher bandwidth (note: this part of the question is for intellectual curiosity only and not
part of the grade)?
Comparison:
Buffer size = 10 packets
    webpage fetch time, Mean: 5.538s, Standard Deviation: 0.562s(reno)
    webpage fetch time, Mean: 5.850s, Standard Deviation: 0.879s(cubic)
    RTT, Mean: 125.334ms, Standard Deviation: 25.244ms(reno)
    RTT, Mean: 130.481ms, Standard Deviation: 21.429ms(cubic)
Buffer size = 50 packets
    webpage fetch time, Mean: 6.040s, Standard Deviation: 2.448s(reno)
    webpage fetch time, Mean: 8.764s, Standard Deviation: 2.099s(cubic)
    RTT, Mean: 428.049ms, Standard Deviation: 169.552ms(reno)
    RTT, Mean: 459.653ms, Standard Deviation: 128.381ms(cubic)
Cubic is a bit slower (5.850s vs. 5.538s) and has slightly more delay (130.481 ms vs. 125.334 ms), 
but its delay is steadier (smaller spread).

With a bigger buffer, Cubic is much slower (8.764s vs. 6.040s) and has more delay (459.653 ms vs. 428.049 ms), 
but its performance is more predictable (less spread).

If the connection was faster:
both might get faster fetch times and less delay. 
Cubic could do better than Reno because it’s built for fast networks. 
With a big buffer, Cubic might use the extra speed to catch up or beat Reno.

## Part 2 - 4
Q: Considering the buffer size of 50 packets, how does BBR’s performance, in terms of latency and throughput,
compare to reno and cubic from your experiments? Which congestion control algorithm can better
mitigate the bufferbloat problem? Explain your finding.
A:
Comparison (Buffer size = 50 packets):
Fetch time (Speed):
    Reno: Average = 6.040s, Standard Deviation = 2.448s
    Cubic: Average = 8.764s, Standard Deviation = 2.099s
    BBR: Average = 5.851s, Standard Deviation = 1.331s
RTT (Delay):
    Reno: Average = 428.049 ms, Standard Deviation = 169.552 ms
    Cubic: Average = 459.653 ms, Standard Deviation = 128.381 ms
    BBR: Average = 384.315 ms, Standard Deviation = 202.408 ms

Speed: BBR is the fastest (5.851s), beating Reno (6.040s) and Cubic (8.764s). Its Standard Deviation is also smallest, so it’s more consistent.
Delay: BBR has the least delay (384.315 ms) compared to Reno (428.049 ms) and Cubic (459.653 ms), but its Standard Deviation is bigger, meaning delay varies more.
Best for bufferbloat:
BBR handles bufferbloat best. It keeps delay lower and speed higher than Reno and Cubic.
Why:
Bufferbloat happens when too many packets get stuck in the buffer, slowing things down. 
Reno and Cubic wait for packets to get lost before slowing down, so they fill the big buffer, causing delays. 
BBR watches how fast the network is and how long packets take, then sends just enough to keep things moving. 
That’s why it’s faster and has less delay—it doesn’t let the buffer clog up as much.

## Part 2 - 5
Q: Describe in technical terms why increasing buffer size reduces performance, causing the bufferbloat effect.
Be sure to explicitly reference the plots you generated and the relationship between TCP congestion control
and buffer size.
# Part 3 Questions

## Part 3 - 1
Q: Considering how the TCP congestion window size changes and the queue length, do you see any difference
in the plots from Part 2 and Part 3? Give a brief explanation for the result you see.



## Part 3 - 2
Q: Considering the buffer size of 50 packets, which of the three congestion control algorithms was most per-
formant (in terms of throughput) in the presence of increased random loss? Why do you think this is the
case?