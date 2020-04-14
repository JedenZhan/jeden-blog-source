## 前言

Cookie 想必大家都很清楚了, 但是...操作 Cookie 的 API 却仅有一个, 我 ???

document.cookie 来获取 cookie 和设置 cookie

黑人问号



那我们就自己封装一个喽

## Cookie

封装前先搞清楚我们需要哪些方法, 简单来说就是 `增删改查` 那我们就大致可以把这个对象构建出来

```js
const mCookie = (() => {
    return {
        getItem (key) {
            // 获取某一个值
        },
        setItem (key, value) {
            // 设置某一个值
        },
        removeItem (key) {
            // 删除某一个值
        },
        hasItem (key) {
            // 判断有没有
        },
        keys () {
            // 获取所有 cookie 的 value
        }
    }
})()
```



## 开始写

### getItem

思路: 

- 使用 document.cookie 获取全部 cookie
- 使用正则表达式匹配出目标 cookie

```js
getItem (key) {
	if (!key) return null
    
    return 
}
```







```js
var domainRegex = /^(\.br\.|\.co\.|\.com\.|\.org\.|\.edu\.|\.net\.)/;

var docCookies = {
    getItem: function (sKey) {
        if (!sKey) { return null; }
        return decodeURIComponent(document.cookie.replace(/(?:^|.*;)\\s*/ + encodeURIComponent(sKey).replace(/[\-\.\+\*]/g, "\\$&") + "\\s*\\=\\s*([^;]*).*$)|^.*$"), "$1")) || null;
    },
    setItem: function (sKey, sValue, vEnd, sPath, sDomain, bSecure) {
        if (!sKey || /^(?:expires|max\-age|path|domain|secure)$/i.test(sKey)) { return false; }
        var sExpires = "";
        if (vEnd) {
            switch (vEnd.constructor) {
                case Number:
                    sExpires = vEnd === Infinity ? "; expires=Fri, 31 Dec 9999 23:59:59 GMT" : "; expires=" + new Date(new Date().getTime() + vEnd * 1000).toUTCString();
                    break;
                case String:
                    sExpires = "; expires=" + vEnd;
                    break;
                case Date:
                    sExpires = "; expires=" + vEnd.toUTCString();
                    break;
            }
        }
        document.cookie = encodeURIComponent(sKey) + "=" + encodeURIComponent(sValue) + sExpires + (sDomain ? "; domain=" + sDomain : "") + (sPath ? "; path=" + sPath : "") + (bSecure ? "; secure" : "");
        return true;
    },
    removeItem: function (sKey, sPath, sDomain) {
        if (!this.hasItem(sKey)) { return false; }
        document.cookie = encodeURIComponent(sKey) + "=; expires=Thu, 01 Jan 1970 00:00:00 GMT" + (sDomain ? "; domain=" + sDomain : "") + (sPath ? "; path=" + sPath : "");
        return true;
    },
    hasItem: function (sKey) {
        if (!sKey) { return false; }
        return (new RegExp("(?:^|;\\s*)" + encodeURIComponent(sKey).replace(/[\-\.\+\*]/g, "\\$&") + "\\s*\\=")).test(document.cookie);
    },
    keys: function () {
        var aKeys = document.cookie.replace(/((?:^|\s*;)[^\=]+)(?=;|$)|^\s*|\s*(?:\=[^;]*)?(?:\1|$)/g, "").split(/\s*(?:\=[^;]*)?;\s*/);
        for (var nLen = aKeys.length, nIdx = 0; nIdx < nLen; nIdx++) { aKeys[nIdx] = decodeURIComponent(aKeys[nIdx]); }
        return aKeys;
    }
};

var grCookie = {
    getItem: docCookies.getItem,
    hasItem: docCookies.hasItem,
    keys: docCookies.keys,
    setItem: function (sKey, sValue, vEnd, sPath, domains, bSecure) {
        for (var i=0;i<domains.length;i++) {
            if (!domainRegex.test(domains[i])) {
                docCookies.setItem(sKey, sValue, vEnd, sPath, domains[i], bSecure);
                break;
            }
        }
    },
    removeItem: function (sKey, sPath, sDomain) {
        for (var i=0;i<sDomain.length;i++) {
            if (!domainRegex.test(sDomain[i])) {
                docCookies.removeItem(sKey, sPath, sDomain[i])
                break;
            }
        }
    }
}

export default grCookie;

```

