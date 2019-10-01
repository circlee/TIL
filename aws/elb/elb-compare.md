
[AWS] AWS ALB vs NLB vs CLB

| <div style="width:200px">Feature</div> | <div style="width:200px">Application Load<br>Balancer</div> | <div style="width:200px">Network Load<br>Balancer</div> | <div style="width:200px">Classic Load <br>Balancer</div> |
| - | :- | :- | :- |
| Protocols | HTTP, HTTPS | TCP | TCP, SSL, HTTP, HTTPS |
| Platforms | VPC | VPC | EC2-Classic, VPC |
| Health checks	 | ✔ | ✔ | ✔ |
| CloudWatch metrics | ✔ | ✔ | ✔ |
| Logging | ✔ | ✔ | ✔ |
| Zonal fail-over | ✔ | ✔ | ✔ |
| Connection draining<br>(deregistration delay) | ✔ | ✔ | ✔ |
| Load Balancing to multiple ports on the same instance	 | ✔ | ✔ |  |
| WebSockets	 | ✔ | ✔ |  |
| IP addresses as targets | ✔ | ✔ |  |
| Load balancer deletion protection	 | ✔ | ✔ |  |
| Path-Based Routing | ✔ |  |  |
| Host-Based Routing | ✔ |  |  |
| Native HTTP/2	 | ✔ |  |  |
| Configurable idle connection timeout | ✔ | ✔ |  |
| Cross-zone load balancing	 | ✔ | ✔ | ✔ |
| SSL offloading | ✔ |  | ✔ |
| Server Name Indication (SNI) | ✔ |  |  |
| Sticky sessions | ✔ |  | ✔ |
| Back-end server encryption | ✔ |  | ✔ |
| Static IP	 |  | ✔ |  |
| Elastic IP address |  | ✔ |  |
| Preserve Source IP address |  | ✔ |  |
| Price (Asia Seoul)<br>checkedAt : 2019-10-01 | 시간당 0.0225 USD<br>LCU-시간당 0.008 USD | 시간당 0.0225 USD<br>LCU-시간당 0.006 USD | 시간당 0.025 USD<br>LCU-시간당 0.008 USD |



