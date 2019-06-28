---
description: Extensions Getting Started Part 1
title: Build a simple extension that pops up NASA picture of the day.
author: Peter Kellner
ms.author: xxx
ms.date: 6/15/2019
ms.topic: article
ms.prod: microsoft-edge-chromium
keywords: edge-chromium, web development, html, css, javascript, developer, extensions
---

# Build a simple extension that pops up NASA picture of the day

* Extension technologies covered in this part 1.
  * Manifest basics
  * Icons associated with extension
  * Default modal popup when extension icon clicked

In part 1, our goal is to build a very simple Chromium extension starting with an empty directory.  Our goal for this extension is the following:

* It has icons associated with it for use by the Chromium extension engine
* It has a very simple manifest.json file
* It has a launch icon that when clicked displays a popup window containing the NASA picture of the day
* It uses the browser LocalStorage to keep from hitting the NASA API to frequently

Every extension must have a `manifest.json` file in its root.  You can think of this as the blueprint for the extension. It tells the browser engine what version the extension is programmed to, the name and description of the extension and lots of other details, many of which we will get to in this multi-part Extension Getting Started Guide. Since this is just part 1, let's create a minimal extension with just some basic information.

Below is the simple  `manifest.json`
```JSON
{
  "name": "NASA Picture of the day viewer",
  "version": "0.0.0.1",
  "manifest_version": 2,
  "description": "A chromium extension to show NASA's Picture of the Day."
}
```

Next thing is to some icons to our `manifest.json` file (and create a new `/icons` directory with the files). When we finally create our package to be installed, these icons will be used for things the button the user clicks to launch the extension (if there is one), images in the store that browser users search to find your extension and other places that are appropriate.  

PNG is the recommended format, but you can also use BMP, GIF, ICO and JPEG. It is recommended to always have at least a 128x128 size icon and the browser will automatically resize it as necessary.

Your directory structure will now look like this

.  
+-- _manifest.json  
+-- icons  
|   +-- nasapod16x16.png  
|   +-- nasapod32x32.png  
|   +-- nasapod48x48.png  
|   +-- nasapod128x128.png  

and your updated `manifest.json` file is as follows.

```JSON
{
  "name": "NASA Picture of the day viewer",
  "version": "0.0.0.1",
  "manifest_version": 2,
  "description": "A chromium extension to show NASA's Picture of the Day.",
  "icons": {
    "16": "icons/nasapod16x16.png",
    "32": "icons/nasapod32x32.png",
    "48": "icons/nasapod48x48.png",
    "128": "icons/nasapod128x128.png"
  }
}
```

As I said earlier, the `manifest.json` is the blueprint (or brains) of the extension. That said, without doing any custom programming, we can add to the extension an html file that will automatically get run when the user clicks on the extension icon (as shown here).

![Toolbar Badge Icon](media/part1-badge1.png)

  The entry we need to add to the `manifest.json` file is `browser_action` and just like `name`, `description`, etc., it's a top level entry. We've named it `popup/popup.html` because, well, it's a popup but we could call it anything.  Clicking on the extension icon launches `popup/popup.html` as  modal dialog that stays up until you click any where outside the dialog.

  Adding our `popup/popup.html` as our default popup for our extensions gives us an updated `manifest.json` as follows.

```JSON
{
  "name": "NASA Picture of the day viewer",
  "version": "0.0.0.1",
  "manifest_version": 2,
  "description": "A chromium extension to show NASA's Picture of the Day.",
  "icons": {
    "16": "icons/nasapod16x16.png",
    "32": "icons/nasapod32x32.png",
    "48": "icons/nasapod48x48.png",
    "128": "icons/nasapod128x128.png"
  },
  "browser_action": {
    "default_popup": "popup/popup.html"
  }
}
```

In a minute, we'll create our popup.html (in a folder off the root of our extension), but for now, let's also bring into our project an image file `images/stars.jpeg` so we have something built into our extension that we can display in our `popup.html` file.

So, in folder popup, let's add the file `popup.html` and let's just have it render our stars image. Here's the `popup.html` file.

```HTML
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>NASA Picture of the Day</title>
  </head>
  <body>
    <div>
      <img src="/images/stars.jpeg" alt="stars" />
    </div>
  </body>
</html>
```

Now, our folder structure for our extension is this.

.  
+-- _manifest.json  
+-- icons  
|   +-- nasapod16x16.png  
|   +-- nasapod32x32.png  
|   +-- nasapod48x48.png  
|   +-- nasapod128x128.png  
+-- popup  
|   +-- popup.html  
+-- images  
|   +-- stars.jpeg  

That's everything we need to build a working extension. Now, all we need to do is test it.  In the next section, I'll show you how to load the extension (we call that side loading) into your Edge Chromium browser so you can run it.