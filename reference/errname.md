# Configurable Errnames

LetsScrapeData automatically handles common exceptions and the following errnames can be configured in the template:

* **normal**: Execution terminates normally and the task is considered completed.
* **parasinvalid**: Invalid task parameter(parasstr) and the task is considered completed.
* **capinvalid**: Invalid automatic capability, such as wrong password or apiKey.
* **caplocked**: Capability is temporarily locked and will be automatically unlocked later
* **capexpired**: The state data of the logged-in capability has expired. If the capability is manually logged in, please log in again.
* **proxylocked**: The proxy(IP) is temporarily blocked from accessing this domain.
* **proxyforbidden**: The proxy(IP) is permanently banned from accessing this domain.
* **cfginvalid**: The template is invalid and needs to be updated before it can be executed again.
* **captchafailed**: Unable to solve the captcha normally.
* **ignore**: The error is ignored and execution continues.
* **other**: Other error.
