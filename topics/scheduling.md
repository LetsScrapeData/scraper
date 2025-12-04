
# How to Schedule Tasks

### Design Goals
##### Prerequisites
LetsScrapeData is a template-driven, general-purpose web scraping tool, not designed for a specific scenario (e.g., scraping only Google Maps, or a scraper that only supports browser automation). The design considers various common scenarios.

##### Task Scheduling Goals
The main goal of task scheduling is to scrape the required data at the lowest cost, while also considering priority, given specified templates and resources. Therefore, effectively utilizing resources such as proxies, system resources, and capabilities while meeting task execution conditions is crucial for task scheduling.

##### Related Notes
* Different templates achieving the same purpose can have a significant impact on resource consumption (and cost). The development and maintenance costs of these templates are not considered in task scheduling. See [Browser Automation vs API Requests](/scraping/browserVsApi) for more information.
* Maximum concurrency and highest access rate are not the goals of task scheduling, but reasonable concurrency and access rate are necessary.
* If more data needs to be scraped within a certain timeframe, more resources will be required.


### Factors Affecting Task Scheduling
LetsScrapeData App has hundreds of parameters that affect task scheduling, mainly including the following categories:
* Proxy
* DomConfig
* CapConfig
* Template
* Global configs
* System resources
* Other resources

Please contact the administrator if needed.