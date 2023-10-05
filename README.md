# JAVASCRIPT-INTERMEDIATE

JAVASCRIPT INTERMEDIATE
WEEK 1: WINDOWS EVENT IN JAVASCRIPT
DAY 1: FRAMES AND WINDOWS
-	We started a new Module Javascript Intermediate
-	I started wit day 1 of week 1
-	We received our score card for Friday sprint

POPUPS AND WINDOW METHODS

Popups and window methods are commonly used in web development to create and manage new browser windows or pop-up dialogs. These techniques are often employed to enhance the user experience and provide additional functionality in web applications.

POPUP BLOCKING

Popup blocking is a feature found in web browsers that prevents websites from opening new browser windows or pop-up windows without user consent. This feature was introduced to improve the browsing experience and protect users from unwanted or potentially malicious pop-up content.

WINDOWS.OPEN

The syntax to open a popup is: window.open(url, name, params):

url
An URL to load into the new window.

name
A name of the new window. Each window has a window.name, and here we can specify which window to use for the popup. If there’s already a window with such name – the given URL opens in it, otherwise a new window is opened.

params
The configuration string for the new window. It contains settings, delimited by a comma. There must be no spaces in params, for instance: width:200,height=100.

Settings for params:
Position:

left/top (numeric) – coordinates of the window top-left corner on the screen. There is a limitation: a new window cannot be positioned offscreen.

width/height (numeric) – width and height of a new window. There is a limit on minimal width/height, so it’s impossible to create an invisible window.

Window features:

menubar (yes/no) – shows or hides the browser menu on the new window.
toolbar (yes/no) – shows or hides the browser navigation bar (back, forward, reload etc) on the new window.
location (yes/no) – shows or hides the URL field in the new window. FF and IE don’t allow to hide it by default.
status (yes/no) – shows or hides the status bar. Again, most browsers force it to show.
resizable (yes/no) – allows to disable the resize for the new window. Not recommended.
scrollbars (yes/no) – allows to disable the scrollbars for the new window. Not recommended.

A minimalistic Window

Creating a minimalistic window in a web application usually involves creating a simple pop-up or modal dialog with minimal UI elements. Below is an example of how you can create a minimalistic window using HTML, CSS, and JavaScript:

HTML:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minimalistic Window</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <button id="openWindowBtn">Open Window</button>

    <!-- Modal -->
    <div id="minimalisticWindow" class="modal">
        <div class="modal-content">
            <span class="close" id="closeWindowBtn">&times;</span>
            <p>This is a minimalistic window.</p>
            <p>You can put your content here.</p>
        </div>
    </div>

    <script src="script.js"></script>
</body>
</html>

CSS: 
/* Styles for the modal window */
.modal {
    display: none;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    overflow: auto;
}

.modal-content {
    background-color: #fff;
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
}

.close {
    float: right;
    font-size: 30px;
    font-weight: bold;
    cursor: pointer;
}

.close:hover {
    color: red;
}

JS: 
// Get the modal and button elements
const modal = document.getElementById('minimalisticWindow');
const openBtn = document.getElementById('openWindowBtn');
const closeBtn = document.getElementById('closeWindowBtn');

// Open the modal when the button is clicked
openBtn.addEventListener('click', () => {
    modal.style.display = 'block';
});

// Close the modal when the close button is clicked
closeBtn.addEventListener('click', () => {
    modal.style.display = 'none';
});

// Close the modal if the user clicks outside of it
window.addEventListener('click', (event) => {
    if (event.target === modal) {
        modal.style.display = 'none';
    }
});

ACCESSING POPUP FROM WINDOW

To access a popup window from the parent window in JavaScript, you can use the window.open() method to open the popup and store a reference to it. Then, you can interact with the popup window using various JavaScript methods and properties. Here's a step-by-step guide on how to do this:

Open the Popup Window:
Use the window.open() method to open the popup window and store a reference to it in a variable. You can specify the URL of the popup and give it a name that can be used to reference it later.

EG:
const popupWindow = window.open('popup.html', 'popupWindowName', 'width=400,height=300');

Accessing Popup Content:
You can interact with the content of the popup window just like you would with any other window or document. You can access elements in the popup's DOM and modify them.

EG:
// Access a specific element in the popup's document
const popupHeading = popupWindow.document.getElementById('popup-heading');

// Modify the content of the element
popupHeading.textContent = 'Hello from the parent window!';

Close the Popup Window:
You can also close the popup window programmatically when you're done with it using the window.close() method.

EG:
popupWindow.close();

Here's a complete example where we open a popup window and change the content of an element within it:

parent.html:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Parent Window</title>
</head>
<body>
    <button id="openPopupBtn">Open Popup</button>
    
    <script>
        let popupWindow;

        document.getElementById('openPopupBtn').addEventListener('click', () => {
            // Open the popup window
            popupWindow = window.open('popup.html', 'popupWindowName', 'width=400,height=300');
        });

        // Function to change the popup content
        function changePopupContent() {
            if (popupWindow) {
                const popupHeading = popupWindow.document.getElementById('popup-heading');
                popupHeading.textContent = 'Content changed from the parent window!';
            }
        }
    </script>
</body>
</html>
 
POPUP/HTML:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Popup Window</title>
</head>
<body>
    <h1 id="popup-heading">Popup Content</h1>
</body>
</html>

ACCESSING WINDOW FROM POPUP

A popup may access the “opener” window as well using window.opener reference. It is null for all windows except popups.

If you run the code below, it replaces the opener (current) window content with “Test”:

let newWin = window.open("about:blank", "hello", "width=200,height=200");

newWin.document.write(

  "<script>window.opener.document.body.innerHTML = 'Test'<\/script>"

);

So the connection between the windows is bidirectional: the main window and the popup have a reference to each other.

CLOSING A POPUP

To close a window: win.close().

To check if a window is closed: win.closed.

Technically, the close() method is available for any window, but window.close() is ignored by most browsers if window is not created with window.open(). So it’ll only work on a popup.

The closed property is true if the window is closed. That’s useful to check if the popup (or the main window) is still open or not. A user can close it anytime, and our code should take that possibility into account.

This code loads and then closes the window:

let newWindow = open('/', 'example', 'width=300,height=300');

newWindow.onload = function() {

  newWindow.close();

  alert(newWindow.closed); // true

};

SCROLLING AND RESIZING 

There are methods to move/resize a window:

win.moveBy(x,y)

Move the window relative to current position x pixels to the right and y pixels down. Negative values are allowed (to move left/up).

win.moveTo(x,y)

Move the window to coordinates (x,y) on the screen.

win.resizeBy(width,height)

Resize the window by given width/height relative to the current size. Negative values are allowed.

win.resizeTo(width,height)

Resize the window to the given size.

There’s also window.onresize event.

Only popups
To prevent abuse, the browser usually blocks these methods. They only work reliably on popups that we opened, that have no additional tabs.

No minification/maximization
JavaScript has no way to minify or maximize a window. These OS-level functions are hidden from Frontend-developers.

Move/resize methods do not work for maximized/minimized windows.

SCROLLING A WINDOW

You can scroll a window in JavaScript using the window.scrollTo() method or by manipulating the scrollTop and scrollLeft properties of the window's document or an element within it.

win.scrollBy(x,y)

Scroll the window x pixels right and y down relative the current scroll. Negative values are allowed.

win.scrollTo(x,y)

Scroll the window to the given coordinates (x,y).

elem.scrollIntoView(top = true)

Scroll the window to make elem show up at the top (the default) or at the bottom for elem.scrollIntoView(false).

There’s also window.onscroll event.

Focus/Blur on a window

Theoretically, there are window.focus() and window.blur() methods to focus/unfocus on a window. Also there are focus/blur events that allow to focus a window and catch the moment when the visitor switches elsewhere.

In the past evil pages abused those. For instance, look at this code:

window.onblur = () => window.focus();

When a user attempts to switch out of the window (blur), it brings it back to focus. The intention is to “lock” the user within the window.

