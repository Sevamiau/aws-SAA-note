# EC2 Spot instance requests

-Can get a discount of up to 90% compared to on-demand
-Define mas spot price and get the instance while current spot price < max
    .The hourly spot price varies based on offer and capacity
    .if the current spot price > tour mas price you can choose to stop or terminate tour instance with a 2 minutes grace period

-Other strategy: Spot Block:
    .'block' spot instance during a specified time frame (1 to 6 hours) without interruptions
    . in rare situations the instance may be reclaimed

You can only cancel spot instances requests that are open, active or disabled.
Cancelling a spot request does no terminate instances
You must first cancel a Spot request and then terminate the associated spot instances
