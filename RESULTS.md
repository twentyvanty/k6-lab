### Step 0.2: More users for longer
**Results:**
- Total requests: 77
- Request rate: 3.637 requests/second
- Average HTTP response time: 290.95 ms
- p(95): 375 ms
- Average iteration duration: 1.33 seconds

**Explanation:**

The request rate stays below 5 requests per second because each virtual user needs to wait for the HTTP request to finish before starting the next iteration. One iteration takes approximately 1.33 seconds on average.

Therefore, each virtual user can complete approximately 0.75 iterations per second. Even with 5 virtual users running concurrently, the total request rate is approximately 3.64 requests per second rather than 5.

The request rate depends on how long each iteration takes, not just the number of virtual users.