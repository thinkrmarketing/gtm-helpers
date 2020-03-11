<script id="gtm-jq-ajax-listen" type="text/javascript">
 (function() {
  'use strict';
 var $;
 var n = 0;
 init();
  function init(n) {
  // Ensure jQuery is available before anything
 if (typeof jQuery !== 'undefined') {
  // Define our $ shortcut locally
 $ = jQuery;
 bindToAjax();
  // Check for up to 10 seconds
 } else if (n < 20) {
 n++;
 setTimeout(init, 500);
 }
 }
  function bindToAjax() {
  $(document).bind('ajaxComplete', function(evt, jqXhr, opts) {
 var fullUrl = document.createElement('a');
 fullUrl.href = opts.url;
 var pathname = fullUrl.pathname[0] === '/' ? fullUrl.pathname : '/' + fullUrl.pathname;
 var queryString = fullUrl.search[0] === '?' ? fullUrl.search.slice(1) : fullUrl.search;
 var queryParameters = objMap(queryString, '&', '=', true);
 var headers = objMap(jqXhr.getAllResponseHeaders(), '\n', ':');
 dataLayer.push({
 'event': 'ajaxComplete',
 'attributes': {
 'type': opts.type || '',
 'url': fullUrl.href || '',
 'queryParameters': queryParameters,
 'pathname': pathname || '',
 'hostname': fullUrl.hostname || '',
 'protocol': fullUrl.protocol || '',
 'fragment': fullUrl.hash || '',
 'statusCode': jqXhr.status || '',
 'statusText': jqXhr.statusText || '',
 'headers': headers,
 'timestamp': evt.timeStamp || '',
 'contentType': opts.contentType || '',
 'response': (jqXhr.responseJSON || jqXhr.responseXML || jqXhr.responseText || '')
 }
 });
  });
  }
  function objMap(data, delim, spl, decode) {
  var obj = {};
 if (!data || !delim || !spl) {
  return {};
  }
  var arr = data.split(delim);
 var i;
  if (arr) {
  for (i = 0; i < arr.length; i++) {
 var item = decode ? decodeURIComponent(arr[i]) : arr[i];
 var pair = item.split(spl);
  var key = trim_(pair[0]);
 var value = trim_(pair[1]);
  if (key && value) {
  obj[key] = value;
  }
  }
  }
  return obj;
  }
 function trim_(str) {
  if (str) {
  return str.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '');
  }
  }
  })();
 </script>