So, there are limitations that forbid the code like that. There are many limitations to protect the user from ads and evils pages. They depend on the browser.

For instance, a mobile browser usually ignores that call completely. Also focusing doesn’t work when a popup opens in a separate tab rather than a new window.

Still, there are some things that can be done.

For instance:

When we open a popup, it’s might be a good idea to run a newWindow.focus() on it. Just in case, for some OS/browser combinations it ensures that the user is in the new window now.
If we want to track when a visitor actually uses our web-app, we can track window.onfocus/onblur. That allows us to suspend/resume in-page activities, animations etc. But please note that the blur event means that the visitor switched out from the window, but they still may observe it. The window is in the background, but still may be visible.

Coding Popups

Creating popups in web development can be done using a variety of techniques, including HTML, CSS, and JavaScript.

MY VIEWS ON THE DAY

Today we started with the new Module Intermediate JavaScript.

I have covered the following:
- Popups and windows
- Window.open
- Settings for params
- Windows features
- A minimalistic window
- Accessing popup from window
- Accessing window from popup
- Closing a Popup
- Scrolling and resizing
- Scrolling a window
- Focus/Blur on a window 
- Coding popup

JAVASCRIPT INTERMEDIATE
WEEK 1
DAY 2: CROSS WINDOW COMMUNICATION
-	I started my day with updating my padlet
-	I started with day 2 of week 1

SAME ORIGIN 

Two URLs are said to have the “same origin” if they have the same protocol, domain, and port.

These URLs all share the same origin:

http://site.com
http://site.com/
http://site.com/my/page.html
These ones do not:

http://www.site.com (another domain: www.matters)
http://site.org (another domain: .orgmatters)
https://site.com (another protocol: https)
http://site.com:8080 (another port: 8080)
The “Same Origin” policy states that:

if we have a reference to another window, e.g. a popup created by window.open or a window inside <iframe>, and that window comes from the same origin, then we have full access to that window.

otherwise, if it comes from another origin, then we can’t access the content of that window: variables, document, anything. The only exception is location: we can change it (thus redirecting the user). But we cannot read the location (so we can’t see where the user is now, no information leak).

IN ACTION: IFRAME

An iframe (inline frame) is an HTML element that allows you to embed another HTML document within the current document. It's commonly used to display external content or a different webpage within a specific section of your web page.

Windows on subdomains: document.domain

By definition, two URLs with different domains have different origins.

But if windows share the same second-level domain, for instance, john.site.com, peter.site.com, and site.com (so that their common second-level domain is site.com), we can make the browser ignore that difference, so that they can be treated as coming from the “same origin” for the purposes of cross-window communication.

To make it work, each such window should run the code:

document.domain = 'site.com';

That’s all. Now they can interact without limitations. Again, that’s only possible for pages with the same second-level domain.

Iframe: wrong document pitfall

The "Wrong Document" error often occurs when trying to manipulate elements within an iframe. This error happens because JavaScript code running in the parent document attempts to access or modify elements inside the iframe as if they were part of the parent document's DOM. However, the iframe's content is in a separate document, and direct access from the parent document is restricted due to security reasons.

To avoid the "Wrong Document" pitfall and interact with elements inside an iframe correctly, you can follow these steps:

Access the iframe element:
First, select the iframe element within the parent document. You can do this using JavaScript's querySelector or getElementById methods, depending on how you've structured your HTML.

javascript

const iframe = document.querySelector('iframe'); // Or use getElementById if the iframe has an ID attribute
Wait for the iframe to load:
To ensure that the iframe's content is fully loaded and accessible, attach an event listener to the iframe's load event. This event is triggered when the iframe's content is loaded and ready for interaction.

javascript

iframe.addEventListener('load', () => {
    // Code to interact with iframe content goes here
});
Access elements within the iframe:
Inside the load event listener, you can access the document of the iframe using the contentDocument or contentWindow.document property. This allows you to interact with elements within the iframe as if you were working with the DOM of the iframe's content document.

javascript

iframe.addEventListener('load', () => {
    const iframeDocument = iframe.contentDocument || iframe.contentWindow.document;

    // Now you can access and manipulate elements within the iframeDocument
    const iframeButton = iframeDocument.getElementById('buttonId');
    iframeButton.addEventListener('click', () => {
        alert('Button inside the iframe was clicked!');
    });
});
By following these steps, you can safely and correctly interact with elements inside an iframe without encountering the "Wrong Document" error. Remember that cross-origin restrictions may apply, and you need permission from the iframe's source if the iframe content is hosted on a different domain to access or modify its contents.
COLLECTION: WINDOWS.FRAMES

An alternative way to get a window object for <iframe>– is to get it from the named collectionwindow.frames:

- By number: window.frames[0] – the window object for the first frame in the document.
- By name: window.frames.iframeName – the window object for the frame withname="iframeName".

An iframe may have other iframes inside. The corresponding window objects form a hierarchy.

Navigation links are:

- window.frames – the collection of “children” windows (for nested frames).
- window.parent – the reference to the “parent” (outer) window.
- window.top – the reference to the topmost parent window.

THE "SANDBOX" IFRAME ATTRIBUTE

The sandbox attribute allows for the exclusion of certain actions inside an <iframe> in order to prevent it from executing untrusted code. It “sandboxes” the iframe by treating it as coming from another origin and/or applying other limitations.

There’s a “default set” of restrictions applied for <iframe sandbox src="...">. But it can be relaxed if we provide a space-separated list of restrictions that should not be applied as a value of the attribute, like this: <iframe sandbox="allow-forms allow-popups">.

In other words, an empty "sandbox" attribute puts the strictest limitations possible, but we can put a space-delimited list of those that we want to lift.

Here’s a list of limitations:

allow-same-origin
By default "sandbox" forces the “different origin” policy for the iframe. In other words, it makes the browser to treat the iframe as coming from another origin, even if its src points to the same site. With all implied restrictions for scripts. This option removes that feature.

allow-top-navigation
Allows the iframe to change parent.location.

allow-forms
Allows to submit forms from iframe.

allow-scripts
Allows to run scripts from the iframe.

allow-popups
Allows to window.open popups from the iframe

CROSS WINDOW MESSAGING

The postMessage interface allows windows to talk to each other no matter which origin they are from.

So, it’s a way around the “Same Origin” policy. It allows a window from john-smith.com to talk to gmail.comand exchange information, but only if they both agree and call corresponding JavaScript functions. That makes it safe for users.

The interface has two parts.

postMessage
The window that wants to send a message calls postMessage method of the receiving window. In other words, if we want to send the message to win, we should call win.postMessage(data, targetOrigin).

Arguments:

data
The data to send. Can be any object, the data is cloned using the “structured cloning algorithm”. IE supports only strings, so we should JSON.stringify complex objects to support that browser.

targetOrigin
Specifies the origin for the target window, so that only a window from the given origin will get the message.

The targetOrigin is a safety measure. Remember, if the target window comes from another origin, we can’t read it’s location in the sender window. So we can’t be sure which site is open in the intended window right now: the user could navigate away, and the sender window has no idea about it.

Specifying targetOrigin ensures that the window only receives the data if it’s still at the right site. Important when the data is sensitive.

onmessage
To receive a message, the target window should have a handler on the message event. It triggers when postMessage is called (and targetOrigin check is successful).

The event object has special properties:

data
The data from postMessage.

origin
The origin of the sender, for instance http://javascript.info.

source
The reference to the sender window. We can immediately source.postMessage(...) back if we want.

To assign that handler, we should use addEventListener, a short syntax window.onmessage does not work.

MY VIEWS ON THE DAY

- The most important about was learning more about iframes.

- All the activities were beneficial because they are assisting on what to put on our Dev Team website.

- Activities were not that tricky they were just guiding on what to put on our project.

DAY 2 REFLECTION:

- Cross window communication.
- Same origin
- In action: iframe
- Windows on subdomain: document.domain
- iframe: wrong document pitfall
- Collection: window.frames
- The "sandbox" iframe attribute
- Cross window messaging
- postMessage 
- Arguments: data, targetOrigin

