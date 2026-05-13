## Spectral History 

**==> picture [505 x 162] intentionally omitted <==**

```
/interface wireless spectral-history <wireless interface name>
```

Plots spectrogram. Legend and frequency ruler is printed every 24 lines. Numbers in the ruler correspond to the value at their leftmost character position. Power values that fall in different ranges are printed as different colored characters with the same foreground and background color, so it is possible to copy and paste the terminal output of this command. 

- value -- select value that is plotted on the output. 'interference' is special as it shows detected interference sources (affected by the 'classifysamples' parameter) instead of power readings, and cannot be made audible; interval -- interval at which spectrogram lines are printed; 

- duration -- terminate command after a specified time. default is indefinite; 

- buckets -- how many values to show in each line of a spectrogram. This value is limited by the number of columns in the terminal. It is useful to reduce this value if using 'audible'; 

- average-samples -- Number of 4us spectral snapshots to take at each frequency, and calculate average and maximum energy over them. (default 10); 

1550 

- classify-samples -- Number of spectral snapshots taken at each frequency and processed by the interference classification algorithm. Generally, more samples give more chance to spot certain types of interference (default 50); 

- range -- 

- 2.4ghz - scan the whole 2.4ghz band; 

5ghz - scan the whole 5ghz band; 

current-channel - scan current channel only (20 or 40 MHz wide); 

range - scan specific range; 

audible=yes -- play each line as it is printed. There is a short silence between the lines. Each line is played from left to right, with higher frequencies corresponding to higher values in the spectrogram.
