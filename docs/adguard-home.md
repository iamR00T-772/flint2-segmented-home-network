# AdGuard Home & Content Filtering

AdGuard Home provides DNS/content filtering at the router level.

The final approach I used favors useful general ad/tracker blocking plus security-oriented filtering rather than maximizing list size.

Testing showed that aggressive lists increased the router's workload and complicated troubleshooting. A smart-TV connectivity problem initially appeared to be related to DNS filtering behavior but ended up ultimately being a Wi-Fi authentication compatibility issue, due to the chosen encryption type.

The broader lesson was to balance filtering coverage against false positives, compatibility, and overall resource cost, since the router in this setup is responsible for administering many other services at the same time.
