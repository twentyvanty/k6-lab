# K6 lab results 
## Part 0 
- Step 0.1, http_req_duration: 307.42ms
- Step 0.2, requests 77, rate 3.637 and p(95) 375, and why the rate stays below 5: The request rate stays below 5 requests per second because each virtual user needs to wait for the HTTP request to finish before starting the next iteration. One iteration takes approximately 1.33 seconds on average. Therefore, each virtual user can complete approximately 0.75 iterations per second. Even with 5 virtual users running concurrently, the total request rate is approximately 3.64 requests per second rather than 5. The request rate depends on how long each iteration takes, not just the number of virtual users.
- Step 0.6, exit code of the normal run: 0 and of the run with P95=300: 99 
- Step 0.7, rules that passed, p(95) 422.21, p(99) 462.71, exit code after your change: 0
- Step 0.8, what was wrong, and how the checks showed it: The API did not always follow the customer's requirements. Although all HTTP requests returned status 200, some pizzas still contained pepperoni and required a knife. The no pepperoni check passed only 85% of the time, while the no knife needed check passed only 65% of the time. The checks revealed that the API returned successful HTTP responses but did not consistently satisfy the customer's requirements.
## Part A results 
Step	Test type	Users	Req/s	p(95)	Max	Failed	Checks
A1	Smoke	1	0.489806	387.45 ms	390.51 ms	0%	100%
A2	Average load	3	1.293446	375.26 ms	479.59 ms	0%	100%
A3	Stress	5	2.197296	398.01 ms	531.59 ms	0%	100%
A4	Spike	5	1.052240	380 ms	450.07 ms	0%	100%
A5	Soak	2	0.978694	394.58 ms	553.58 ms	0%	100%
## Part B 
1. Because each virtual user waits for requests to finish and sleeps between iterations before sending more requests.
2. Yes. p(95) increased from 375.26ms to 398.01ms. However, the system remained within its operational envelope because all performance thresholds passed.
3. The exact recovery time must be checked from the A4 dashboard graph. The terminal summary alone does not show it.
4. The overall results show 0% failed requests and p(95) of 394.58ms. The graph is needed to confirm whether performance worsened over time. A soak test can reveal memory leaks.
5. Because p(95) shows the response time experienced by 95% of requests and helps identify slow requests that the average might hide.
6. Network conditions and latency may be different. Server hardware, resources, and workloads may be different
7. It could overload the server, disrupt services, and affect other users. It may also violate laws or terms of service.
8. Vague: The app should load quickly. Testable: With 50 concurrent users, 95% of requests must finish within 800ms, and fewer than 1% may fail.
9. thresholds: {
  http_req_duration: ['p(95)<800'],
  http_req_failed: ['rate<0.01'],
  checks: ['rate>0.99'],
},
