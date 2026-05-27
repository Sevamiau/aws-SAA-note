# Amazon CloudFront Cache Invalidations

- In case you updated the back-end origin, CloudFront doesn't know about it and will only get the refreshed content after the TTL has expired
- However you can force an entire or partial cache refresh (thus bypassing the TTL) by performing a CloudFront Invalidations
- You can invalidate all files (*) or a special path (/images/*)


