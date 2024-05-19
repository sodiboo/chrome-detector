# Is It Chrome?

This page uses Cloudflare's proxying functionality to determine if the user is using Chrome. `is-it-chrome.css` will actually serve a page that depends on the user agent string.

Note that "Chrome" here is defined as any user agent string that contains the word "Chrome". This includes Google Chrome, but also other browsers using the Chromium engine.

# How it works

The Cloudflare configuration uses two Transform Rules:

- If `(http.request.uri.path eq "/is-it-chrome.css" and http.user_agent contains "Chrome")` \
  Then, rewrite the path to `/its-chrome.css`
- If `(http.request.uri.path eq "/is-it-chrome.css" and not http.user_agent contains "Chrome")` \
  Then, rewrite the path to `/its-not-chrome.css`

We can then determine if the user is using Chrome without serving them any JavaScript.

I noticed that pageload causes a flash of unstyled content. You may want to set inline styles and override them with `!important` to determine what's shown to Chrome users - this way, it won't flash for non-Chrome users.