**Note:** For the screenshots, you can store all of your answer images in the `answer-img` directory.

## Verify the monitoring installation

*TODO:* run `kubectl` command to show the running pods and services for all components. Take a screenshot of the output and include it here to verify the installation

#### Pods in all Namespaces

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/pods_all_ns.png">

#### Services in all Namespaces

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/svc_all_ns.png">

#### Pods and Services in Monitoring and Observability Namespaces

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/pods_svc_monitoring_and_observability_ns.png">

## Setup the Jaeger and Prometheus source
*TODO:* Expose Grafana to the internet and then setup Prometheus as a data source. Provide a screenshot of the home page after logging into Grafana.

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/grafana.png">

## Create a Basic Dashboard
*TODO:* Create a dashboard in Grafana that shows Prometheus as a source. Take a screenshot and include it here.

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/basic_dashboard.png">

## Describe SLO/SLI
*TODO:* Describe, in your own words, what the SLIs are, based on an SLO of *monthly uptime* and *request response time*.

SLIs or Service Level Indicators are measurable indicators of how the application/website/service is faring compared to the promise of the organization to its customers and stakeholders. This promise is also known as SLOs or Service Level Objectives. 

An example SLI for a monthly uptime is the rate of the 20x or 30x (valid requests) responses of the website in a total incoming requests per month. For example, the average 20x or 30x responses of the web application for the month of October 2022 is 97.99%.

On the other hand, the SLI for a request response time is how long the request took to be served in actuality. For example, it took an average of 700ms for incoming requests to be served in the month of October 2022.

## Creating SLI metrics.
*TODO:* It is important to know why we want to measure certain metrics for our customer. Describe in detail 5 metrics to measure these SLIs. 

1. The average 20x or 30x responses of the web application for the month of October 2022 is 97.99%.
2. It took an average of 700ms for incoming requests to be served for the month of October 2022.
3. 1.5% of the total incoming requests had 50x responses for the month of October 2022.
4. The average CPU usage of the web application for the month of October 2022 is 83.67%.
5. The login requests in the web application for the month of October 2022 took an average of 2 seconds to be served.

## Create a Dashboard to measure our SLIs
*TODO:* Create a dashboard to measure the uptime of the frontend and backend services We will also want to measure to measure 40x and 50x errors. Create a dashboard that show these values over a 24 hour period and take a screenshot.

<!-- PromQL Commands:

1. [Uptime] Average 20x/30x: 
   1. To get count: prometheus_http_requests_total{code=~"2.*"}  and prometheus_http_requests_total{code=~"3.*"} 
   2. To get the average: sum(prometheus_http_requests_total{code=~"2.*"})/sum(prometheus_http_requests_total)
   3. Second metric: sum(prometheus_http_requests_total{code=~"3.*"})/sum(prometheus_http_requests_total)
2. [Response Time] Average incoming requests response: 
   1. sum(rate(prometheus_http_request_duration_seconds_sum[5m])) / sum(rate(prometheus_http_request_duration_seconds_count[5m]))
   2. sum(prometheus_http_request_duration_seconds_sum) / sum(prometheus_http_request_duration_seconds_count)
   3. sum(prometheus_http_request_duration_seconds_count) / sum(prometheus_http_request_duration_seconds_sum)
3. [50x Errors] Average 50x:  sum(prometheus_http_requests_total{code=~"5.*"})/sum(prometheus_http_requests_total)
4. [40x Errors] Average 40x: sum(prometheus_http_requests_total{code=~"4.*"})/sum(prometheus_http_requests_total)
5. CPU usage: rate(process_cpu_seconds_total[5m])
    -->

#### Prometheus SLI Dashboard

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/dashboard_prometheus_sli.png">

## Tracing our Flask App
*TODO:*  We will create a Jaeger span to measure the processes on the backend. Once you fill in the span, provide a screenshot of it here. Also provide a (screenshot) sample Python file containing a trace and span code used to perform Jaeger traces on the backend service.

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/span_in_Flask_app_1.png">


<img src="https://github.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/blob/main/answer-img/backend_in_jaeger.png?raw=true">

## Jaeger in Dashboards
*TODO:* Now that the trace is running, let's add the metric to our current Grafana dashboard. Once this is completed, provide a screenshot of it here.

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/backend_in_grafana.png">

