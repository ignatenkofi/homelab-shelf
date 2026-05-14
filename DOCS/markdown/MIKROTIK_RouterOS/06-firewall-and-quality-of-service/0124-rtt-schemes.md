## RTT Schemes 

The CAKE queue discipline allows you to specify the Round Trip Time (RTT) it should consider when managing traffic. This is important because the time it takes for a packet to travel from a source to a destination and back impacts how CAKE manages network congestion. If the actual RTT of your network is close to the value you specify, both the throughput and latency of your network should be well managed. 

Here are the RTT settings you can use, what they mean, and when you might use them: 

1. `rtt TIME` : Manually specify an RTT. This is for advanced users who know the exact RTT they want to use. 

2. `datacentre` : This is for extremely high-performance networks, such as a 10 Gigabit Ethernet (10GigE) network in a data center. The RTT is assumed to be 100 microseconds. Example: Use this if you're managing network traffic in a high-capacity data center. 

3. `lan` : This is for pure Ethernet networks, such as those you might find in a home or office environment. The RTT is assumed to be 1 millisecond. Example: Use this if you're managing traffic on a wired home or office network, but not when shaping for an Internet access link. 

4. `metro` : This is for traffic mostly within a single city. The RTT is assumed to be 10 milliseconds. Example: Use this if you're managing traffic for a network in a single city, like a city-wide corporate network. 

5. `regional` : This is for traffic mostly within a European-sized country. The RTT is assumed to be 30 milliseconds. Example: Use this if you're managing traffic for a network that spans a country. 

6. `internet` : This is suitable for most Internet traffic. The RTT is assumed to be 100 milliseconds. Example: Use this if you're managing general Internet traffic on a typical broadband connection. 

7. `oceanic` : This is for Internet traffic with generally above-average latency, such as that suffered by Australasian residents. The RTT is assumed to be 300 milliseconds. Example: Use this if you're managing traffic in a location with high latency, like Australia or New Zealand. 

8. `satellite` : This is for traffic via geostationary satellites. The RTT is assumed to be 1000 milliseconds (1 second). Example: Use this if you're managing traffic for a network that uses a satellite internet connection. 

9. `interplanetary` : This disables Active Queue Management (AQM) actions, because the RTT is so long (3600 seconds). It's named "interplanetary" because the distance from Earth to Jupiter is about one light-hour. Example: This is not typically used in standard networking situations, but might be useful in extremely high latency situations, such as experimental long-distance communication scenarios. 

Remember, these are guidelines, and the best setting depends on the specific characteristics and requirements of your network. If you are unsure, the `int` 1 `ernet` setting is a good starting point for most scenarios​ ​.
