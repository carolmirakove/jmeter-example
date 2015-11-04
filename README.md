# About

This `jmeter-example` repository contains an example JMeter project to demonstrate the relationship between Thread Groups > HTTP Requests > Response Assertions, data-driving scripts, and reporting and monitoring controllers. This is not a runnable project, it is for reference only.

## Modeling Tests
### Thread Groups
The page views and transactions in your JMeter thread groups should reflect the traffic patterns of your existing and aspirational production environment. I like to model my thread groups using the following approach:
* Determine the percentages of your transactions, e.g., 50% Home Page, 40% Detail Page, 10% Checkout.
* Determine the number of transactions in real-world sessions, e.g., 30% 1 transaction, 40% 2 transactions, 30% 3 transactions
* Design thread groups that reflect both your transactions per session and overall transaction weights, e.g.,
  * User 1: 30% of threads: Home Page
  * User 2: 20% of transactions: Home Page, Detail Page
  * User 3: 20% of transactions: Detail Page, Detail Page
  * User 4: 30% of threads: Home Page, Detail Page, Checkout
  
### Test Load Types
Typically we are interested in three categories of load: average-day traffic, historical peak traffic, and aspirational peak traffic. I find it useful to use average-day load in my initial runs to validate the system under test and the load models, then ramp up to historical peak loads, followed by aspirational loads. Troubleshooting bottlenecks is most manageable under the minimum load that reveals them. 

Key metrics for load models include page views per second and per hour, sessions per hour, session duration, sessions per hour per virtual user, and ramp up time.

As with any model, no matter how sound your math, thread groups may not generate your intended Load Targets either because of error or because of a system variable you didn't account for. If the page hits are lower or higher than intended, then the number of virtual users or think time should be adjusted.

## Developing Tests
The [Apache JMeter user manual](https://jmeter.apache.org/usermanual/) is of course the canonical reference for developing a JMeter project.

The example project in this repository demonstrates the elements I have found most useful, e.g., Simple Controllers, Gaussian Random Timers, config defaults, CSV Data Sets. 

When developing and debugging thread groups, I find the View Results Tree Listener to be valuable for its granular request and response data, but it should be disabled or removed when running a load test as it can create excess overhead for the test agent.

## Running Tests
You can use the Start icon in the toolbar to run and debug, but for bigger test runs you probably want to run tests from the command line to minimize test-runner overhead, and in fact you will need to do this if you are using multiple test agents and aggregating results.

## Monitoring Tests
Work with your engineering team and product owners to determine performance acceptance criteria, and then assign owners to monitor each metric under load. In addition to client page-load and transaction times, you should also monitor server-side metrics such as CPU, memory, disk I/O, network I/O, and errors in the server logs.

Wishing you all the uptime!
