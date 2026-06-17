# How to Check Completed Tasks

It is common to encounter anomalies during data scraping, resulting in a failure to collect the intended data. It is crucial to determine the validity of the collected data and, depending on the situation, decide whether to re-collect or re-extract it.

### Introduction to check template

A normal template has an optional associated template—known as a check template—which can be specified using the _checkTemplateId_ attribute. This template is used to:

- Verify the accuracy of data collected from completed tasks
- Determine whether data needs to be re-collected
- Re-extract data
- Generate sub-tasks that need to be added

### Prerequisites for check template

To effectively verify whether completed tasks have collected the correct data—or to re-extract data—relevant information (such as API responses) must be saved (these are compressed prior to storage). Designers of normal templates need to weigh which original data (_origData_) requires preservation.

For client-side rendered web pages, even when using browser automation for data collection, API responses are generally much smaller in volume than the fully rendered HTML; therefore, if original data needs to be saved, it is recommended to prioritize extracting it from the intercepted API responses.

You can promptly delete unnecessary schedules (and their associated tasks) and adjust data retention periods to remove unwanted data and free up disk space.

### When to add check template

Normal templates are used for data scraping—including re-scraping—and typically require network access; some may also require a login. Check templates are used to check data collected by completed tasks and do not access the network. It is generally recommended to add a check template when a normal template fails to scrape the correct data, particularly when the normal template is widely used by many people.

The _templateCat_ attribute of the check template must be 42, and the _domainId_ attribute must be the same as that of the corresponding normal template.

### Input of check template

- datatables of completed task
- paras of completed task: origParas, similiar to inParas
- para1: reextract, whether to re-extract, default "1" (true)
- optional paras as needed

### Output of check template

- The variable _checkResult_ stores the check result; valid check results are as follows:
  - ok: Both origData and extractedData are correct.
  - incorrectOrigData: origData is incorrect; re-collect is required.
  - incorrectExtractedData: origData is correct, but extractedData is incorrect and was not re-extracted (reextract is "0").
  - newExtractedData: origData is correct, but extractedData was incorrect and has been re-extracted (reextract is "1"); the re-extracted data is stored in datatables and subtasks.
- datatables: valid only when checkResult is newExtractedData
- subtasks: valid only when checkResult is newExtractedData

### How to execute check template

First, select the schedule and the corresponding template in the web interface, then choose the "Execute Check Template" menu item from the top-right corner to trigger a check on the completed tasks.

If the _checkResult_ is "incorrectOrigData", delete the completed task and its associated data, then add a new task to re-collect the data.

If the _checkResult_ is "newExtractedData", replace the previously extracted data; if there are subtasks, add new subtasks (generally, there is no need to worry about re-collecting data, as the previously collected correct data will be automatically shared).
