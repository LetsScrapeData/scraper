# How to Scrape Pop-up Pages

LetsScrapeData supports pop-up web pages that can be used for the current task as well as for subtasks.

### Related Actions

The following actions may trigger pop-up pages:

- **action_click**
- **action_goto**
- **action_input**
- **action_scroll_by**
- **action_scroll_intoview**
- **action_scroll_to**
- **action_select**

### Related Attributes

The default setting is that no webpage pops up. The following attributes of the action are related to the pop-up webpage:

- _popuppage_:
  - ignored: default value, don't care if the page pops up
  - required: there must be a pop-up page, otherwise it is considered abnormal
  - optional: there may be a pop-up page
- popupsubtask: If true, the popup page will be used to execute a new subtask, otherwise it will be used for the current task.
- _eurl_
- _eloc_
- _pn1_
- _pv1_
- _pn2_
- _pv2_

The attributes eurl/eloc/pn1/pv1/pn2/pv2 determine if the pop-up webpage meets certain conditions; otherwise, they consider the pop-up webpage not to exist.
