```js
function (e) {
    e = e || window.event;
    if (e){
        e.returnValue = '关闭浏览器聊天内容将会丢失。';
    }

    setTimeout(function() {
        // report session data
        console.time('report');
        var stayTime = new Date().getTime() - accountFactory.getLoginTime();
        reportService.report(reportService.ReportType.sessionData, {
            uin: accountFactory.getUin(),
            browser: navigator.userAgent,
            rmsg: accountFactory.getRMsgCount(),
            rconv: accountFactory.getRConvCount(),
            smsg: accountFactory.getSMsgCount(),
            sconv: accountFactory.getSConvCount(),
            lifetime: stayTime
        }, true);
    }, 0);

    return '关闭浏览器聊天内容将会丢失。';
}
```

