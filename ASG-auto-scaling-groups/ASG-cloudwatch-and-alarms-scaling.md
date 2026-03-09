# Auto Scaling - CloudWatch Alarms and Scaling

-Its possible to scale an ASG based on CloudWatch Alarms
-An alarm monitors a metric (such as Average CPU or custom metrics)
-Metrics such as Average CPU are computed for the overall EC2 instances
-Based on the alarm:
      * We can create scale-out policies (increase the number of instances)
      * We can create scale-in policies (decrease the number of instances)
