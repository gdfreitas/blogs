# Accessibility: Providing feedback on dynamic web apps

Keywords: front-end, a11y, wai-aria, aria-alive

On today's web it is very common to have many dynamic interactions, whether it is a click here that gives feedback there, elements that update by themselves or appear/hide according to a user trigger or a time interval.

Have you ever wondered how users of assistive technologies such as screen readers, who navigate through the keyboard, receive feedback from these actions?

  If you're a frontend developer and you have no idea what a screen reader is, I think the opportunity has come to add it to your toolbox for everyday use. The most common screen readers are: NVDA for Windows users, VoiceOver for MacOSX/iOS users, and Talkback for ChromeOS/Android users.

We could create a huge list of examples, but I'll bring three very common examples to illustrate:

1. Social networks usually have a global notifications component in the header, which updates in real time providing information or communications directed to the user in a timeline format. E.g.: "You received a new friend request" or "A person you follow posted a new post".
2. E-commerces also has a very common global header component to digitally represent a shopping cart, the user browsing the main content of the page can add items to the cart while browsing. E.g.: "Nike Black T-Shirt" *click* "Item added to cart"
5. Toasts are also very common, designed to mimic behavior that originated on mobile devices, usually floating in some corner of the page, often providing feedback directed from the action user's just submitted.

These actions often take place far from the user's current focused element while browsing, so how do we provide this feedback?

## WAI-ARIA

To implement this type of feedback, we can combine the attributes of [WAI-ARIA](http://www.w3.org/TR/wai-aria/) or use some elements that by default already inherit this behavior, they are those with role equal to: log, status, alert, progressbar, marquee, timer.

### aria-live

An element with this attribute indicates that this region will be updated. It also describes the types of updates that user-agents (browsers) and [assistive technologies](https://www.w3.org/TR/wai-aria-1.1/#dfn-assistive-technology) can expect. Learn more on spec: (https://www.w3.org/TR/wai-aria-1.1/#aria-live)

Values:
- `off (default)`: Indicates that updates to the region should not be presented to the user unless the user is currently focused on that region.
- `assertive`: Indicates that updates to the region have the highest priority and should be presented the user immediately.
- `polite`: Indicates that updates to the region should be presented at the next graceful opportunity, such as at the end of speaking the current sentence or when the user pauses typing.

Some other attributes can be used together to provide an even better experience, such as [aria-atomic](https://www.w3.org/TR/wai-aria-1.1/#aria-atomic) and [aria-relevant](https://www.w3.org/TR/wai-aria-1.1/#aria-relevant).

## Basic Example

*Example taken from MDN.*

A clock which updates every 10 seconds, notice it's behaviour using a screen reader.

```html
<div id="clock" role="timer" aria-live="polite" aria-atomic="true">
  <span id="clock-hours">00</span>:<span id="clock-mins">00</span>:<span id="clock-secs">00</span>
</div>

<script>
  const updateClock = () => {
    const now = new Date();
    document.getElementById('clock-hours').innerHTML = now.getHours();
    document.getElementById('clock-mins').innerHTML = ("0" + now.getMinutes()).substr(-2);
    document.getElementById('clock-secs').innerHTML = ("0" + now.getSeconds()).substr(-2);
  }

  updateClock();

  // Updates every 10 seconds
  setInterval(updateClock, 10000);
</script>
```

Have you ever had the opportunity to do something similar? Access the source on GitHub https://github.com/gdfreitas/blogs.

## Resources

- [Accessibility ARIA Live Regions MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions)
