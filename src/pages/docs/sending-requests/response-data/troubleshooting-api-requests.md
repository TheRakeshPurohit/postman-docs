---
title: "Debug API requests using the Postman Console"
updated: 2023-10-05
contextual_links:
  - type: section
    name: "Additional resources"
  - type: subtitle
    name: "Videos"
  - type: link
    name: "Debugging with the Console | Postman Level Up"
    url: "https://www.youtube.com/watch?v=YCsURct9wCk&list=PLM-7VG-sgbtC5tNXxd28cmePSa9BYwqeU&index=9"
  - type: link
    name: "Clear the Console | Postman Level Up"
    url: "https://youtu.be/assHxTMirnk"
  - type: subtitle
    name: "Blog posts"
  - type: link
    name: "Powerful Debugging with the Postman Console"
    url: "https://blog.postman.com/powerful-debugging-with-the-postman-console/"
---

If your API request isn't behaving as expected, there can be many possible reasons. To find out what the problem is, you can use the Postman Console to troubleshoot your request. This guide also lists common issues and their causes.

> This guide specifically discusses troubleshooting API requests. To troubleshoot issues with the Postman app, see [Troubleshoot app issues](/docs/introduction/troubleshooting-inapp/). To troubleshoot issues with Postman Monitors, see [Troubleshooting monitors](/docs/monitoring-your-api/troubleshooting-monitors/).

## Contents

