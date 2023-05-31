# Discord Token Grabber

Recently I came accross a blog post which detailed a new way to grab Discord tokens. This technique mainly hit the crypto currency community.

The steps taken to grab the token are:

  1. A TA will contact the victim. In this case the TA will explain that he is a reporter and wants to do an article on CryptoCurrency he asks if it's possible for the victim to write a piece (A bit about himself etc). On his website all he needs to do is verify      his discord account to ensure it's him writing it.
 
 (usually this process will be drawn out and will invole the TA inviting the victim to a Discord server to show he is a legit reporter etc)
 
 2. The victim will then navigate to the webpage and drag the bookmarklet into an open Discord tab.
 
 3. This will allow for a malicious javascript payload to trigger stealing the users Discord token. 


# How this Works

This leverages the use of [bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet). Which essentially allow the execution of JavaScript code without leaving the current domain.

I wrote some javascript code and then converted this to a bookmarklet using a [converter](https://chriszarate.github.io/bookmarkleter/).

![image](https://github.com/JaRm222/DiscordTokenGrabber/assets/31806899/a1351476-1a5c-4953-9210-f518c33a038a)

I then used a simple html file which would allow a user to drag this to their bookmarks bar.

```html
	<a href="javascript:void%20function(){alert(%22This%20is%20a%20bookmarklet%22)}();"> Drag this </a>
```

By enabling our bookmarks bar. Dragging the link to it and clicking on the bookmark we are greeted with an alert.

![image](https://github.com/JaRm222/DiscordTokenGrabber/assets/31806899/09258c40-a537-497d-bd23-f85450325642)

Now we know how to use a bookmarklet we need to find a way to steal a users Discord token.

A Discord token essentially allows a user to make api requests. Which can allow someone to send messages etc.

Discord have taken some mitigation strategies such as renaming window.localStorage, however, we can simply reload the page and get the token before the mitigations are executed.

```javascript
javascript:(function(){location.reload();let frame = document.createElement('iframe');document.body.appendChild(frame);alert(frame.contentWindow.localStorage.token)})()
```
So now we have everything we need to execute this phishing attack. We just need to make it more believable. Add some CSS animations etc.

![image](https://github.com/JaRm222/DiscordTokenGrabber/assets/31806899/d4dafc05-afde-4260-be55-3d78de0c522f)

This is just a quick one I made.

The TA can now make a webrequest to store the discord token and verify the user on their webpage. We can use some more javascript to create more funky stuff but this is just a barebones look into how the technique works
