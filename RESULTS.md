# K6 lab results 
## Part 0 
- Step 0.1, http_req_duration: 307.42ms
- Step 0.2, requests 77, rate 3.637 and p(95) 375, and why the rate stays below 5: The request rate stays below 5 requests per second because each virtual user needs to wait for the HTTP request to finish before starting the next iteration. One iteration takes approximately 1.33 seconds on average. Therefore, each virtual user can complete approximately 0.75 iterations per second. Even with 5 virtual users running concurrently, the total request rate is approximately 3.64 requests per second rather than 5. The request rate depends on how long each iteration takes, not just the number of virtual users.
- Step 0.6, exit code of the normal run: 0 and of the run with P95=300: 99 
- Step 0.7, rules that passed, p(95) 422.21, p(99) 462.71, exit code after your change: 0
- Step 0.8, what was wrong, and how the checks showed it: The API did not always follow the customer's requirements. Although all HTTP requests returned status 200, some pizzas still contained pepperoni and required a knife. The no pepperoni check passed only 85% of the time, while the no knife needed check passed only 65% of the time. The checks revealed that the API returned successful HTTP responses but did not consistently satisfy the customer's requirements.
## Part A results 
| Step | Test type | Users | Req/s | p(95) | Max | Failed | Checks | | ---- | ------------ | ----- | ----- | ----- | --- | ------ | ------ | | A1 | Smoke | 1 | | | | | | | A2 | Average load | 3 | | | | | | | A3 | Stress | 5 | | | | | | | A4 | Spike | 5 | | | | | | | A5 | Soak | 2 | | | | | | 
## Part B 
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9.