DAY 3: THE CLICKJACKING ATTACKS
Clickjacking

Clickjacking, also known as a UI (User Interface) redress attack or UI redressing, is a malicious technique where an attacker tricks a user into clicking on something different from what the user perceives, thereby potentially performing actions without the user's knowledge or consent. The attacker usually accomplishes this by overlaying a legitimate UI element with a deceptive one.

Here are some important points about clickjacking attacks:

How It Works:

Attackers create a website or web page containing an iframe or multiple iframes.
They position these iframes in a way that they are invisible or transparent to the user.
The iframes load legitimate websites or web applications in the background.
The attacker's page may contain deceptive elements like buttons or links that are positioned directly over the invisible iframes.
Deceptive Actions:

When users interact with what they perceive as legitimate UI elements (e.g., clicking a button or link), they are actually interacting with the hidden iframes.
This can lead to unintended actions, such as making financial transactions, changing account settings, or posting social media content without the user's consent.
Preventing Clickjacking:

Frame Busting: Website owners can use frame-busting techniques to prevent their sites from being loaded within iframes on other domains. This helps protect against clickjacking attacks.
X-Frame-Options Header: Servers can send an HTTP response header called "X-Frame-Options" to instruct browsers not to render the page in an iframe or to allow it only from specific domains.
Content Security Policy (CSP): Implementing a CSP can help control which sources are allowed to load content in iframes.
JavaScript: Websites can use JavaScript to detect if their page is loaded within an iframe and take appropriate actions, such as redirecting to the main page.
Protection for Users:

Users should be cautious when clicking on unfamiliar or suspicious links.
Modern browsers often have security features to prevent clickjacking, but users should keep their browsers updated.
Real-World Scenarios:

Clickjacking can be used for various malicious purposes, including stealing sensitive information, spreading malware, or tricking users into sharing their social media accounts.
Legitimate Use Cases:

While clickjacking is typically malicious, there are legitimate use cases for UI overlay, such as for accessibility features, lightboxes, or interactive widgets. In these cases, it's important for website owners to implement security measures to prevent misuse.
Clickjacking is a security concern that both website owners and users need to be aware of, and it emphasizes the importance of security measures and best practices in web development to protect against such attacks.

OLD SCHOOL DEFENSES (WEAK)

The oldest defense is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).

That looks like this:

if (top != window) {

  top.location = window.location;

}

That is: if the window finds out that it’s not on top, then it automatically makes itself the top.

This is not a reliable defense, because there are many ways to hack around it. Let’s cover a few.

Blocking top-navigation
We can block the transition caused by changing top.location in beforeunload event handler.

The top page (enclosing one, belonging to the hacker) sets a preventing handler to it, like this:

window.onbeforeunload = function() {

  return false;

};

When the iframe tries to change top.location, the visitor gets a message asking them whether they want to leave.

In most cases the visitor would answer negatively because they don’t know about the iframe – all they can see is the top page, there’s no reason to leave. So top.location won’t change!

Sandbox attribute
One of the things restricted by the sandbox attribute is navigation. A sandboxed iframe may not change top.location.

So we can add the iframe with sandbox="allow-scripts allow-forms". That would relax the restrictions, permitting scripts and forms. But we omit allow-top-navigation so that changing top.location is forbidden.

Here’s the code:

<iframe sandbox="allow-scripts allow-forms" src="facebook.html"></iframe>

There are other ways to work around that simple protection too.

X-FRAME-OPTIONS

The server-side header X-Frame-Options can permit or forbid displaying the page inside a frame.

It must be sent exactly as HTTP-header: the browser will ignore it if found in HTML <meta> tag. So, <meta http-equiv="X-Frame-Options"...> won’t do anything.

The header may have 3 values:

DENY
Never ever show the page inside a frame.

SAMEORIGIN
Allow inside a frame if the parent document comes from the same origin.

ALLOW-FROM domain
Allow inside a frame if the parent document is from the given domain.

For instance, Twitter uses X-Frame-Options: SAMEORIGIN.

Here’s the result:

<iframe src="https://twitter.com"></iframe>

Depending on your browser, the iframe above is either empty or alerting you that the browser won’t permit that page to be navigating in this way.

Showing with disabled functionality
The X-Frame-Options header has a side-effect. Other sites won’t be able to show our page in a frame, even if they have good reasons to do so.

So there are other solutions… For instance, we can “cover” the page with a <div> with styles height: 100%; width: 100%;, so that it will intercept all clicks. That <div> is to be removed if window == top or if we figure out that we don’t need the protection.

SAMESITE COOKIE ATTRIBUTE

The SameSite cookie attribute is a security feature introduced in web browsers to control how cookies are sent with cross-origin requests. It helps mitigate certain types of cross-site request forgery (CSRF) and cross-site scripting (XSS) attacks by restricting when cookies can be sent along with a request. The SameSite attribute can have one of three values: Strict, Lax, or None.

Strict (SameSite=Strict):

Cookies with the SameSite=Strict attribute are only sent in first-party, same-site requests. They are not sent in cross-site requests.
This setting provides the highest level of security and helps prevent CSRF attacks, but it can break some functionality that relies on cross-site requests.
Lax (SameSite=Lax):

Cookies with the SameSite=Lax attribute are sent in first-party requests (i.e., requests originating from the same site), as well as in top-level navigation requests that originate from a link (e.g., when a user clicks a link to go to another site).
However, cookies are not sent in cross-site requests triggered by third-party resources, such as images, scripts, or iframes.
This setting strikes a balance between security and usability.
None (SameSite=None):

Cookies with the SameSite=None attribute are sent with all requests, regardless of their origin.
This setting is often used when you need to enable cookies for cross-origin requests, such as for single sign-on (SSO) or embedding third-party content via iframes.
When setting SameSite=None, you should also set the Secure attribute to ensure that the cookie is only sent over HTTPS connections.

Clickjacking Presentation

Clickjacking is a malicious technique used in web security attacks where an attacker tricks a user into clicking on a visible element on a web page that is different from what the user perceives. This can lead to unintended actions, often without the user's knowledge or consent. Clickjacking is also known as a UI (User Interface) redress attack or UI redressing.

Here's how clickjacking typically works:

Deceptive Overlay: The attacker creates a web page that contains a visible element (e.g., a button, a game, or an enticing link) that the user is likely to click on.

Hidden Content: Beneath this visible element, the attacker places invisible or transparent iframes that load other web pages or applications. These hidden iframes are positioned in a way that aligns with the visible element.

User Interaction: When the user interacts with the visible element (e.g., clicks on it), they are actually clicking on the invisible iframes underneath. Since the user cannot see the hidden content, they may not realize that they are taking actions on a different web page.

Unintended Actions: The attacker can control the content within the hidden iframes to perform actions on behalf of the user. These actions can range from posting social media updates to making financial transactions or changing account settings, depending on the context of the clickjacking attack.

User Unawareness: Because the user sees the visible element and not the hidden iframes, they remain unaware that their actions are being exploited by the attacker.

To protect against clickjacking attacks, web developers and website owners can implement several security measures:

Frame Busting: Implement frame-busting techniques to prevent your website from being embedded within iframes on other domains.

X-Frame-Options Header: Set the "X-Frame-Options" HTTP response header to control how your site can be framed. You can specify whether it should not be framed at all, be allowed from the same origin, or be allowed from specific domains.

Content Security Policy (CSP): Implement a CSP that restricts which sources are allowed to load content in iframes.

JavaScript Protections: Use JavaScript to detect if your page is loaded within an iframe and take appropriate actions, such as redirecting to the main page.

It's crucial for both website owners and users to be aware of the risks associated with clickjacking and take steps to prevent falling victim to or facilitating such attacks. Users should exercise caution when clicking on unfamiliar or suspicious links, and developers should implement best practices to secure their web applications against clickjacking vulnerabilities.


