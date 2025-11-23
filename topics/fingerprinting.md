
# Fingerprinting
[Fingerprinting](https://developer.mozilla.org/en-US/docs/Glossary/Fingerprinting) is a practice in which websites identify a particular browser by collecting and combining distinguishing features of the browser and underlying operating system. Elements of a fingerprint might include, for example:
* the browser version
* the timezone and preferred language
* the set of video or audio codecs that are available on the system
* the fonts installed on the system
* the state of the browser's settings
* the computer's display size and resolution

Whether retrieving data through a browser or an API request, you should try to mimic the real user environment, including the browser and proxy.

### Browser
Most common browsers now automatically update by default, so you can use them directly. However, it's recommended to prioritize browser controllers like Patchright and Camoufox to minimize the chance of being detected.

### API
LetsScrapeData supports multiple API contexts. It is recommended to use the default API context first. It will automatically generate fingerprints that simulate real users and will update to use the most appropriate tools as needed.
It also provides flexible control over the HTTP headers of [API](/topics/api) requests.