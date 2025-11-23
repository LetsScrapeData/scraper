<div align="center">
  <div>
    <a href="https://www.LetsScrapeData.com" style="text-decoration: none" target="_blank">
      <img src="https://www.letsscrapedata.com/assets/logo.svg" width="160" alt="LetsScrapeData">
    </a>
  </div>
  <!-- <div>This is part of LetsScrapeData <a href="https://www.npmjs.com/~letsscrapedata"> web scraping suites </a>.</div> -->
  <div>You can use a free <a href="https://www.LetsScrapeData.com">LetsScrapeData App</a> if you want to scrape web data without programming.</div>
  <br/>
</div>

<font size=4>Please get help and discuss how to scrape a website on the [discord server](https://discord.gg/46atZ8kPVb), which can respond quickly. It is better to submit issues on [github](https://github.com/LetsScrapeData/scraper) for better tracking.</font>

## Features

1. Template driven web scraping

- The templates are intuitive and easier to maintain.

2. Browser operations supported by the [controller](https://www.npmjs.com/package/@letsscrapedata/controller) package

- Same interface of playwright, patchright, camoufox, puppeteer, cheerio: easy to switch between them
- Web browsing automation: goto(open) / click / input / hover / select / scroll
- Automatic captcha solver: Recaptcha(v2 & v3), Cloudflare Turnstile, GeeTest(v3 & v4), image/text, cooridinate
- State data management: cookies, localStorage, HTTP Headers, custom session data
- Elements selection by CSS selectors or XPath: whether in frames or not
- Automatic file saving: such as screenshot, pdf, mhtml, download directly or by clicking

3. API request

- Both browser and API can be used at the same time and cookies/headers are shared.
- HTTP headers: intercepted, generated automatically or by browser automation, got by API or others

4. fingerprint management:

- Automatically generate fingerprints of the latest common browsers

5. Simple rate limits: automatic flow control, such as interval / max concurrency /times per period
6. Simple proxy management: multiple "static" proxies to increase concurrency
7. Subtasks: complex task can be split into multiple simple subtasks for better maintenance and increased concurrency
8. Data export

## Install

```sh
npm install @letsscrapedata/scraper
```

## Examples

1. Example with default ScraperConfig:

```javascript
// javascript
import { scraper } from "@letsscrapedata/sraper";

/**
 * tid: ID of template to be executed, such as template for scraping one list of example in page "https://www.letsscrapedata.com/pages/listexample1.html"
 * parasstrs: input parameters of tasks, such as "1"
 * this example will execute five tasks using template 10001, each of them scrapes the data in one page.
 */
const newTasks = [{ tid: 10001, parasstrs: ["1", "2", "3", "4", "5"] }];

/* The following line can do the same thing using subtasks, scraping the data in the first five pages */
// const newTasks = [{ tid: 10002, parasstrs: ["5"] }];

await scraper(newTasks);
```

2. Templates
- The simplest way is to use an existing template. You can search [Scrapers](/scrapers/readme) or [Discord](https://discord.gg/46atZ8kPVb) to see if there is a template that meets your requirements.
- You can also quickly [design templates](/start/readme) for scraping different websites.
- Alternatively, you can ask someone else on [Discord](https://discord.gg/46atZ8kPVb) to help you design a template.

3. Example with ScraperConfig

```javascript
// typescript
import { scraper, TemplateTasks, ScraperConfig } from "@letsscrapedata/sraper";

const scraperConfig: ScraperConfig = {
  browserConfigs: [
    /* launch a chromium browser using puppeteer, no proxy */
    { browserControllerType: "puppeteer", proxyUrl: "" },
    /* launch a chromium browser using playwright, proxy */
    { browserContollerType: "playwright", proxyUrl: "http://proxyId:port" },
    /* connect to the current browser using patchright */
    { browserUrl: "http://localhost:9222/" },
  ],
  // exitWhenCompleted: true,
  // lsdLaunchOptions: { headless: true },
  // loadUnfinishedTasks: true,
  // loadFailedTasksInterval: 5
  // captcha: { clientKey: "xxx" } // to solve captcha using 2captca
};

const newTasks: TemplateTasks[] = [{ tid: 10002, parasstrs: ["9"] }];

await scraper(newTasks, scraperConfig);
```

## ScraperConfig

Common configurations:

- Proxies and browser: browserConfigs, by default launching a browser using browserControllerType/browserType, without proxy
- Launch options of browser: lsdLaunchOptions, default {headless: false}
- Whether to load unfinished tasks: loadUnfinishedTasks, default false
- Whether to exist when completed: exitWhenCompleted, default false
- File format of scraped data: dataFileFormat, default "jsonl"
- API Key of captcha solver: captcha.clientKey

Complete configurations:

```javascript
export interface ScraperConfig {
  /**
   * @default false
   */
  exitWhenCompleted?: boolean;
  /**
   * whether to use the parasstr in XML if parasstr of a task is ""
   * @default false
   */
  useParasstrInXmlIfNeeded?: boolean;
  /**
   * whether to load unfinished tasks
   * @default false
   */
  loadUnfinishedTasks?: boolean;
  ////////////////////////////////////////////////////////////////////////////    directory
  /**
   * @default "", which will use current directory of process + "/data/"
   * if not empty, baseDir must be an absolute path, and the directory must exist and have read and write permissions.
   */
  baseDir?: string;
  /**
   * filename in action_setvar_get/get_file must include inputFileDirePart for security.
   * @default "LetsScrapeData"
   */
  inputFileDirPart?: string;
  ////////////////////////////////////////////////////////////////////////////    browser
  /**
   * wether to use puppeteer-extra-plugin-stealth, use patchright instead
   * @default false
   */
  useStealthPlugin?: boolean;
  /**
   * default browserControllerType of BrowserConfig
   * @default "patchright"
   */
  browserControllerType?: BrowserControllerType;
  /**
   * default browserType of BrowserConfig
   * @default "chromium"
   */
  browserType?: LsdBrowserType;
  /**
   * @default { headless: false, geoip: true }
   */
  lsdLaunchOptions?: LsdLaunchOptions;
  /**
   * @default {browserUrl: ""}
   */
  lsdConnectOptions?: LsdConnectOptions;
  /**
   * Important: browsers to be launched or connected using proxyUrl
   * @default [{proxyUrl: ""}], launch a default browser using default type of browser controller, no proxy
   */
  browserConfigs?: BrowserConfig[];
  ////////////////////////////////////////////////////////////////////////////    captcha
  captcha?: {
    /**
     * clientKey of 2captcha
     */
    clientKey: string;
    // if you need to solve captcha in camoufox, please contact administrator
  },
  ////////////////////////////////////////////////////////////////////////////    template
  /**
   * the default maximum number of concurrent tasks that can execute the same template in a browserContext
   * @default 1
   */
  maxConcurrency?: number;
  /**
   * @default ""
   */
  readCode?: string;
  /**
   * @default []
   */
  templateParas?: TemplatePara[];
  ////////////////////////////////////////////////////////////////////////////    scheduler
  /**
   * @default 10
   */
  totalMaxConcurrency?: number;
  /**
   * min miliseconds between two tasks of the same template
   * @default 2000
   */
  minMiliseconds?: number,
  ////////////////////////////////////////////////////////////////////////////    data
  /**
   * whether to move all dat_* files into a new directory "yyyyMMddHHmmss"
   * @default false
   */
  moveDataWhenStart?: boolean;
  /**
   ** DataFileFormat = "csv" | "jsonl" | "tsv" | "txt";
   * @default "jsonl"
   */
  dataFileFormat?: DataFileFormat;

   * valid only when dataFileFormat is "txt"
   */
  columnSeperator?: string;
}

/**
 * Only one of browserUrl and proxyUrl will take effect, and browserUrl has higher priority.
 */
export interface BrowserConfig {
  browserControllerType?: BrowserControllerType;
  /**
   * url used to connected the current browser
   ** url starts with "http://", such as "http://localhost:9222/"
   ** browserUrl can be used when mannaul login in advance.
   */
  browserUrl?: string;
  /**
   * proxy
   ** no proxy will be used if proxyUrl is ""
   ** valid only if !browserUrl
   */
  proxyUrl?: string;
  /**
   * type of browser to be launched
   * valid only if !browserUrl
   * @default "chromium"
   */
  browserType?: LsdBrowserType;
}
```