DAY 4: ARRAYBUFFER AND BINARY ARRAY

ArrayBuffer

An ArrayBuffer is a built-in object in JavaScript that represents a fixed-length binary data buffer. It is part of the JavaScript Typed Array specification and is used to work with raw binary data directly. Unlike regular JavaScript arrays, which can hold elements of various data types, an ArrayBuffer can only store binary data.

In web-development, we meet binary data mostly while dealing with files (create, upload, download). Another typical use case is image processing.

That’s all possible in JavaScript, and binary operations are high-performant.

Although, there’s a bit of confusion because there are many classes. To name a few:

ArrayBuffer, Uint8Array, DataView, Blob, File, etc.

Binary data in JavaScript is implemented in a non-standard way, compared to other languages. But when we sort things out, everything becomes fairly simple.

The basic binary object is ArrayBuffer – a reference to a fixed-length contiguous memory area.

We create it like this:

let buffer = new ArrayBuffer(16); // create a buffer of length 16

alert(buffer.byteLength); // 16

This allocates a contiguous memory area of 16 bytes and pre-fills it with zeroes.

ArrayBuffer is not an array of something

Let’s eliminate a possible source of confusion. ArrayBuffer has nothing in common with Array:

It has a fixed length, we can’t increase or decrease it.
It takes exactly that much space in the memory.
To access individual bytes, another “view” object is needed, not buffer[index].
ArrayBuffer is a memory area. What’s stored in it? It has no clue. Just a raw sequence of bytes.

To manipulate an ArrayBuffer, we need to use a “view” object.

A view object does not store anything on its own. It’s the “eyeglasses” that give an interpretation of the bytes stored in the ArrayBuffer.

For instance:

Uint8Array – treats each byte in ArrayBufferas a separate number, with possible values are from 0 to 255 (a byte is 8-bit, so it can hold only that much). Such value is called a “8-bit unsigned integer”.
Uint16Array – treats every 2 bytes as an integer, with possible values from 0 to 65535. That’s called a “16-bit unsigned integer”.
Uint32Array – treats every 4 bytes as an integer, with possible values from 0 to 4294967295. That’s called a “32-bit unsigned integer”.
Float64Array – treats every 8 bytes as a floating point number with possible values from 5.0x10-324to 1.8x10308.
So, the binary data in an ArrayBuffer of 16 bytes can be interpreted as 16 “tiny numbers”, or 8 bigger numbers (2 bytes each), or 4 even bigger (4 bytes each), or 2 floating-point values with high precision (8 bytes each).

ArrayBuffer is the core object, the root of everything, the raw binary data.

But if we’re going to write into it, or iterate over it, basically for almost any operation – we must use a view, e.g:

let buffer = new ArrayBuffer(16); // create a buffer of length 16

let view = new Uint32Array(buffer); // treat buffer as a sequence of 32-bit integers

alert(Uint32Array.BYTES_PER_ELEMENT); // 4 bytes per integer

alert(view.length); // 4, it stores that many integers

alert(view.byteLength); // 16, the size in bytes

// let's write a value

view[0] = 123456;

// iterate over values

for(let num of view) {

  alert(num); // 123456, then 0, 0, 0 (4 values total)

}

TYPEDARRAY

The common term for all these views (Uint8Array, Uint32Array, etc) is TypedArray. They share the same set of methods and properties.

They are much more like regular arrays: have indexes and iterable.

A typed array constructor (be it Int8Array or Float64Array, doesn’t matter) behaves differently depending on argument types.

There are 5 variants of arguments:

new TypedArray(buffer, [byteOffset], [length]);

new TypedArray(object);

new TypedArray(typedArray);

new TypedArray(length);

new TypedArray();

1. If an ArrayBuffer argument is supplied, the view is created over it. We used that syntax already.

Optionally we can provide byteOffset to start from (0 by default) and the length (till the end of the buffer by default), then the view will cover only a part of the buffer.

2. If an Array, or any array-like object is given, it creates a typed array of the same length and copies the content.

We can use it to pre-fill the array with the data:

let arr = new Uint8Array([0, 1, 2, 3]);
alert( arr.length ); // 4, created binary array of the same length
alert( arr[1] ); // 1, filled with 4 bytes (unsigned 8-bit integers) with given values
3. If another TypedArray is supplied, it does the same: creates a typed array of the same length and copies values. Values are converted to the new type in the process, if needed.

let arr16 = new Uint16Array([1, 1000]);
let arr8 = new Uint8Array(arr16);
alert( arr8[0] ); // 1
alert( arr8[1] ); // 232, tried to copy 1000, but can't fit 1000 into 8 bits (explanations below)
4. For a numeric argument length – creates the typed array to contain that many elements. Its byte length will be length multiplied by the number of bytes in a single item TypedArray.BYTES_PER_ELEMENT:

let arr = new Uint16Array(4); // create typed array for 4 integers
alert( Uint16Array.BYTES_PER_ELEMENT ); // 2 bytes per integer
alert( arr.byteLength ); // 8 (size in bytes)
5. Without arguments, creates an zero-length typed array.

We can create a TypedArray directly, without mentioning ArrayBuffer. But a view cannot exist without an underlying ArrayBuffer, so gets created automatically in all these cases except the first one (when provided).

To access the ArrayBuffer, there are properties:

arr.buffer – references the ArrayBuffer.
arr.byteLength – the length of the ArrayBuffer.
So, we can always move from one view to another:

let arr8 = new Uint8Array([0, 1, 2, 3]);
// another view on the same data
let arr16 = new Uint16Array(arr8.buffer);
Here’s the list of typed arrays:

Uint8Array, Uint16Array, Uint32Array – for integer numbers of 8, 16 and 32 bits.
Uint8ClampedArray – for 8-bit integers, “clamps” them on assignment (see below).
Int8Array, Int16Array, Int32Array – for signed integer numbers (can be negative).
Float32Array, Float64Array – for signed floating-point numbers of 32 and 64 bits.
No int8 or similar single-valued types

Please note, despite of the names like Int8Array, there’s no single-value type like int, or int8 in JavaScript.

That’s logical, as Int8Array is not an array of these individual values, but rather a view on ArrayBuffer

OUT-OF-BOUNDS BEHAVIOUR

Out-of-bounds behavior, in the context of programming, refers to what happens when you attempt to access or manipulate data at a memory location or array index that is outside the valid range of memory allocated for that data structure. This behavior is highly dependent on the programming language, the data structure being used, and the memory management system in place.

TYPEDARRAY METHODS

TypedArray has regular Array methods, with notable exceptions.

We can iterate, map, slice, find, reduce, etc.

There are a few things we can’t do though:

No splice – we can’t “delete” a value, because typed arrays are views on a buffer, and these are fixed, contiguous areas of memory. All we can do is to assign a zero.
No concat method.
There are two additional methods:

arr.set(fromArr, [offset]) copies all elements from fromArr to the arr, starting at position offset (0 by default).
arr.subarray([begin, end]) creates a new view of the same type from begin to end (exclusive). That’s similar to slice method (that’s also supported), but doesn’t copy anything – just creates a new view, to operate on the given piece of data.
These methods allow us to copy typed arrays, mix them, create new arrays from existing ones, and so on.

DATAVIEW

DataView is a special super-flexible “untyped” view over ArrayBuffer. It allows accessing the data on any offset in any format.

For typed arrays, the constructor dictates what the format is. The whole array is supposed to be uniform. The i-th number is arr[i].
With DataView we access the data with methods like .getUint8(i) or .getUint16(i). We choose the format at method call time instead of the construction time.
The syntax:

new DataView(buffer, [byteOffset], [byteLength])

buffer – the underlying ArrayBuffer. Unlike typed arrays, DataView doesn’t create a buffer on its own. We need to have it ready.
byteOffset – the starting byte position of the view (by default 0).
byteLength – the byte length of the view (by default till the end of buffer).

CODE PRACTICE

