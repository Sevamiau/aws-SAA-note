# Auto Scaling Groups - Scaling Cooldowns

----------

* After a scaling activity happens, you are in the **cooldown period** (default 300seconds)
* During the cooldown period the ASG will not launch or terminate additional instances (to allow for metrics to stabilize)

- Advice: use a pre-baked AMI so instances launch and become healthy faster, which lets you shorten the cooldown period and react to load changes more quickly

## Exam trap

- If a question says instances are launching and terminating too rapidly ("thrashing") → the cooldown period is too short
- Default cooldown is 300 seconds — you can reduce it if your AMI starts up fast

----------

