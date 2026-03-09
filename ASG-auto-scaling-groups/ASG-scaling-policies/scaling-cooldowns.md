# Auto Scaling Groups - Scaling Cooldowns

----------

* After a scaling activity happens, you are in the **cooldown period** (default 300seconds)
* During the cooldown period the ASG will not launch or terminate additional instances (to allow for metrics to stabilize)

* Advice: Use a ready-to-use AMI to reduce config time in order to be serving request fasters and reduce the cooldown perdiod

----------

