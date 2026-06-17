# How to Use Scripts

虽然LetsScrapeData模板支持上百个预定义函数和字符串模板进行大多数数据处理和计算，在计算复杂时，仅使用这些函数可能是模板过于复杂，此时可使用脚本。目前仅支持JavaSCript脚本。

> 提醒：
>
> - 虽然支持脚本，出于性能、后期维护等原因(比如出于安全原因，可能对脚本进行更严格的限制)，建议优先使用预定义函数，除非必要时才使用自定义脚本。
> - **js-isolated**类型脚本相对安全；**js-vm2**类型脚本进行了限制，但仍存在安全隐患；我们随时可能根据需要进行更严格的限制。
> - 建议尽可能使用**js-isolated**类型脚本，以后extract和fun场景可能仅支持该类型脚本。
> - 如果存在潜在安全隐患，将来可能需要先通过评审、对用户提示安全风险、或仅对信用级别高的设计者开放等。
> - 如果发现任何潜在恶意脚本，永久禁止使用。

### 安全考虑

出于安全原因：

- 所有脚步的输入数据先序列化为字符串后传入，再根据具体场景，转换为对应对象。
- 所有脚本的输出数据只能为字符串传出，再根据具体场景，转换为对应对象。
- 针对不同类型脚本，限制了可使用的资源、外部程序包、函数。

### 脚本类型

脚本类型决定脚本可以使用的功能，LetsScrapeData支持如下类型的自定义JavaScript脚本：

- **js-isolated**脚本：脚本仅能使用原生JavaScript支持的功能(不能使用crypto、Buffer等)，只能读取外部传入的数据。
- **js-vm2**脚本：脚本可使用原生JavaScript支持的功能和如下指定的程序包和函数，只能读取外部传入的数据。
  - crypto
  - Buffer
  - URL
  - URLSearchParams
  - 根据需要，其它可安全使用的函数
  <!-- - cheerio -->

### 脚本使用场景

脚本使用场景决定脚本的用途、输入和输出数据，LetsScrapeData模板支持在以下场景执行自定义JavaScript脚本：

- **api**：用于计算API请求中复杂的请求头和请求数据，比如加密的签名参数；通过**action_api**的*scriptname*属性指定脚本。
- **extract**"：用于从采集的原始数据中提取需要的数据；通过**action_extract_script**的*scriptname*属性指定脚本。
- **fun**"：用于从采集的原始数据中提取需要的数据；通过**action_extract_script**的*scriptname*属性指定脚本。

以上场景的脚步均可通过全局变量inData访问输入数据，具体定义参见后面说明。

除了以上场景，在**action_setvar_get.get_evulate**中也可使用JavasScript脚本，出于安全原因，不能用于访问cookies和localStorage；以后为了安全，可能更严格限制其使用，因此建议尽量避免使用**get_evaluate**。

### 脚本配置

1. 针对不同的脚本使用场景，使用*scriptname*属性设置引用的脚本名称。
2. 根据需要，使用**scripts.script**对每个脚本进行配置：

- _name_：脚本名称，必须与上面的scriptname同名。
  - 脚本内容保存在单独的脚本文件中，该文件必须位于模板所在目录的scripts目录下，文件名为scriptname，文件扩展名为"js"；在保存和调试模板时，会自动读取该脚本文件内容。
- _scenario_：脚本使用场景，有效值为"api"、"extract"、"fun"，不同场景的输入和输出数据不同，参见后面说明。
- _solution_: 脚本类型，有效值为"js-isolated"、"js-vm2"。
- _externals_："cookies"、"localStorage"、"pageEvaluate"等，多个以逗号分割；仅当"scenario"为"api"、且*solution*为"js-vm2"时有效。
  - cookies和localStorage为状态数据中的内容，参见[如果需要登录](/topics/login)

### 脚本文件总体说明

所有类型脚本均遵从以下说明：

- 第一部分：脚本说明和模拟输入，可选，可包含如下内容：
  - 版本说明: 如需要，必须放第一行，比如 "// version: 1.0.0"
  - 脚本其它说明：需要为注释格式
  - 模拟输入：比如inData，单独调试脚本时使用；非调试时，会自动传入相关内容，详见后面不同场景的详细说明。
  - 第一部分结束分割行：如果有这部分内容，必须包含此行内容，必须以"// start of script:"开头，表示下一行开始为脚本真实内容
- 第二部分：脚本真实内容，可包含注释内容；模板仅保存这部分内容。
  - **js-isolated**类型脚本的最后一行脚本必须是字符串、存有字符串的变量，或者是返回字符串的函数，不要使用return；具体请参考[isolated-vm](https://www.npmjs.com/package/isolated-vm)。
  - **js-vm2**类型脚本需要将一个函数赋值给module.exports，该函数无输入参数，返回字符串；具体请参考[vm2](https://www.npmjs.com/package/vm2)。
- 第三部分：调试打印部分，可选
  - 第三部分开始分割行：如果有这部分内容，必须包含此行内容，必须以"// end of script:"开头，表示从行开始为第三部分内容。
  - 其它内容：一般打印执行脚本的输出结果，用于调试。

### api场景脚本的输入和输出数据

##### 脚本输入数据

脚本可访问全局变量inData: ApiScriptInData:

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
  headers?: DataRecord; // original headers
  data?: any; // original request data
  cookies?: CookieItem[]; // valid if script.externals includes "cookies"
  localStorage?: LocalStorageItem[]; // valid if script.externals includes "localStorage"
  vars: {
    inParas: DataRecord;
    userData: DataRecord;
    [key: string]: any;
  };
  errName: string; // value of errname attribute in action_api
}

```

##### 脚本输出数据

脚本需要输出文本JSON.stringify(outData: ApiScriptOutData):

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
  errName?: string;
  message?: string;
}
```

### extract场景脚本的输入和输出数据

##### 脚本输入数据

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

##### 脚本输出数据

```javascript
interface ExtractScriptOutData {
  execData: Record<Tabname, DataRecord[]>; // new execData that replace or append the original execData
  errName?: string;
  vars?: Record<string, string>; // key must be start with "extract", or ignored
}
```

### fun场景脚本的输入和输出数据

##### 脚本输入数据

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

##### 脚本输出数据
