# Overview

### Introduction
LetsScrapeData helps you to start web scraping quickly without coding. Main features are listed below:
* Mutual help
Users can help each other to scrape data, solve the excessive restrictions on web access, speed up data scraping, and reduce the number of web page visits.
* Free
LetsScrapeData is free to use, and there is no limit on the number of deployments or concurrency. Most scraping templates are also free. (Proxy/captcha/OCR are charged if used, but the price is cheaper than buying it yourself from third parties. If there is no template you need, please contact us.)
* Zero-code or No-code
LetsScrapeData uses templates to scrape data, and you can start collecting data immediately without writing code.

### Quick start for user
As a user, if you want to start scraping data immediately, please refer to [Quick Start - User Guide](/manual/README).

### Main terms
LetsScrapeData app scrapes data by executing the actions defined in the template using specified parameters. LetsScrapeData uses the following main terms:
* Template: The template defines actions to be executed to scrape the desired data and the relevant description of the template (template name, relevant parameters, description of what data to scrape), and is uniquely identified by an integer named <b style="color: blue">tid</b>.
* Parameters: Independent variables that control how actions defined in the template are performed, and a template can contain 0, 1, or more parameters.  For example, a template that scrapes the details of a product on an e-commerce platform will have a parameter: product number.
* Task: A unit of execution that is implemented by performing actions defined in the template using specified parameters. There are two types of tasks: unfinished and completed, completed means completed successfully, and unfinished refers to not yet completed successfully, including failed.
* Subtask: A complex task can be split into multiple subtasks, for example, the task of scraping the first 100 pages of notebook lists on an e-commerce platform can be split into 100 subtasks that scrape only one page.
* Timing: The time when the new task is triggered, which is also the desired time to scrape data. There are two types of timing:
  * Once: Trigger a new task at a time now or at some time in the future.
  * Regularly: Trigger a new task at regular intervals, such as one o'clock in the morning every day, and you can specify the end time or number of triggers.
* Schedule: Schedule creates a task of a template with specified parameters based on the timing configuration. You can restart the timing after modifying the timing configuration or parameters.
* Data table: The table that holds the scraped data, uniquely identified by a string <b style="color: blue">tabname </b>starting with "dat_". A template may involve 0, 1 or more data tables.
* User: People who use LetsScrapeData app to scrape data. In most cases, you are just a user.
* Designer: People who design templates using extensions like LetsScrapeData.

### Main supported web scraping techniques
* Rate limits: automatic flow control for massive data scraping, such as interval / concurrent /times per period
* Monitoring: such as succeeded / failed / tried / to do
* IP rotation: by using proxy or mutual help
* CAPTCHAs solving: such as recaptcha, hcapthca, image or text captcha 
* Login wall: automatically or manually
* Decode encrypted information: such as data encrypted using SVG/WOFF
* Information in the picture
* Intercept API requests
* Multiple data interfaces: API / database / file, etc
* Browser operations: goto or open / click / input / hover / select / scroll
* Automatic file saving: such as screenshot, pdf, mhtml, download directly or by clicking
* Automatically detect pop-up web pages
* Request headers: such as user agent
* Adapt quickly to web changes
* Data cleaning: more than 50 data cleaning functions
* Data export
* Data synchronization

### Quick start for designer
As a designer, you can quickly start designing the template you need. Please refer to [Quick Start - Template Design](/template/README).

<!-- introduction to LetsScrapeData: https://youtu.be/gt25G8Lzt3E -->