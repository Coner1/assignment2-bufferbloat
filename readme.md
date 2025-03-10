[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/atebqxQy)
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
# Name : Jane Doe
# SID : 1234567
# CCID : jdoe
# - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


# Settings
(h1-s1)link delay = 10ms
(s1-h2)link delay = 10ms


# Part 2 Questions
## Part 2 - 1
Q: What was the mean and standard deviation of webpage fetch time when using the reno TCP congestion
algorithm for a buffer size of 10 packets? How did this result change with a buffer size of 50 packets?
A:
Buffer size = 10 packets
    webpage fetch time, Mean: 5.538s, Standard Deviation: 0.562s
Buffer size = 50 packets
    webpage fetch time, Mean: 6.040s, Standard Deviation: 2.448s

When the buffer size went from 10 to 50 packets, the average time to fetch a webpage got slower by about 0.5 seconds (from 5.538s to 6.040s), as seen in the console log(![Screenshot-run.png](screenshot%2FScreenshot-run.png)) and curl.txt from directories `data_reno_10` and `data_reno_50`. The spread also grew a lot, meaning the times varied more with the bigger buffer.
Here is why: 
A bigger buffer lets more packets wait in line before being sent. This slows down the webpage fetch because packets take longer to get through. The bigger spread happens because sometimes the line moves fast, and sometimes it’s slow, depending on how full the buffer gets. With a small buffer, things move quicker and stay steadier.

## Part 2 - 2
Q: Looking once again at the reno congestion algorithm, how are RTT measurements impacted by buffer size? Refer to the plots generated for the buffer size of 10 and 50.
A:
Buffer size = 10 packets
    RTT, Mean: 125.334ms, Standard Deviation: 25.244s
Buffer size = 50 packets
    RTT, Mean: 428.049ms, Standard Deviation: 169.552ms

RTT is how long it takes a signal to go and come back. With a bigger buffer (50 packets), the average RTT jumped from 125.334 ms to 428.049 ms—about 300 ms slower. The spread also got much bigger, showing more ups and downs. The plots from directories `data_reno_10` and `data_reno_50` clearly show this big jump.

Here is why: 
With a small buffer, packets move fast because there’s not much room to wait. A bigger buffer holds more packets, so they sit around longer before moving. This waiting makes RTT longer. The bigger spread comes from the buffer filling up unevenly—sometimes it’s quick, sometimes it’s a long wait.

## Part 2 - 3
Q: How does the cubic congestion algorithm compare to reno in terms of webpage fetch time (a measure of throughput) and ping RTT (a measure of latency)? Would your answer change if the link between the router and h2 had much higher bandwidth (note: this part of the question is for intellectual curiosity only and not part of the grade)?
A:
Comparison:
Buffer size = 10 packets
    webpage fetch time, Mean: 5.538s, Standard Deviation: 0.562s (reno)
    webpage fetch time, Mean: 5.850s, Standard Deviation: 0.879s (cubic)
    RTT, Mean: 125.334ms, Standard Deviation: 25.244ms (reno)
    RTT, Mean: 130.481ms, Standard Deviation: 21.429ms (cubic)
Buffer size = 50 packets
    webpage fetch time, Mean: 6.040s, Standard Deviation: 2.448s (reno)
    webpage fetch time, Mean: 8.764s, Standard Deviation: 2.099s (cubic)
    RTT, Mean: 428.049ms, Standard Deviation: 169.552ms (reno)
    RTT, Mean: 459.653ms, Standard Deviation: 128.381ms (cubic)

Cubic is a bit slower (5.850s vs. 5.538s) and has slightly more delay (130.481 ms vs. 125.334 ms), but its delay is steadier (smaller spread), as observed in console log(![Screenshot-run.png](screenshot%2FScreenshot-run.png)screenshot/Sc) and  `data_reno_10` and `data_cubic_10`. With a bigger buffer, Cubic is much slower (8.764s vs. 6.040s) and has more delay (459.653 ms vs. 428.049 ms), but its performance is more predictable (less spread), as seen in `data_reno_50` and `data_cubic_50`.

If the connection was faster: both might get faster fetch times and less delay. Cubic could do better than Reno because it’s built for fast networks. With a big buffer, Cubic might use the extra speed to catch up or beat Reno.

## Part 2 - 4
Q: Considering the buffer size of 50 packets, how does BBR’s performance, in terms of latency and throughput, compare to reno and cubic from your experiments? Which congestion control algorithm can better mitigate the bufferbloat problem? Explain your finding.
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