function concatUint8Arrays(arrays) {
  // Calculate the total length of the concatenated array
  let totalLength = 0;
  for (const array of arrays) {
    totalLength += array.length;
  }

  // Create a new Uint8Array with the total length
  const result = new Uint8Array(totalLength);

  // Copy the contents of input arrays into the result array
  let offset = 0;
  for (const array of arrays) {
    result.set(array, offset);
    offset += array.length;
  }

  return result;
}

// Example usage:
const array1 = new Uint8Array([1, 2, 3]);
const array2 = new Uint8Array([4, 5, 6]);
const concatenatedArray = concatUint8Arrays([array1, array2]);

console.log(concatenatedArray); // Outputs: Uint8Array [ 1, 2, 3, 4, 5, 6 ]

DAY 5 ASSESSMENT DAY

We wrote an assessment
and after the assessment i got busy with my portfolio.

JAVASCRIPT INTERMEDIATE
WEEK2: FILES PATTERN AND FLAGS
DAY 1: FILE OBJECTS

FETCH

In JavaScript, the `fetch` API is used for making network requests, typically to retrieve data from a remote server or to send data to a server. It provides a more modern and flexible way to work with HTTP requests compared to older methods like `XMLHttpRequest`. The `fetch` API is promise-based, which makes it suitable for handling asynchronous operations.

Here's how to use the `fetch` API in JavaScript:

1. **Basic Usage**:

   The simplest usage of the `fetch` function involves providing the URL of the resource you want to fetch. It returns a promise that resolves to the `Response` object representing the response to the request.

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       if (!response.ok) {
         throw new Error('Network response was not ok');
       }
       return response.json(); // Parse the response as JSON
     })
     .then(data => {
       // Work with the data
       console.log(data);
     })
     .catch(error => {
       console.error('There was a problem with the fetch operation:', error);
     });
   ```

2. **Handling JSON Data**:

   In the above example, `response.json()` is used to parse the response body as JSON. This is a common practice when dealing with APIs that return JSON data.

3. **Handling Errors**:

   The `fetch` API doesn't throw an error for HTTP error responses (e.g., 404 or 500). You need to check the `response.ok` property or use the `throw` statement as shown in the example to handle such cases.

4. **Setting Request Options**:

   You can customize the request by providing an optional second argument to the `fetch` function. This argument is an object where you can set various options like headers, HTTP method, and request body.

   ```javascript
   fetch('https://api.example.com/data', {
     method: 'POST',
     headers: {
       'Content-Type': 'application/json',
       // Add other headers as needed
     },
     body: JSON.stringify({ key: 'value' }),
   })
     .then(response => response.json())
     .then(data => {
       // Handle the response data
     })
     .catch(error => {
       console.error('Error:', error);
     });
   ```

5. **Async/Await**:

   You can also use async/await syntax to make the code more readable:

   ```javascript
   async function fetchData() {
     try {
       const response = await fetch('https://api.example.com/data');
       if (!response.ok) {
         throw new Error('Network response was not ok');
       }
       const data = await response.json();
       console.log(data);
     } catch (error) {
       console.error('Error:', error);
     }
   }

   fetchData();
   ```

6. **Cross-Origin Requests (CORS)**:

   When making requests to a different origin (domain), you may encounter Cross-Origin Resource Sharing (CORS) restrictions. The server must include appropriate CORS headers to allow your web page to make requests to it.

7. **Working with Headers and Cookies**:

   You can manipulate headers and cookies using the `Headers` and `Request` objects to send custom headers or cookies with your request.

The `fetch` API is powerful and flexible, making it suitable for a wide range of HTTP request scenarios in web development.

JavaScript can send network requests to the server and load new information whenever is needed.

For example, we can:

Submit an order,

Load user information,

Receive latest updates from the server,

· …etc.

…And all of that without reloading the page!

There’s an umbrella term “AJAX” (abbreviated Asynchronous Javascript And Xml) for that. We don’t have to use XML though: the term comes from old times, that’s that word is there.

There are multiple ways to send a network request and get information from the server.

The fetch() method is modern and versatile, so we’ll start with it. It evolved for several years and continues to improve, right now the support is pretty solid among browsers.

The basic syntax is:

let promise = fetch(url, [options])

url – the URL to access.

options – optional parameters: method, headers etc.

The browser starts the request right away and returns a promise.

Getting a response is usually a two-stage process.

First, the promise resolves with an object of the built-in Response class as soon as the server responds with headers.

So we can check HTTP status, to see whether it is successful or not, check headers, but don’t have the body yet.

The promise rejects if the fetch was unable to make HTTP-request, e.g. network problems, or there’s no such site. HTTP-errors, even such as 404 or 500, are considered a normal flow.

We can see them in response properties:

· ok – boolean, true if the HTTP status code is 200-299.

status – HTTP status code.

ACTIVITY 3

Response provides multiple promise-based methods to access the body in various formats:

response.json() – parse the response as JSON object,
response.text() – return the response as text,
response.formData() – return the response as FormData object (form/multipart encoding, explained in the next chapter),
response.blob() – return the response as Blob(binary data with type),
response.arrayBuffer() – return the response as ArrayBuffer (pure binary data),
additionally, response.body is a ReadableStreamobject, it allows to read the body chunk-by-chunk, we’ll see an example later.

But there’s a list of forbidden HTTP headers that we can’t set:

· Accept-Charset, Accept-Encoding

· Access-Control-Request-Headers

· Access-Control-Request-Method

· Connection

· Content-Length

· Cookie, Cookie2

· Date

· DNT

· Expect

· Host

· Keep-Alive

· Origin

· Referer

· TE

· Trailer

· Transfer-Encoding

· Upgrade

· Via

· Proxy-*

· Sec-*

These headers ensure proper and safe HTTP, so they are controlled exclusively by the browser.

POST REQUEST

To make a POST request, or a request with another method, we need to use fetch options:

method – HTTP-method, e.g. POST,
body – one of:
a string (e.g. JSON),
FormData object, to submit the data as form/multipart,
Blob/BufferSource to send binary data,
URLSearchParams, to submit the data in x-www-form-urlencoded encoding, rarely used.

In JavaScript, you can make a POST request using the 'fetch'  API, which allows you to send data to server.

SENDING AN IMAGE

- We can also submit binary data directly using Blob or BufferSource. 
- Sending an image in a POST Request using JavaScript, you can use the 'fetch' API to send the message as part of the request body.

Response properties:

response.status – HTTP code of the response,

response.ok – true is the status is 200-299.

response.headers – Map-like object with HTTP headers.

Methods to get response body:

response.json() – parse the response as JSON object,

response.text() – return the response as text,

response.formData() – return the response as FormData object (form/multipart encoding, see the next chapter),

response.blob() – return the response as Blob(binary data with type),

response.arrayBuffer() – return the response as ArrayBuffer (pure binary data),

Fetch options so far:

method – HTTP-method,

headers – an object with request headers (not any header is allowed),

body – string, FormData, BufferSource, Blob or UrlSearchParams object to send.

ACTIVITY 4: FETCH USERS FROM GITHUB

To fetch users from GitHub using JavaScript, you can make a GET request to the GitHub API. The GitHub API provides endpoints for retrieving information about users, repositories, and more. Here's an example of how to fetch users from GitHub using the `fetch` API:

```javascript
// Define the GitHub API endpoint for searching users
const apiUrl = 'https://api.github.com/search/users';

// Define the query parameters for the search (e.g., searching for users with the username "example")
const queryParams = {
  q: 'example', // Replace 'example' with your desired search query
};

// Build the URL with query parameters
const url = new URL(apiUrl);
url.search = new URLSearchParams(queryParams);

