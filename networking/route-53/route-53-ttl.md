# Route 53 - Records TTL (time to live)

- Hight TTL - e.g: 24 hr 
  * Less traffic on route 53 
  * Possibly outdated Records

- Low TTL - e.g: 60 sec.
  * More traffic on route 53 (more $$)
  * Records are outdated for less time
  * Easy to change records 

- Except for Alias Records, TTL is mandatory for each DNS record   