Speed: BBR is the fastest (5.851s), beating Reno (6.040s) and Cubic (8.764s). Its Standard Deviation is also smallest, so it’s more consistent, as shown in `data_bbr_50`. Delay: BBR has the least delay (384.315 ms) compared to Reno (428.049 ms) and Cubic (459.653 ms), but its Standard Deviation is bigger, meaning delay varies more, as observed in `data_reno_50`, `data_cubic_50`, and `data_bbr_50`.
Best for bufferbloat: BBR handles bufferbloat best. It keeps delay lower and speed higher than Reno and Cubic.
Why: Bufferbloat happens when too many packets get stuck in the buffer, slowing things down. Reno and Cubic wait for packets to get lost before slowing down, so they fill the big buffer, causing delays. BBR watches how fast the network is and how long packets take, then sends just enough to keep things moving. That’s why it’s faster and has less delay—it doesn’t let the buffer clog up as much.

## Part 2 - 5
Q: Describe in technical terms why increasing buffer size reduces performance, causing the bufferbloat effect. Be sure to explicitly reference the plots you generated and the relationship between TCP congestion control and buffer size.
A:
Increasing the buffer size reduces performance because it causes bufferbloat, where too many packets get stuck waiting in the buffer. This makes the network slower by increasing delay (RTT) and sometimes making webpage fetching take longer.
How it happens: TCP controls how fast data is sent. For Reno, it keeps sending packets until some get lost, then slows down. With a small buffer, it fills up fast, tells Reno to slow down, and keeps packets moving quickly. With a big buffer, it can hold more packets, so Reno keeps sending without stopping soon enough. This creates a long line of packets waiting, which adds delay and can slow down the whole process.

For Reno (10 packets): The blue line (TCP CWND) goes up and down rapidly. This quick change causes the RTT (green line), Curl Request (yellow areas), and Queue Length (red line) to also go up and down quickly. Overall, the CWND stays around a steady level, usually between 5-20 MSS, as seen in the plot from `data_reno_10`.
For Reno (50 packets): The blue line (TCP CWND) takes much more time to turn around and adjust because there is a larger buffer. With more space to hold packets, it doesn’t fill up as fast, so the CWND grows higher (up to 50 MSS or more) and takes longer to drop back down, as shown in the plot from `data_reno_50`.

Why it reduces performance: A bigger buffer lets Reno send more packets before slowing down, jamming the network with waiting packets. This raises delay (RTT) and can slow speed, as the plots from `data_reno_10` and `data_reno_50` show the Queue Length (red) spiking higher with 50 packets, pushing RTT (green) up significantly.


# Part 3 Questions

## Part 3 - 1
Q: Considering how the TCP congestion window size changes and the queue length, do you see any difference
in the plots from Part 2 and Part 3? Give a brief explanation for the result you see.

A:
Yes, there are differences in the plots between Part 2 (no loss) and Part 3 (with 5% loss). 
Looking at the output directories like lossy_reno_10 and lossy_reno_50:

TCP CWND (blue line): In Part 3, the CWND drops more often and stays lower compared to Part 2. 
For example, in lossy_reno_10, the CWND fluctuates rapidly between 20-50 MSS instead of 50-100 MSS, and in lossy_reno_50, it takes longer to recover but doesn’t grow as high.
Queue Length (red line): The queue length spikes are shorter and less frequent in Part 3. In lossy_reno_50, it peaks around 20-30 MSS during requests, compared to 40-50 MSS in Part 2.
Explanation:

Packet loss (5%) tricks Reno into thinking the network is full, so it reduces the CWND quickly to avoid sending too much. 
This lowers the queue length because fewer packets are sent, but it also means the network doesn’t fill the buffer as much. 
The rapid drops in CWND in the plots show Reno reacting to loss, unlike the steadier growth in Part 2.

## Part 3 - 2
Q: Considering the buffer size of 50 packets, which of the three congestion control algorithms was most per-
formant (in terms of throughput) in the presence of increased random loss? Why do you think this is the
case?

A:
Based on the output directories lossy_reno_50, lossy_cubic_50, and lossy_bbr_50, 
Cubic was the most performant in terms of throughput with a 50-packet buffer in a lossy network. 
The average download times from screenshot show:

Reno: 4.3s ± 0.7s
Cubic: 4.1s ± 0.6s
BBR: 5.3s ± 1.0s
which means:
Cubic has the lowest average download time (4.1s), meaning it delivers the highest throughput. 
It’s also the most consistent, with the smallest variation (±0.6s). 
BBR is the slowest (5.3s) and has the most variation (±1.0s).

Here are my thoughts on why this happened:
In a lossy network (5% loss), Reno and Cubic are designed to slow down when packets are lost, thinking the network is full. 
But Cubic is better at recovering quickly because it increases its sending rate more aggressively after a loss compared to Reno. 
This helps Cubic keep sending data faster, leading to better throughput (lower fetch time). 
BBR, on the other hand, focuses on delay and speed, not just loss, so random packet drops confuse it more, slowing it down in this case (higher fetch time). 
