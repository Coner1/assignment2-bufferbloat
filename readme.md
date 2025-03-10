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

## Part 2 - 2
Q: Looking once again at the reno congestion algorithm, how are RTT measurements impacted by buffer size?
Refer to the plots generated for the buffer size of 10 and 50.

## Part 2 - 3
Q: How does the cubic congestion algorithm compare to reno in terms of webpage fetch time (a measure of
throughput) and ping RTT (a measure of latency)? Would your answer change if the link between the router
and h2 had much higher bandwidth (note: this part of the question is for intellectual curiosity only and not
part of the grade)?

## Part 2 - 4
Q: Considering the buffer size of 50 packets, how does BBR’s performance, in terms of latency and throughput,
compare to reno and cubic from your experiments? Which congestion control algorithm can better
mitigate the bufferbloat problem? Explain your finding.

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