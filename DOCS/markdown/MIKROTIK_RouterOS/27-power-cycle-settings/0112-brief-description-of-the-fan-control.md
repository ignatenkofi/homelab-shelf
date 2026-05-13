## Brief description of the fan-control 

If at least one of the internal measured (CPU, SFP, Switch, Board etc.) temperatures exceed fan-target-temp , the fans will start to spin. The higher the temperature, the faster the fans will spin. For devices with PWM fans, as the internal measured temperatures exceed fan-target-temp , the fans will linearly increase their RPM to try to keep the temperature at fan-target-temp if possible and will get to their Max RPM when the temperature is equal or exceeds fan -full-speed-temp .  For devices with DC fans, as the internal measured temperatures exceed fan-target-temp , the fans will start spinning but at a higher minimum RPM by default. This may result in cooling the device to the point where the fans turn-off completely if fan-min-speed-percent is set to 0% , while with the default value of 12% fans will never go to a full stop therefore reducing the noise and On/Off peaks that may occur. The temperature then may slowly increase to fan-target-temp and the fans will turn on again. Currently, there is one exception. The S+RJ10 modules have a temperature threshold of 65C before they trigger the fans. Since it's a higher temperature threshold, the fans will start spinning at a higher initial speed to cool the device. All the above mentioned functionality is directly related to the fan-control-interval parameter value as it will determine how often FAN controller monitors all sensor data and triggers changes in fan-control. 

**==> picture [13 x 13] intentionally omitted <==**

PWM and DC fans react to fan-control differently. While PWM fans will increase/decrease their RPM in a linear way the DC fans have only few possible speed ratings at which they may operate. 

All readings are approximate and may not be 100% precise. Their purpose is to ~inform users about possible/upcoming failures. 

1767
