
### Template Config
```xml
<?xml-model href="https://www.LetsScrapeData.com/xsd/lsd_en.xsd" type="application/xml" schematypens="http://www.w3.org/2001/XMLSchema"?>
<template tid="10011" version="0.0.6" commited="true">
  <attrs>
    <attr name="name" value="Demo - token captcha solver" />
    <attr name="desc" value="Demo - token captcha solver: solve GeeTest(V3/V4), Recaptcha(V2/V3), Cloud Flare(turnstile) captchas" />
    <attr name="domainId" value="1" />
    <attr name="cfgShareLevel" value="120" />
    <attr name="parasstr" value="https://2captcha.com/demo/cloudflare-turnstile" />
  </attrs>
  <paras>
    <para paraname="para1" name="pageUrl" desc="pageUrl, url of web page to be opened" />
  </paras>
  <actions>
    <action_goto url="${inParas.para1}" wait="5000" />
    <action_captcha>
      <!-- <captcha_geetest/> -->
      <!-- <captcha_recaptcha minscore="0.5" /> -->
      <captcha_turnstile />
    </action_captcha>
  </actions>
</template>
```
