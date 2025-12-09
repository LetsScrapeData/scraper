# Security

### State data
Some websites require [login](/topics/login) before accessing related pages. The capabilities used for automatic login and the state data obtained after login contain sensitive information and cannot be accessed arbitrarily.

##### Capability
Automatic login information (such as username and password) is encrypted and stored locally, and can only be used locally.
> **Warning**: Do not add any capabilites (credentials) involving money! Furthermore, related accounts may be banned! You should be fully aware of the potential risks when adding capabilites; LetsScrapeData assumes no responsibility for any possible consequences.

##### Sensitive state data
The cookies, localStorage, and HTTP headers in the state data may contain sensitive information. This information can only be used to access web pages or APIs and should not be viewed by users. Sensitive information obtained from the template must be stored in a special variable called [secureData](/topics/variable) to prevent users from seeing it.

### File Directory
The template can read local files (such as text files containing a large number of product IDs) and write content such as web page images to local files. For security reasons, these files must be located in a specific directory or its subdirectories.

If you need to change this directory, please refer to the relevant configuration instructions.

### Security suggestions
Security is very important. If you have any other suggestions, please let us know.
