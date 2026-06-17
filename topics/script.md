# How to Use Scripts

While LetsScrapeData templates support hundreds of predefined functions and string templates for most data processing and calculation tasks, relying solely on these can make templates overly complex when calculations are intricate; in such cases, scripts may be used. Currently, only JavaScript is supported.

> Note:
>
> - Although scripting is supported, we recommend prioritizing predefined functions for reasons such as performance and maintainability (e.g., stricter security restrictions may be applied to scripts); use custom scripts only when necessary.
> - **js-isolated** scripts are relatively secure; **js-vm2** scripts are subject to limitations but still pose potential security risks. We reserve the right to impose stricter restrictions at any time as needed.
> - We recommend using **js-isolated** scripts whenever possible; future support for "extract" and "fun" scenarios may be limited exclusively to this type.
> - Scripts posing potential security risks may be subject to future measures such as mandatory review, security warnings to users, or restricted access (e.g., available only to designers with high trust ratings).
> - Any script found to be potentially malicious will be permanently banned.

### Security Considerations

For security reasons:

- All input data for scripts is serialized into strings before being passed in, and subsequently converted into the appropriate objects based on the specific scenario.
- All output data from scripts is passed out solely as strings, and subsequently converted into the appropriate objects based on the specific scenario.
- Restrictions are imposed on the resources, external packages, and functions available for use, depending on the script type.

### Script Types

The script type determines the functionality available to the script. LetsScrapeData supports the following types of custom JavaScript scripts:

- **js-isolated** scripts: These scripts can only use features supported by native JavaScript (e.g., crypto and Buffer are unavailable) and can only read data passed in from an external source.
- **js-vm2** scripts: These scripts can use features supported by native JavaScript as well as the specific packages and functions listed below; they can only read data passed in from an external source.
  - crypto
  - Buffer
  - URL
  - URLSearchParams
  - Other functions deemed safe for use as needed
  <!-- - cheerio -->

### Script Use Scenarios

The usage scenario determines the script's purpose and its input/output data. LetsScrapeData templates support the execution of custom JavaScript scripts in the following scenarios:

- **api**: Used to calculate complex request headers and request data (such as encrypted signature parameters) for API requests; the script is specified via the _scriptname_ attribute of **action_api**.
- **extract**: Used to extract required data from original data; the script is specified via the _scriptname_ attribute of **action_extract_script**.
- **fun**: Used to extract required data from original data; the script is specified via the _scriptname_ attribute of **action_extract_script**.

In all the above scenarios, scripts can access input data via the global variable _inData_ (please refer to the subsequent section for specific definitions).

In addition to the scenarios above, JavaScript scripts can also be used within **action_setvar_get.get_evaluate**. However, for security reasons, they cannot access cookies or localStorage. Usage restrictions may become stricter in the future for security purposes; therefore, it is recommended to avoid using **get_evaluate** whenever possible.

### Script Configuration

1. Use the _scriptname_ attribute to specify the name of the referenced script based on the usage scenario.
2. Configure each script using **scripts.script** as needed:

- _name_: The script name; must match the _scriptname_ defined above.
- The script content is stored in a separate file located in the "scripts" subdirectory of the template's directory. The filename must be _scriptname_ with a ".js" extension. The content is automatically read when saving or debugging the template.
- _scenario_: The usage scenario. Valid values ​​are "api", "extract", and "fun". Input and output data differ by scenario; see the detailed explanations below.
- _solution_: The script type. Valid values ​​are "js-isolated" and "js-vm2".
- _externals_: External dependencies such as "cookies", "localStorage", or "pageEvaluate" (separated by commas). Valid only when _scenario_ is "api" and _solution_ is "js-vm2".
- "cookies" and "localStorage" refer to data within the state object; see [When Login Is Required](/topics/login).

### General Script File Specifications

All script types must adhere to the following specifications:

- Part 1: Script description and mock input (optional). May include:
  - Version info: If required, must be on the first line (e.g., "// version: 1.0.0").
  - Other descriptions: Must be formatted as comments.
  - Mock input: e.g., _inData_, used for standalone script debugging. During normal execution (non-debugging), relevant content is passed in automatically; see the detailed scenario explanations below.
  - Part 1 separator line: If this section exists, it must include a line starting with "// start of script:", indicating that the actual script content begins on the next line.
