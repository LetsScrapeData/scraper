
# How to Monitor Web Scraping

### Design goals

##### Background
Due to changes in business and technology, especially anti-bot policies, web scrapers are more prone to exceptions than other types of software tools, making monitoring even more crucial.

##### Monitoring goals
To promptly detect exceptions and assist in their rapid resolution, thereby reducing development and operational maintenance costs.

### Timely exception detection
Timely exception detection is crucial for reducing invalid scraping operations and minimizing network or capability bans. Only by promptly detecting exceptions can they be quickly resolved, enabling rapid completion of the desired data scraping, improving service availability, and enhancing user trust.

LetsScrapeData automatically handles common exceptions, and templates must also be able to [fully handle various exceptions](/topics/exception). LetsScrapeData can then promptly detect and log exceptions.

### Assisting in exception resolution
Usually, once an exception is discovered, the problem can be quickly located and resolved. Sometimes, detailed exception information, i.e., exception logs, is needed to help template designers quickly pinpoint the issue.

### Handling exceptions
Exception handling falls into three main categories:
* Treating task completion as abnormal: such as invalid parameters.
* Invalid template: Automatically stop the execution of the task and other tasks  of the template. Continue executing the tasks of the corrected template.
* Other exceptions: such as proxy failure or expired login. Automatic actions will be taken (e.g., switching proxies or re-login) before retrying.

Once an exception is detected, everything except for template correction is handled automatically by task scheduling. This significantly reduces operational costs and improves user satisfaction.

