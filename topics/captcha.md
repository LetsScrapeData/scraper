

# How to Solve Captchas

Some captchas can be bypassed by using a high-quality proxy or rate limiting. Some captchas cannot be bypassed, such as those used when logging in or visiting a website for the first time. Most common captchas can be automatically resolved using third-party services.

LetsScrapeData can automatically solve common captchas, including Recaptcha(v2 & v3), Cloudflare Turnstile, GeeTest(v3 & v4), image/text, cooridinate, , with the help of third-party services (such as 2captcha). More types of CAPTCHAs can be supported as needed.

### How to sovle Recaptcha captchas
The following action can automatically solve Recpatcha(v2 & v3) captchas:
```xml
<action_captcha>
  <captcha_recaptcha />
  <!-- <captcha_recaptcha minscore="0.5" /> -->
</action_captcha>
```
Example: [template 10011](/examples/tid10011_captchaToken.md)

### How to sovle Cloudflare Turnstile captchas
The following action can automatically solve Cloudflare captchas:
```xml
<action_captcha>
  <captcha_turnstile />
</action_captcha>
```
Example: [template 10011](/examples/tid10011_captchaToken.md)

### How to sovle GeeTest captchas
The following action can automatically solve GeeTest(v3 & v4) captchas:
```xml
<action_captcha>
  <captcha_geetest/>
</action_captcha>
```
Example: [template 10011](/examples/tid10011_captchaToken.md)

### How to sovle image/text captchas
The following action can automatically solve image/text captchas:
```xml
<action_captcha>
  <captcha_text>
    <image_element>
      <element loc="${inParas.para2}" />
    </image_element>
    <input_element>
      <element loc="${inParas.para3}" />
    </input_element>
    <submit_element>
      <element loc="${inParas.para4}" />
    </submit_element>
    <check_result attr="${inParas.para6}" failedstr="${inParas.para7}">
      <element loc="${inParas.para5}" />
    </check_result>
  </captcha_text>
</action_captcha>
```
Example: [template 10012](/examples/tid10012_captchaText.md)

### How to sovle coordinate captchas
The following action can automatically solve coordinate captchas:
```xml
<action_captcha>
  <captcha_coordinate lang="zh">
    <image_element>
      <element loc="${inParas.para4}" />
      <element loc="${inParas.para5}" />
    </image_element>
    <!-- <submit_element>
      <element loc="${inParas.para4}" />
    </submit_element> -->
    <check_result attr="" failedstr="">
      <element loc="${inParas.para4}" />
    </check_result>
  </captcha_coordinate>
</action_captcha>
```
Example: [template 10013](/examples/tid10013_captchaCoordinate.md)