## Report Error
*TODO:* Using the template below, write a trouble ticket for the developers, to explain the errors that you are seeing (400, 500, latency) and to let them know the file that is causing the issue also include a screenshot of the tracer span to demonstrate how we can user a tracer to locate errors easily.

TROUBLE TICKET

Name: Juan dela Cruz

Date: November 6, 2022

Subject: Backend service's star endpoint shows "Method Not Allowed" error 405.

Affected Area: star endpoint

Severity: High

Description: The Mongo database connection cannot be found. The tracer span is 2f33c63.


## Creating SLIs and SLOs
*TODO:* We want to create an SLO guaranteeing that our application has a 99.95% uptime per month. Name four SLIs that you would use to measure the success of this SLO.

**SLOs:**

1. 99.95% of uptime per month
2. .03% of 40x/50x responses per month.
3. Application responses should be served within 1500 ms per month.
4. Monthly average CPU usage should be 60% or less.
5. Monthly average memory usage should not exceed 600Mib.

**SLIs:**

1. The average 20x or 30x responses of the web application for the month of October 2022 is 97.99%.
2. 1.5% of the total incoming requests had 50x responses for the month of October 2022.
3. It took an average of 1070 ms for incoming requests to be served for the month of October 2022.
4. The average CPU usage of the application is 42.65% for the month of October 2022.
5. The average memory usage of the application is 300Mib for the month of October 2022.

## Building KPIs for our plan
*TODO*: Now that we have our SLIs and SLOs, create a list of 2-3 KPIs to accurately measure these metrics as well as a description of why those KPIs were chosen. We will make a dashboard for this, but first write them down here.

1. The average 20x or 30x responses of the web application for the month of October 2022 is 97.99%.
   - Monthly uptime - this KPI indicates the total usability of the application.
   - 20x code responses per month - this KPI indicates availability of the pages of the application.
   - Monthly traffic - this KPI will indicate the number of requests served by the application.
2. 1.5% of the total incoming requests had 50x responses for the month of October 2022.
   - Monthly downtime - this KPI indicates the number of times the application was down
   - Errors per month - this KPI will indicate the monthly errors encountered in the application.
   - Monthly traffic - this KPI will indicate the number of requests served by the application.
3. It took an average of 1070 ms for incoming requests to be served for the month of October 2022.
   - Average monthly latency - this KPI will indicate the time it took for the application to respond to requests.
   - Monthly uptime - this KPI indicates the total usability of the application.
   - Monthly traffic - this KPI will indicate the number of requests served by the application.
4. The average CPU usage of the application is 42.65% for the month of October 2022.
   - Average monthly CPU usage of pod used by the application - this KPI will indicate how much CPU is used by the source pod of the application.
   - Average monthly CPU usage of all the pods - this KPI will indicate how much CPU is used by all the pods required to run the application.
   - Monthly quota limit - this KPI will indicate whether the application is exceeding its usage of the CPU quota.
5. The average memory usage of the application is 300Mib for the month of October 2022.
   - Average monthly memory usage of pod used by the application - this KPI will indicate how much memory is used by the source pod of the application.
   - Average monthly memory usage of all the pods - this KPI will indicate how much memory is used by all the pods required to run the application.
   - Monthly quota limit - this KPI will indicate whether the application is exceeding its usage of the memory quota.

## Final Dashboard
*TODO*: Create a Dashboard containing graphs that capture all the metrics of your KPIs and adequately representing your SLIs and SLOs. Include a screenshot of the dashboard here, and write a text description of what graphs are represented in the dashboard.  

<img src="https://raw.githubusercontent.com/tuandungbrse/Project_Starter_Files-Building_a_Metrics_Dashboard/main/answer-img/final_dashboard.png">

1. Uptime panel - this represents the 20x/30x (successful) responses of the application.
2. 50x and 40x Errors panel - these represents the 40x/50x (error) responses of the application.
3. Average Response Time panel - this represents the average response time of the application per request.
4. CPU Usage panel - this represents the CPU usage of the backend application. This also provides an option to select a few pods for comparison and consolidate the total CPU usage of all the pods per namespace.
5. Memory Usage panel - this represents the memory usage of the backend application. This also provides an option to select a few pods for comparison and consolidate the total memory usage of all the pods per namespace.