# Live Routings

Since the version 5.4.6, the Askia Rendering Engine (Design.exe’s screen mode or AskiaExt.dll) is able to answer on certain [AJAX](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events) requests.

It’s useful for live routing or to navigate in the interview without to refresh the entire page.

But the Askia Rendering Engine is not responsible about how the client browser will interpret the response of the AJAX requests.

It means it should be take into account in the ADPs and ADCs to send the [AJAX](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events) requests to the server side and also to apply the modifications depending of the response sent by the server.

## ADP

The `askia.live.routing.js` file should be included in the `dynamic` folder of the ADPs and the `askia.ajax.min.js` should be included in the `static` folder of the ADPs.

### askia.live.routing.js:  
It creates 2 arrays (`arrLiveRoutingInputCode` and `arrLiveRoutingShortcut`) and attach it to the window object

* `window.arrLiveRoutingInputCode` is an array of input codes of the source questions of the live routings in the current page
* `window.arrLiveRoutingShortcut` is an array of shortcut of the source questions of the live routings in the current page

### askia.ajax.min.js:
This file manage the [AJAX](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events) requests and responses.

## ADC
For the ADCs, you will need to call `askia.triggerAnswer()` to send the input's form to the server side when needed so usually when the input's data change. An example of the code used in an ADC:

```javascript
/**
* Send the input's form to the server side only if the current question
* is a source question of a live routing on the page
*/
if (window.askia 
  && window.arrLiveRoutingShortcut 
  && window.arrLiveRoutingShortcut.length > 0
  && window.arrLiveRoutingShortcut.indexOf(options.currentQuestion) >= 0) {
  askia.triggerAnswer();
}
```

> Attention, make sure to call this method `askia.triggerAnswer();` only if the current question is a source question of a live routing on the page to limit the number of requests send to the server.

The current implementation of the live routings in `askia.ajax.min.js` are for [askiaShowQuestion](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events#askiashowquestion), [askiaHideQuestion](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events#askiahidequestion) and [askiaReload](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events#askiareload).

[For more details...](https://github.com/AskiaADX/ADXStudio/wiki/Javascript-Ajax-Events)