- Part 2: Actual script content (may include comments). Only this part is saved by the template.
  - For **js-isolated** scripts, the final line must be a string, a variable holding a string, or a function returning a string; do not use the "return" keyword. Please refer to [isolated-vm](https://www.npmjs.com/package/isolated-vm) for details.
  - **js-vm2** type scripts require assigning a function to "module.exports"; this function takes no input parameters and returns a string. Please refer to [vm2](https://www.npmjs.com/package/vm2) for details.
- Part 3: Debugging/Logging section (optional)
  - Section separator line: If this section is included, this specific line is mandatory; it must begin with "// end of script:" to indicate that the content following this line belongs to Part 3.
  - Other content: Typically used to print the script's execution output for debugging purposes.

### Input and Output Data for api Scenario Scripts

##### Script Input Data

The script can access the global variable _inData_ (type: _ApiScriptInData_):

```javascript
type DataRecord = Record<string, string>;

interface CookieItem {
    name: string;
    value: string;
    domain: string;
    path: string;
    expires: number;
    httpOnly: boolean;
    secure: boolean;
    sameSite: 'Strict' | 'Lax' | 'None';
}

interface LocalStorageItem {
    name: string;
    value: string;
}

interface ApiScriptInData {
  method: "DELETE" | "GET" | "POST" | "PUT";
  url: string;
  headers?: DataRecord; // valid if original headers is not undefined
  data?: any; // valid if original request data is not undefined
  cookies?: CookieItem[]; // valid if script.external includes "cookies"
  localStorage?: LocalStorageItem[]; // valid if script.external includes "localStorage"
  vars: {
    inParas: DataRecord;
    userData: DataRecord;
    [key: string]: any;
  };
  errName: string; // value of errname attribute in action_api
}

```

##### Script Output Data

The script must output a string containing the result of _JSON.stringify(outData)_ (type: _ApiScriptOutData_):

```javascript
interface ApiScriptOutData {
  /**
   * headers to be used (original headers are ignored)
   */
  headers?: HttpHeaders;
  /**
   * new headers to be added (or replaced); newHeaders is ignored if headers has a valid value
   */
  newHeaders?: HttpHeaders;
  /**
   * replace original request data if data is not undefined
   */
  data?: any;
  /**
   * optional error, such as "cfginvalid"(template/script is invalid) or "other"(task failed)
   ** invalid errName is ignored
   */
  errName?: string;
  /**
   * When cookies or localStorage are accessed, the message is ignored
   */
  message?: string;
}
```

### Input and Output Data for extract Scenario Scripts

##### Script Input Data

The script can access the global variable _inData_ (type: _ExtractScriptInData_):

```javascript
type Tabname = string; // "dat_\d{16}", such as "dat_0000000000007001"
type DataRecord = Record<string, string>;

interface ExtractScriptInData {
  vars: {
    inParas: DataRecord;
    userData: DataRecord;
    [key: string]: string;
  };
  execData: Record<Tabname, DataRecord[]>; // original data, such as responses of APIs
  tabName: string; // value ot tabname attribue in action_extract_script
  maxLoops: number; // value of maxloops attribute in action_extract_script
  errName: string; // value of errname attribute in action_extract_script
}
```

##### Script Output Data

The script must output a string containing the result of _JSON.stringify(outData)_ (type: _ExtractScriptOutData_):

```javascript
interface ExtractScriptOutData {
  /**
   * For each datatable(tabname) in execData, new records will replace or append to (action_extract_script.opType) the original records
   */
  execData: ExecData;
  /**
   * vars[varname] is set to a variable if varname starts with "extract" and does not include "." and value of vars[varname] is a string:
   ** extractSubtasks is typically used to return new subtasks, refer to action_subtask.subtasks
   ** extractError is typically used to return error messages
   */
  vars?: Record<string, string>;
  /**
   * optional error, such as "cfginvalid"(template/script is invalid) or "other"(task failed)
   ** invalid errName is ignored
   */
  errName?: string;
}
```

### Input and Output Data for fun Scenario Scripts

##### Script Input Data

The script can access the global variable _inData_ (type: _FunScriptInData_):

```javascript
interface FunScriptInData {
  origStr: string;
  arg1: string;
  arg2: string;
  arg3: string;
  arg4: string;
  arg5: string;
};
```

##### Script Output Data

The script must output a string.