// Make a GET request to the GitHub API
fetch(url)
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // Parse the response as JSON
  })
  .then(data => {
    // Handle the response data
    const users = data.items; // An array of user objects
    console.log(users);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this code:

1. You define the GitHub API endpoint for searching users, which is `https://api.github.com/search/users`.

2. You define query parameters using the `queryParams` object. In this example, we are searching for users with the username "example." Replace `'example'` with your desired search query.

3. You use the `URL` and `URLSearchParams` objects to build the URL with the query parameters.

4. You make a GET request to the GitHub API using the `fetch` function, passing in the constructed URL.

5. You handle the response in the promise chain. If the response status is not okay (i.e., it's not in the 200-299 range), an error is thrown. Otherwise, you parse the response as JSON and work with the response data.

Please note that GitHub API requests may require authentication for certain endpoints or to increase your rate limits. If you plan to make many requests or need access to private user data, consider using OAuth tokens or personal access tokens for authentication.


JAVASCRIPT INTERMEDIATE
WEEK 2
DAY 2: FORM DATA
SENDING A SIMPLE FORM

In JavaScript, you can work with form data in several ways. Form data typically refers to the data entered by users in HTML forms. You can access and manipulate this data using JavaScript. Here are some common tasks related to form data in JavaScript:

1. Accessing Form Elements:
   To access form elements, you can use the `document.getElementById()` or `document.querySelector()` methods. Here's an example:

   ```html
   <form id="myForm">
       <input type="text" id="username" name="username" />
       <input type="password" id="password" name="password" />
       <button type="submit">Submit</button>
   </form>

   <script>
       const form = document.getElementById("myForm");
       const usernameInput = document.getElementById("username");
       const passwordInput = document.getElementById("password");

       // You can now work with these form elements
   </script>
   ```

2. Handling Form Submission:
   You can listen for the form's `submit` event and prevent the default action to handle form submission with JavaScript. Here's an example:

   ```html
   <form id="myForm">
       <input type="text" id="username" name="username" />
       <input type="password" id="password" name="password" />
       <button type="submit">Submit</button>
   </form>

   <script>
       const form = document.getElementById("myForm");

       form.addEventListener("submit", function (event) {
           event.preventDefault(); // Prevent the form from submitting
           
           // Access and process form data here
           const username = form.username.value;
           const password = form.password.value;

           // Perform validation or submit data to a server, etc.
       });
   </script>
   ```

3. Getting Form Field Values:
   To access the values entered by the user in form fields, you can use the `.value` property of form elements. For example:

   ```javascript
   const username = usernameInput.value;
   const password = passwordInput.value;
   ```

4. Validating Form Data:
   You can validate the user's input before submitting the form. For example, checking if required fields are filled, validating email addresses, or ensuring that passwords meet certain criteria.

5. Modifying Form Data:
   You can also programmatically set values for form elements using JavaScript. For example, you can set default values or update the form based on user interactions.

6. Sending Form Data to a Server:
   If you want to send the form data to a server, you can use techniques like AJAX requests, the Fetch API, or traditional form submission to handle the data submission.

Remember that when dealing with form data in JavaScript, it's important to validate and sanitize the data on the server-side to ensure security and prevent malicious input.

These are the basic concepts for working with form data in JavaScript. Depending on your specific use case, you may need to perform additional tasks or use libraries like jQuery or frameworks like React for more complex form handling.

FORMDATA METHODS

The FormData object in JavaScript provides several methods to work with form data in an HTML form. These methods allow you to manipulate and retrieve data from form elements. 

We can modify fields in FormData with methods:

formData.append(name, value) – add a form field with the given name and value,
formData.append(name, blob, fileName) – add a field as if it were <input type="file">, the third argument fileName sets file name (not form field name), as it it were a name of the file in user’s filesystem,
formData.delete(name) – remove the field with the given name,
formData.get(name) – get the value of the field with the given name,
formData.has(name) – if there exists a field with the given name, returns true, otherwise false
A form is technically allowed to have many fields with the same name, so multiple calls to append add more same-named fields.

There’s also method set, with the same syntax as append. The difference is that .set removes all fields with the given name, and then appends a new field. So it makes sure there’s only field with such name:

formData.set(name, value),
formData.set(name, blob, fileName).

SENDING A FORM WITH A FILE

Sending a form with a file in JavaScript involves using the `FormData` object to construct the form data, including the file input, and then sending it to a server using the `fetch` API or other methods. Here's a step-by-step guide on how to send a form with a file using JavaScript:

1. Create an HTML form that includes a file input field:

```html
<!DOCTYPE html>
<html>
<head>
    <title>File Upload Form</title>
</head>
<body>
    <form id="fileUploadForm" enctype="multipart/form-data">
        <label for="file">Choose a file:</label>
        <input type="file" id="file" name="file" required><br><br>
        
        <button type="submit">Upload</button>
    </form>

    <script src="script.js"></script>
</body>
</html>
```

2. Create a JavaScript file (e.g., `script.js`) to handle the form submission:

```javascript
document.addEventListener("DOMContentLoaded", function () {
    const form = document.getElementById("fileUploadForm");

    form.addEventListener("submit", function (event) {
        event.preventDefault(); // Prevent the default form submission

        const formData = new FormData(form);

        // You can now send the form data (including the file) to a server using the fetch API
        fetch("your_server_endpoint_here", {
            method: "POST",
            body: formData,
        })
        .then(response => {
            if (!response.ok) {
                throw new Error("Network response was not ok");
            }
            return response.text(); // or response.json() if the server responds with JSON
        })
        .then(data => {
            // Handle the server response here
            console.log("Server response:", data);
        })
        .catch(error => {
            // Handle errors here
            console.error("There was a problem with the fetch operation:", error);
        });
    });
});
```

3. Replace `"your_server_endpoint_here"` with the actual URL where you want to send the form data, including the file. This URL should be the endpoint on your server that handles file uploads.

4. When the user selects a file and submits the form, the JavaScript code will prevent the default form submission, create a `FormData` object containing the form data (including the file), and then use the `fetch` API to send the data to the specified server endpoint.

5. You can handle the server's response within the `.then()` block and implement any further logic needed.

Note that when handling file uploads on the server side, you'll need to configure your server to accept and process file uploads and store them in an appropriate location. The specific server-side implementation may vary depending on your server technology (e.g., Node.js, PHP, Python, etc.).

SENDING A FORM WITH BLOB DATA

You can send a form with Blob data using JavaScript and the `FormData` object. Blobs are often used to represent binary data, such as files. Here's how you can send a form with Blob data:

1. Create an HTML form that includes a file input field and other form elements if needed:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Form with Blob Data</title>
</head>
<body>
    <form id="blobUploadForm">
        <!-- Other form fields -->
        <input type="text" id="textData" name="textData" placeholder="Text Data"><br><br>

        <label for="file">Choose a file:</label>
        <input type="file" id="file" name="file" accept=".txt" required><br><br>
        
        <button type="submit">Upload</button>
    </form>

    <script src="script.js"></script>
</body>
</html>
```

2. Create a JavaScript file (e.g., `script.js`) to handle the form submission:

```javascript
document.addEventListener("DOMContentLoaded", function () {
    const form = document.getElementById("blobUploadForm");

    form.addEventListener("submit", function (event) {
        event.preventDefault(); // Prevent the default form submission

        const textData = document.getElementById("textData").value;

        const fileInput = document.getElementById("file");
        const file = fileInput.files[0]; // Get the selected file

        if (!file) {
            alert("Please select a file.");
            return;
        }

        // Create a FormData object and append the Blob data
        const formData = new FormData();
        formData.append("textData", textData);
        formData.append("file", file);

        // You can now send the form data (including the Blob data) to a server using the fetch API
        fetch("your_server_endpoint_here", {
            method: "POST",
            body: formData,
        })
        .then(response => {
            if (!response.ok) {
                throw new Error("Network response was not ok");
            }
            return response.text(); // or response.json() if the server responds with JSON
        })
        .then(data => {
            // Handle the server response here
            console.log("Server response:", data);
        })
        .catch(error => {
            // Handle errors here
            console.error("There was a problem with the fetch operation:", error);
        });
    });
});
```

3. Replace `"your_server_endpoint_here"` with the actual URL where you want to send the form data, including the Blob data. This URL should be the endpoint on your server that handles the form submission.

4. When the user selects a file and submits the form, the JavaScript code will prevent the default form submission, retrieve the text data and Blob data, create a `FormData` object, and then use the `fetch` API to send the data to the specified server endpoint.

5. You can handle the server's response within the `.then()` block and implement any further logic needed.

This example demonstrates how to send a form with Blob data, including a text field and a file input. The server-side implementation should handle both the text data and the Blob data appropriately.

FETCH: DOWNLOAD PROGRESS

To track the download progress of a file fetched using the `fetch` API in JavaScript, you can use the `response.body` and the `ReadableStream` interface. You can monitor the progress by reading chunks of data and calculating the total bytes received.
The fetch method allows to track download progress.

Please note: there’s currently no way for fetch to track upload progress. For that purpose, please use XMLHttpRequest, we’ll cover it later.

To track download progress, we can use response.body property. It’s a “readable stream” – a special object that provides body chunk-by-chunk, as it comes.

Unlike response.text(), response.json() and other methods, response.body gives full control over the reading process, and we can count how much is consumed at any moment.
The result of await reader.read() call is an object with two properties:

done – true when the reading is complete.
value – a typed array of bytes: Uint8Array.
We wait for more chunks in the loop, until done is true.


 Here's an example of how to do this:

```javascript
const url = 'https://example.com/yourfile.zip'; // Replace with the URL of the file you want to download

fetch(url)
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    
    // Get the content length from the response headers
    const contentLength = response.headers.get('content-length');
    const total = parseInt(contentLength, 10);

    // Initialize variables to track progress
    let received = 0;

    // Create a new ReadableStream to read the response body
    const reader = response.body.getReader();

    // Define a function to recursively read chunks of data
    function readChunk() {
      reader.read().then(({ done, value }) => {
        if (done) {
          // All data has been received
          console.log('Download complete!');
        } else {
          // Update progress
          received += value.byteLength;
          const percentage = (received / total) * 100;
          console.log(`Downloaded ${received} bytes (${percentage.toFixed(2)}%)`);

          // Continue reading the next chunk
          readChunk();
        }
      }).catch(error => {
        console.error('Error reading data:', error);
      });
    }

    // Start reading the chunks
    readChunk();
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

In this example:

1. We initiate a `fetch` request to download the file from the specified URL.

2. We check if the response status is OK. If not, we handle the error accordingly.

3. We retrieve the `content-length` header from the response to determine the total size of the file.

4. We set up variables to keep track of the bytes received and create a `ReadableStream` using `response.body.getReader()`.

5. We define a `readChunk` function that reads a chunk of data from the stream. When a chunk is received, we update the progress and continue reading the next chunk until all data has been received.

6. We start reading the chunks by calling `readChunk()`.

This code will log the progress of the file download as it happens. You can modify it to suit your needs, such as displaying the progress to the user or taking other actions when the download is complete.

FETCH: ABORT

You can use the `AbortController` and `AbortSignal` to cancel a fetch request in JavaScript. This allows you to stop a fetch operation before it completes, which can be useful in scenarios where the user decides to cancel the request or in response to some other event. Here's how you can use it:

```javascript
// Create an AbortController
const abortController = new AbortController();

// Get the AbortSignal from the AbortController
const abortSignal = abortController.signal;

// Create a fetch request with the AbortSignal
const url = 'https://example.com/api/data';
const options = {
  method: 'GET',
  signal: abortSignal,
};

// Perform the fetch request
const fetchPromise = fetch(url, options);

// Add an event listener to a cancel button or some other event
const cancelButton = document.getElementById('cancelButton');
if (cancelButton) {
  cancelButton.addEventListener('click', () => {
    // Call the abort method on the AbortController to cancel the request
    abortController.abort();
  });
}

// Handle the fetch request response
fetchPromise
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  })
  .then(data => {
    // Process the fetched data
    console.log(data);
  })
  .catch(error => {
    if (error.name === 'AbortError') {
      console.log('Fetch was aborted by the user or some event.');
    } else {
      console.error('Fetch error:', error);
    }
  });
```

In this example:

1. We create an `AbortController` and obtain the associated `AbortSignal` from it.

2. We use the `AbortSignal` by passing it as the `signal` property in the `fetch` options.

3. We start the fetch request, and it will be associated with the `AbortController`.

4. We add an event listener to a cancel button or some other event. When this event is triggered, we call the `abort()` method on the `AbortController`, which cancels the fetch request.

5. We handle the fetch request as usual, but we also handle the potential `AbortError` that may occur if the request is aborted.

By using the `AbortController`, you can gracefully cancel fetch requests, which is particularly useful in scenarios where you want to provide users with the ability to cancel long-running operations or handle specific events that require the request to be stopped.


JAVASCRIPT INTERMEDIATE
WEEK 2
DAY 3:FETCH: CROSS ORIGIN REQUEST
FETCH: CROSS-ORIGIN REQUESTS

If we make a fetch from an arbitrary web-site, that will probably fail.

The core concept here is origin – a domain/port/protocol triplet.

Cross-origin requests – those sent to another domain (even a subdomain) or protocol or port – require special headers from the remote side. That policy is called “CORS”: Cross-Origin Resource Sharing.

For instance, let’s try fetching http://example.com:

try {

  await fetch('http://example.com');

} catch(err) {

  alert(err); // Failed to fetch

}

Fetch fails, as expected.

Why? A brief history
Because cross-origin restrictions protect the internet from evil hackers.

Seriously. Let’s make a very brief historical digression.

For many years a script from one site could not access the content of another site.

That simple, yet powerful rule was a foundation of internet security. E.g. a script from the page hacker.com could not access the user’s mailbox at gmail.com. People felt safe.

JavaScript also did not have any special methods to perform network requests at that time. It was a toy language to decorate a web page.

But web developers demanded more power. A variety of tricks were invented to work around the limitation.


USING FORMS

- Using forms is a fundamental aspect of web development and allows users to input data, which can then be submitted to a server for processing. HTML provides a set of elements and attributes to create forms.

- One way to communicate with another server was to submit a <form> there. People submitted it into <iframe>, just to stay on the current page, like this:

<iframe name="iframe"></iframe>
<form tagert="iframe" method="POST" action="url">
</form>

So, it was possible to make a GET/POST request to another site, even without networking methods. But as it’s forbidden to access the content of an <iframe>from another site, it wasn’t possible to read the response.

As we can see, forms allowed to send data anywhere, but not receive the response. To be precise, there were actually tricks for that (required special scripts at both the iframe and the page), but let these dinosaurs rest in peace.

SIMPLE REQUEST

There are two types of cross-domain requests:

Simple requests.

All the others.

Simple Requests are, well, simpler to make, so let’s start with them.

A simple request is a request that satisfies two conditions:

Simple method: GET, POST or HEAD

Simple headers – the only allowed custom headers are:

Accept,
Accept-Language,
Content-Language,
Content-Type with the value application/x-www-form-urlencoded, multipart/form-data or text/plain.

Any other request is considered “non-simple”. For instance, a request with PUT method or with an API-Key HTTP-header does not fit the limitations.

The essential difference is that a “simple request” can be made with a <form> or a <script>, without any special methods.

So, even a very old server should be ready to accept a simple request.

Contrary to that, requests with non-standard headers or e.g. method DELETE can’t be created this way. For a long time, JavaScript was unable to do such requests. So an old server may assume that such requests come from a privileged source, “because a webpage is unable to send them”.

When we try to make a non-simple request, the browser sends a special “preflight” request that asks the server – does it agree to accept such cross-origin requests, or not?

And, unless the server explicitly confirms that with headers, a non-simple request is not sent.

Now we’ll go into details. All of them serve a single purpose – to ensure that new cross-origin capabilities are only accessible with explicit permission from the server.

CORS FOR SIMPLE REQUESTS

If a request is cross-origin, the browser always adds Origin header to it.

For instance, if we request https://anywhere.com/request from https://javascript.info/page, the headers will be like:

GET /request
Host: anywhere.com
Origin: https://javascript.info

As you can see, Origin contains exactly the origin (domain/protocol/port), without a path.

The server can inspect the Origin and, if it agrees to accept such a request, adds a special header Access-Control-Allow-Origin to the response. That header should contain the allowed origin (in our case https://javascript.info), or a star *. Then the response is successful, otherwise an error.

The browser plays the role of a trusted mediator here:

It ensures that the correct Origin is sent with a cross-domain request.

If checks for correct Access-Control-Allow-Origin in the response, if it is so, then JavaScript access, otherwise forbids with an error.


**RESPONSE HEADERS**

For cross-origin requests, JavaScript has limitations on which response headers it can access by default. These headers are known as "simple response headers" and include:

1. **Cache-Control**
2. **Content-Language**
3. **Content-Type**
4. **Expires**
5. **Last-Modified**
6. **Pragma**

However, there's one notable omission from this list:

- **No Content-Length Header:** JavaScript is not granted access to the `Content-Length` header by default. This header provides the full length of the response content. If you want to track the percentage of progress when downloading something, you need additional permissions to access this header.

To allow JavaScript to access any other response header, the server must explicitly list it in the `Access-Control-Expose-Headers` header. Here's an example:

```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 12345
API-Key: 2c9de507f2c54aa1
Access-Control-Allow-Origin: https://javascript.info
Access-Control-Expose-Headers: Content-Length, API-Key
```

In this example, the server is allowing the script running on a page from "https://javascript.info" to access the `Content-Length` and `API-Key` headers of the response because they are listed in the `Access-Control-Expose-Headers` header.

Understanding these rules for response headers is important when working with cross-origin requests in JavaScript, especially when dealing with scenarios like tracking download progress or accessing custom headers.


NON-SIMPLE REQUESTS

Non-simple requests, also known as complex requests, refer to HTTP requests that are more intricate and potentially have a greater impact on the server compared to simple requests. These requests do not meet the criteria for simple requests and often involve HTTP methods other than GET, POST, or HEAD or include certain types of custom headers. Handling non-simple requests involves additional considerations, particularly with regards to Cross-Origin Resource Sharing (CORS).

Here are some key characteristics of non-simple requests:

1. **HTTP Methods:** Non-simple requests often use HTTP methods other than GET, POST, or HEAD. Methods such as PUT, DELETE, PATCH, or custom methods fall into this category.

2. **Custom Headers:** These requests may include custom headers that are not part of the standard set of headers used in simple requests.

3. **Preflight Requests:** Non-simple requests typically trigger preflight requests. Preflight requests are OPTIONS requests sent by the browser to the target server before the actual request. The purpose of the preflight request is to check whether the actual request from the specified origin is permitted by the server.

4. **CORS Configuration:** To handle non-simple requests, the server must be configured to respond to preflight requests and include the appropriate CORS headers in the response. This includes headers like `Access-Control-Allow-Origin`, `Access-Control-Allow-Methods`, and `Access-Control-Allow-Headers`.

5. **Credentials:** If the non-simple request includes credentials, such as cookies or HTTP authentication, the server must be configured to handle credentials by including `Access-Control-Allow-Credentials: true` in the CORS headers.

6. **Error Handling:** Proper error handling is crucial when dealing with non-simple requests, as they can have a more significant impact on the server. Servers should provide informative error responses and handle exceptions gracefully.

Here's an example of a preflight request and a corresponding actual request for a non-simple request:

**Preflight (OPTIONS) Request:**

```http
OPTIONS /api/resource HTTP/1.1
Host: example.com
Origin: https://clientwebsite.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: X-Custom-Header
```

**Actual (PUT) Request:**

```http
PUT /api/resource HTTP/1.1
Host: example.com
Origin: https://clientwebsite.com
Content-Type: application/json
X-Custom-Header: custom-value

{"data": "updated"}
```

In this example, the preflight request is sent to check if the PUT request with custom headers is allowed. If the server responds with the appropriate CORS headers, the actual request is sent.

Handling non-simple requests correctly is crucial for securing web applications and ensuring that cross-origin interactions do not pose security risks or unintentional side effects on the server. Servers must be configured to support CORS and respond appropriately to preflight requests.


CREDENTIALS

In JavaScript, credentials are typically used in the context of making network requests, particularly when using the Fetch API or XMLHttpRequest to interact with web services or APIs that require authentication. Credentials are used to specify how cookies, HTTP authentication, and other user credentials are included with the request.

There are three possible values for the `credentials` property when making a fetch request:

1. `"same-origin"` (default): This setting sends credentials if the request is made to the same origin as the requesting page. It includes cookies and HTTP authentication headers if applicable.

```javascript
fetch('https://example.com/api/data', {
  credentials: 'same-origin',
  // other options
})
```

2. `"include"`: This setting always sends credentials, regardless of the origin. It includes cookies and HTTP authentication headers with the request.

```javascript
fetch('https://example.com/api/data', {
  credentials: 'include',
  // other options
})
```

3. `"omit"`: This setting never sends credentials with the request, even if it's a same-origin request.

```javascript
fetch('https://example.com/api/data', {
  credentials: 'omit',
  // other options
})
```

These credentials settings are important for security and privacy reasons. By default, JavaScript fetch requests are subject to the same-origin policy, which means that they can only access resources on the same domain unless the server explicitly allows cross-origin requests (using CORS headers). The `credentials` property gives you control over whether to include authentication information with cross-origin requests or not.

Remember to use these options responsibly, especially when dealing with sensitive user data or authentication. Always follow best practices for web security when working with credentials in JavaScript.


FETCH API

The Fetch API is a modern JavaScript interface for making network requests (HTTP requests) in web applications. It provides a more powerful and flexible way to interact with web resources compared to the older XMLHttpRequest.

Here's an overview of how to use the Fetch API:

1. **Making a Simple GET Request:**

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       if (!response.ok) {
         throw new Error('Network response was not ok');
       }
       return response.json(); // Parse the response body as JSON
     })
     .then(data => {
       // Use the data from the response
       console.log(data);
     })
     .catch(error => {
       // Handle errors
       console.error('Fetch error:', error);
     });
   ```

   In this example, we use `fetch` to send a GET request to a URL. It returns a Promise that resolves to the Response object. We check if the response is OK (status code 200-299) and then parse the response body as JSON.

2. **Making Other Types of Requests (POST, PUT, DELETE, etc.):**

   You can specify the HTTP method and include request headers and a request body as needed when making non-GET requests:

   ```javascript
   fetch('https://api.example.com/resource', {
     method: 'POST', // or 'PUT', 'DELETE', etc.
     headers: {
       'Content-Type': 'application/json',
       // Other headers as needed
     },
     body: JSON.stringify({ key: 'value' }) // Request body data
   })
     .then(/* Handle the response as before */)
     .catch(/* Handle errors */);
   ```

3. **Handling Responses:**

   You can use methods like `json()`, `text()`, or `blob()` on the Response object to parse the response body in different formats:

   ```javascript
   fetch('https://api.example.com/text')
     .then(response => response.text()) // Parse response as text
     .then(text => {
       console.log(text);
     });
   ```

4. **Handling Errors:**

   Use `.catch()` to handle any network errors or exceptions that occur during the fetch operation.

5. **Advanced Configuration:**

   Fetch allows you to configure various options, such as setting request headers, specifying credentials, and more. You can include these options in the second argument to `fetch`.

6. **Async/Await Syntax:**

   You can use `async` and `await` to write asynchronous code that looks more synchronous:

   ```javascript
   async function fetchData() {
     try {
       const response = await fetch('https://api.example.com/data');
       if (!response.ok) {
         throw new Error('Network response was not ok');
       }
       const data = await response.json();
       console.log(data);
     } catch (error) {
       console.error('Fetch error:', error);
     }
   }
   ```

The Fetch API provides a more modern and consistent way to perform network operations in JavaScript, making it easier to work with data from APIs and other web resources.