* [Troubleshooting your requests](#troubleshooting-your-requests)
* [Debugging in the Console](#debugging-in-the-console)
* [Common issues](#common-issues)
* [Getting help](#getting-help)

## Troubleshooting your requests

Postman will indicate any whitespace or invalid characters in parts of your request that may not function as expected so that you can rectify your values. Invalid characters are highlighted in the request method, URL (including the path), parameters, headers (including your key names), and body.

<img alt="Invalid Characters" src="https://assets.postman.com/postman-docs/invalid-character-message-v9.jpg" width="400px"/>

If Postman isn't able to send your request or doesn't receive a response, you will get a message with details about the error. Select __View in Console__ to get an overview of your request and to help identify the source of the issue.

## Debugging in the Console

Every request sent by Postman is logged in the Postman Console, so you can view the detail of what happened when you sent a request. This means you can use the Console to help debug your requests when an API isn't behaving as you expect. Keeping the Console open while you work will increase the visibility of your network calls and log messages while debugging.

The Postman Console logs the following information:

* The primary request that was sent, including all underlying request headers, variable values, and redirects.
* The proxy configuration and certificates used for the request.
* Network information such as IP addresses, ciphers, and protocols used.
* Log statements and asynchronous requests from test or pre-request scripts.
* The raw response sent by the server before it's processed by Postman.

> Monitor results are logged to a separate console. For more information on how to view logs from a monitor run, see [Viewing monitor results](/docs/monitoring-your-api/viewing-monitor-results/#console-log).

### Opening the Console

Open the Console by selecting <img alt="Console icon" src="https://assets.postman.com/postman-docs/icon-console-v9.jpg#icon" width="16px"> **Console** in the Postman footer. In the Postman desktop app, you can use **⌘+Option+C** or **Ctrl+Alt+C** to open the Postman Console in a new window.

### Viewing request errors from the Console

You will get an error message if Postman isn't able to send your request or doesn't receive a response from the API you sent the request to. This message includes an overview of the issue and a link to the Console. There you can access detailed information about the request.

![Request not sent](https://assets.postman.com/postman-docs/v10/response-error-console-link-v10-22.jpg)

Select __View in Console__ to inspect the request details in the Console and find out more about what went wrong.

<img alt="Error in Console" src="https://assets.postman.com/postman-docs/v10/console-pane-opened-from-response-v10-22.jpg" width="506px"/>

### Navigating the Console

The Postman Console displays network information and the request and response headers and body for each request, together with any Console output messages coming from your scripts.

Filter by log message type under **All Logs**. Select the more actions icon <img alt="More actions icon" src="https://assets.postman.com/postman-docs/icon-more-actions-v9.jpg#icon" width="16px"> to turn timestamps and network information on or off.

<img alt="Console options" src="https://assets.postman.com/postman-docs/v10/console-pane-log-options-v10-22.jpg" width="371px"/>

The Console will log the last 5,000 messages and 24 hours by default. Select __Clear__ to empty the list.

### Using log statements

Using log statements at appropriate locations in your test scripts can help you debug your requests. Postman accepts the following log statements:

* `console.log()`
* `console.info()`
* `console.warn()`
* `console.error()`
* `console.clear()`

<img alt="Console info" src="https://assets.postman.com/postman-docs/v10/console-logs-in-pane-v10-1.jpg" />

## Common issues

If your issue with sending a request isn't listed here, see [Getting help](#getting-help) for information how to contact Postman support.

Issue | Resolving the issue
--- | ---
**Connectivity** | If Postman fails to send your request, you may be experiencing connectivity issues. Check your connection by attempting to open a page in your web browser.
**Firewalls** | Some firewalls may be configured to block non-browser connections. If this happens you will need to contact your network administrators for Postman to work.
**Proxy configuration** | If you are using a proxy server to make requests, check your configuration. By default, Postman uses the proxy settings configured in your operating system's network settings. The [Postman Console](#debugging-in-the-console) will provide debugging information regarding proxy servers.
**SSL certificates** | You may experience issues using HTTPS connections. You can turn off **SSL certificate verification** in [Settings](/docs/getting-started/installation/settings/) by selecting the settings icon <img alt="Settings icon" src="https://assets.postman.com/postman-docs/icon-settings-v9.jpg#icon" width="16px"> then **Settings > General**. If that doesn't help, your server might be using a client-side SSL connection, which you can configure by selecting the settings icon <img alt="Settings icon" src="https://assets.postman.com/postman-docs/icon-settings-v9.jpg#icon" width="16px"> then **Settings > Certificates**. Use the [Postman Console](#debugging-in-the-console) to ensure that the correct SSL certificate is being sent to the server. Learn more about [working with certificates](/docs/sending-requests/authorization/certificates/).
**Client certificates** | Client certificates may be required for your API server. You can [add a client certificate](/docs/sending-requests/authorization/certificates/) in [Settings](/docs/getting-started/installation/settings/) by selecting the settings icon <img alt="Settings icon" src="https://assets.postman.com/postman-docs/icon-settings-v9.jpg#icon" width="16px"> then **Settings > Certificates**.
**Wrong request URLs** | If you are using variables or path parameters with your request, make sure the final address is correct by opening the [Postman Console](#debugging-in-the-console), which will display the URL your request was sent to when it executed. Unresolved request variables can result in invalid server addresses.
**Wrong protocol** | Check if you're using `https://` instead of `http://` in your URL (or the opposite).
**Short timeouts** | If you configure a short timeout in Postman, the request could be timing out before completion, resulting in an error. To avoid this issue, increase the **Request timeout** in [Settings](/docs/getting-started/installation/settings/) by selecting the settings icon <img alt="Settings icon" src="https://assets.postman.com/postman-docs/icon-settings-v9.jpg#icon" width="16px"> then **Settings > General**.
**Invalid responses** | If your server sends the wrong response encoding errors, or invalid headers, Postman may fail to interpret the response.
**TLS version** | Postman supports TLS version 1.2 and higher, which [may not be supported if you are using an older browser or operating system](https://support.postman.com/hc/en-us/articles/360041392573-Deprecating-TLS-1-0-and-TLS-1-1).
**Postman errors** | It's possible that Postman might be making invalid requests to your API server. You can confirm this by checking your server logs, if available. If you believe this is happening, contact the Postman team using the [GitHub issue tracker](https://github.com/postmanlabs/postman-app-support/issues).
**Unresolved variables** | An unresolved variable isn't defined in an active scope that's available for the request it’s used in. For more information on why this happens and how to solve the problem, see [Fixing unresolved variables](/docs/sending-requests/variables/variables/#fixing-unresolved-variables).
**CORS** |If the [Postman web app](/docs/getting-started/installation/installation-and-updates/#use-the-postman-web-app) fails to send your request, you may be experiencing a cross-origin resource sharing (CORS) error. Make sure you're using the best [Postman Agent](/docs/getting-started/basics/about-postman-agent/) for your request.

## Getting help

If you are still having problems with your request, there are options for you to get help:

* Ask for community help in the [Postman forum](https://community.postman.com/).
* If you think the problem is with Postman itself, search the [issue tracker](https://github.com/postmanlabs/postman-app-support/issues) on GitHub to check if someone has already reported the issue and whether there is a known solution.
* If you need to include confidential data, file a support ticket with [Postman support](https://support.postman.com/hc/en-us), including your Console logs.