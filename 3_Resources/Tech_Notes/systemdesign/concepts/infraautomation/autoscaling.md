
### Purpose
* You can scale up/down to save money on/off peak.
* Automatically react to higher demand

### pitfalls
* When you are moving the monitoring/zookeeper service, ensure puppet agents are turned off before you turn off autoscaler service.
  [Reddit insfrastructure](https://youtu.be/nUcO7n4hek4?t=1629)
* Also not let your auto-scaler terminate a ton of instances at the same time.   