# ASG Scaling Policies

## Quick decision table

| Policy | How it works | Pick this when |
|---|---|---|
| Target Tracking | Keeps a metric at a target value | Default choice — simplest to configure |
| Step Scaling | Adds/removes N instances when alarm crosses a threshold | Need different responses at different severity levels |
| Simple Scaling | Single fixed response to one alarm | Legacy — prefer Step Scaling |
| Scheduled Scaling | Changes capacity at a fixed time | Traffic pattern is predictable (e.g. business hours) |
| Predictive Scaling | Uses ML to forecast and scale ahead | Traffic has recurring patterns, want to scale before the spike |

---

## Target Tracking Scaling

- You define a target metric value and AWS manages the rest
- Example: keep average CPU at 40%
- Simplest to set up — recommended as the default

## Step Scaling

- Triggered by a CloudWatch alarm crossing a threshold
- Different step sizes for different levels of breach
- Example:
  - CPU > 70% → add 2 instances
  - CPU > 90% → add 5 instances
  - CPU < 30% → remove 1 instance

## Scheduled Scaling

- Scales at a specific time, independent of metrics
- Example: increase min capacity to 10 at 5 PM on Fridays
- Use when you know traffic will spike at a predictable time

## Predictive Scaling

- Analyzes historical load and forecasts future demand
- Schedules scaling actions in advance
- Good for recurring patterns (daily/weekly cycles)

---

## Exam trap

- "Automatically adjust to maintain performance" → Target Tracking
- "Scale before a known event (Black Friday, weekly spike)" → Scheduled or Predictive
- "React differently based on how severe the CPU spike is" → Step Scaling
