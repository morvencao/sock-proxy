# Set up SOCK proxy for slack desktop app on macOS

1. Create a SOCK proxy to that server, if you're using SS, there will be a default sock proxy:
```
127.0.0.1:1086
```
2. Go to System Preferences
3. Select your network interface (most probably WIFI or Wired connection)
4. Click on Advanced..
5. Click on Proxies tab
6. Select and check off Automatic Proxy Configuration
7. Paste in this URL: https://raw.githubusercontent.com/morvencao/sock-proxy/master/slack-proxy.pac
7. Apply the changes

Applying `proxy.pac` configuration file hosted on Github on macOS
**Note: The proxy.pac file must be served from http[s]. Local files don't work on recent macOS systems, since file:// URLs are sandboxed. Use Github :)**

```
function FindProxyForURL(url, host) {

    if (shExpMatch(host, "slack.com") ||
        shExpMatch(host, "*.slack.com") ||
        shExpMatch(host, "*.slack-msgs.com") ||
        shExpMatch(host, "*.slack-files.com") ||
        shExpMatch(host, "*.slack-imgs.com") ||
        shExpMatch(host, "*.slack-edge.com") ||
        shExpMatch(host, "*.slack-core.com") ||
        shExpMatch(host, "*.slack-redir.net")) {
        // Use SOCK proxy, or fall back to a DIRECT traffic.
        // ssh -D 1086 [user]@[server]
        return "SOCKS 127.0.0.1:1086; DIRECT";
    }

    return "DIRECT";
}
```

Here you go. Slack is working again. Enjoy!
