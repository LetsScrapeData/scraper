# How to Handle Exceptions

LetsScrapeData automatically handles common exceptions, but to build a stable scraper, it's necessary to handle various exceptions based on specific scenarios.

For configurable exceptions in the template, see [errname](/reference/errname).

### How to handle common exceptions in actions
Each action has an *errname* attribute, which defines how to handle common exceptions. For example:
* ***action_click***: If the expected clickable element does not appear, it defaults to a template configuration error ("cfginvalid").

* ***action_loopinstr***: If the list of strings to loop through is empty, it defaults to ignoring ("ignore").

* ***action_api***: If the API request is abnormal, it defaults to the task failing and exiting ("normal").

For the default values ​​of the *errname* attribute for each action, see the help documentation for each action.

### How to validate data to meet expectations
It is recommended to validate frequently changing websites and key data items to promptly identify exceptions and improve the template.

Data validation can be performed by configuring the following properties:
* *pattern*: Parameters for constructing the regular expression, new [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)(pattern, flags)

* *flags*: Defaults to "", "i" indicates case-insensitive matching.

* *valerrname*: Defaults to "ignore", indicating no data validation.

The default configuration of the above properties does not perform data validation. The following can be modified to perform the desired data validation:
* ***column_xxx***: Validates the validity of the extracted record field data.
* ***action_api***: Validates the validity of the API response data.
* ***action_setvar_xxx***: Validates the validity of different retrieved data.

### How to handle different status codes of API response
Refer to [How to Scrape Data Using API](/topics/api) for details.

### How to handle Specific exceptions
The template should determine potential exceptions based on the specific scenario and trigger errors using ***action_exit***. For example:
* If there's a high probability that the user is entering invalid parameters, it's recommended to check the validity of the input parameters. If invalid, trigger a "parasinvalid" error. When designing templates, validity should be checked first when submitting input parameters; see [How to design GUI for parameters](/topics/para).
* In manual login templates, it should be determined whether the user has successfully logged in within the specified time; otherwise, an error should be triggered, treating it as a login failure.