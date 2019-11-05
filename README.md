# "You don't need jQuery" Cheatsheet

**Why another "You don't need jQuery" article?**
* They are too verbose: use of wasteful pharenthesis, new line, semicolon, etc;
  create less concise variable; or even function. Presence of function means they
  don't realize they replace jQuery with "theirOwnQuery" :thumbsdown:. They don't
  realize jQuery is so elegance that they fail to replace it.
* The solution is out of context. jQuery solves problems only by javascript. If
  any solution force you to write CSS (or anykind except javascript), it means it
  fails to replace jQuery.
* They still mention IE :thumbsdown:. Ask your users to throw away IE and use
  newest open source browser, you will be free from pain.

**Credit:**
* https://github.com/nefe/You-Dont-Need-jQuery
* http://youmightnotneedjquery.com/

**How to jump to the point immediately:**
1. press `[CTRL]+[F]`
2. then type `[.]` or `[#]`, then type the keyword, then type `[(]`
3. then press `[ENTER]`

**How to read:**
* This script is designed to be self documented. Rather than written like this:
  ```js
  $(param).attr(attribute); // param is CSS selector, HTMLElement, HTMLElement collection
  ```
  it would be more elegance and natural if it written like this:
  ```js
  $jqList.attr(attribute);
  ```
  You have to interpret it as `$(selector).attr(attribute);` or as
  `$jqList.attr(attribute);` or as `$(elmList).attr(attribute);`

* One unit of solution is defined as a consecutive number of lines and ended
  with blank line. The example of problem below has 3 solutions.
  ```js
  $jqList.attr(attribute);

  document.querySelectorAll(selector)[0].getAttribute(attribute);

  elm.getAttribute(attribute);

  elmList[0].getAttribute(attribute);
  ```
  A problem and its solution(s) is (are) boundaried by `// =====` or by `// -----`.

* If operand appears as hardcoded value (whether it is string, number, boolean,
  or null), than you shoud not change it with any value, otherwise the behaviour /
  output is unpredictable.
  ```js
  elm.addEventListener("click", func); // in this case is "click"
  ```
  If operand appears as variable, than you can change it with any value with
  same type. Confirm it's type at the declaration line (at the topmost).
  ```js
  elm.addEventListener("click", func); // in this case is func
  ```

* If you see ` // TODO` this means i need your help to fill this space.

**Real code reality:**

We know that jQuery instance methods can act as setter and getter. In the solutions
bellow, you will see many getter written like this one `$jqList.attr(attribute);`.
But there is no such thing like that, right?!. The realistic is like this one
`let pocket = $jqList.attr(attribute);` or like this one
`if ($jqList.attr(attribute)) {/* ... */}`. The reason we
write like that kind is to shorten the line, and eliminate all possibility which
can bloat this article.

In other side, we can't avoid the fact that a particular jQuery method has many
variant, and it is very tolerant with it's parameter. We decided not to create a
generic statement for this kind of problem in order to simplify readers to digest
the solution. The con is there is so many duplicate algorithm, but the pro is
readers don't have to care about other statement.

Not like vanilla js which gives you 3 kind of output (a `null`, a particular
single object, or a collection of particular object), jQuery always gives you a
collection. This design, guaranties you to call any instance method of its member
item safely. This situation is not not applicable with vanilla js, you have to
know exactly what type of the output is, and have to make additional condition.
Unless you are sure with what you are dealing with, most solution in this article
are not safe. The exact solutions are like this:
```js
$jqList.attr(attribute);

// unsafety if you are not sure
attr = document.querySelector(selector).getAttribute(attribute);

// safety
pocket = document.querySelector(selector);
if (pocket) {
    attr = pocket.getAttribute(attribute);
}

// unsafety if you are not sure
attr = elm.getAttribute(attribute);

// safety
if (elm) {
    elm.getAttribute(attribute);
}

// unsafety if you are not sure
attr = elmList[0].getAttribute(attribute);

// safety
if (elmList[0]) {
    attr = elmList[0].getAttribute(attribute);
}
```

But if you see `elmList.forEach(/* ... */)`, this is always safety.

<br/>

If you feel disturbed by the code being covered, copy this script, and execute
in console window (note: only effective on width screen):
```js
(() => {
    let mdBody = document.querySelector(".markdown-body");
    let parent = mdBody.parentNode;
    let current = mdBody;
    while(parent) {
        parent.childNodes.forEach(item => {
            let style = item.style;
            if (item == document.body || !style) return;
            style.setProperty('margin', '0px', 'important');
            style.setProperty('padding', '0px', 'important');
            style.setProperty('border', '0px', 'important');
            if (item != current) style.setProperty('display', 'none', 'important');
        });
        current = parent;
        parent = parent.parentNode;
    }
    mdBody.style.width = window.document.documentElement.clientWidth + "px";
    mdBody.style.setProperty('padding', '10px', 'important');
})();
```


<br/><br/>

## Here we are:

```js
/** @type {HTMLElement} */
let elm = document.createElement("div");

/** @type {NodeList} */
let elmList = document.querySelectorAll("div");

/** @type {HTMLElement} */
let otherElm = document.createElement("div");

/** @type {string} */
let standardEventName = "click";

/** @type {string} */
let nonStandardEventName = "any";

/** @type {string} */
let eventName = standardEventName || nonStandardEventName;

/** @type {string} */
let markupString = "<div>hello</div>";

/** @type {string} */
let nonMarkupString = "hello";

/** @type {number} */
let number = 1000;

/** @type {Function} */
let func = function(){};


// =============================================================================
// SIMILAR METHOD: #blur(), #change(), #click(), #contextmenu(), #dblclick(),
// #focus(), #focusin(), #focusout(), #keydown(), #keypress(), #keyup(), #mousedown(),
// #mouseenter(), #mouseleave(), #mousemove(), #mouseout(), #mouseover(), #mouseup(),
// #resize(), #scroll(), #select(), #submit(),

    // ---------------------------------
    // SIGNATURE: .blur(handler)
    $jqList.blur(func);

    elm.addEventListener("blur", func);

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .blur([eventData], handler)
    $jqList.blur({data1: "val1", data2: "val2"}, (event) => {
        console.log(event.data.data1, event.data.data2);
    });

    elm.addEventListener("blur", (event) => {
        const evenData = {data1: "val1", data2: "val2"};
        console.log(evenData.data1, evenData.data2);
    });

    elmList.forEach(elm => {/* same as above */});

    // TODO

    // ---------------------------------
    // SIGNATURE: .blur()
    $jqList.blur();

    elm.dispatchEvent(new Event("blur"));

    elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIMILAR METHOD: #error(), #load((), .unload(()

    // ---------------------------------
    // SIGNATURE: .error(handler)
    $jqList.error(func);

    elm.addEventListener("error", func);

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .error([eventData], handler)
    $jqList.error({data1: "val1", data2: "val2"}, (event) => {
        console.log(event.data.data1, event.data.data2);
    });

    elm.addEventListener("error", (event) => {
        const evenData = {data1: "val1", data2: "val2"};
        console.log(evenData.data1, evenData.data2);
    });

    elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIMILAR METHOD: #hide(), #show()
//
// #hide() : "none"
// #show() : "" | "inline" | "inline-block" | "inline-table" | "block"

    // ---------------------------------
    // SIGNATURE: .hide()
    $jqList.hide();

    elm.style.display = "none";

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .hide([duration], [complete])
    // see: .hide(duration, [easing], [complete])

    // ---------------------------------
    // SIGNATURE: .hide(options)
    $jqList.hide(options);

    elm.style.transition = `all ${options.duration}ms ${options.easing}`;
    elm.style.height = "0px";
    elm.style.width = "0px";
    elm.style.opacity = "0";
    setTimeout(() => {elm.style.transition = ""; options.complete()}, options.duration);

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .hide(duration, [easing], [complete])
    $jqList.hide(duration, easing, complete);

    elm.style.transition = `all ${duration}ms ${easing}`;
    elm.style.height = "0px";
    elm.style.width = "0px";
    elm.style.opacity = "0";
    setTimeout(() => {elm.style.transition = ""; complete()}, duration);

    elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .add(selector)
$jqList.add(elm);

[...elmList].push(elm);

// ---------------------------------
// SIGNATURE: .add(elements)
$jqList.add(elm);

// TODO

// ---------------------------------
// SIGNATURE: .add(html)
$jqList.add(elm);

// TODO

// ---------------------------------
// SIGNATURE: .add(selection)
$jqList.add(elm);

// TODO

// ---------------------------------
// SIGNATURE: .add(selector, context)
$jqList.add(elm);

// TODO


// =============================================================================
// SIGNATURE: .addBack([selector])
$jqList.addBack();

[...elmList].filter((item, idx, self) => idx >= self.indexOf(elm));


// =============================================================================
// SIGNATURE: .addClass(className)
$jqList.addClass(className);

elm.classList.add(className);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .addClass(function)
$jqList.addClass((idx, className) => (idx % 2) ? "odd" : "even");

elmList.forEach((item, idx) => item.classList.add((idx % 2) ? "odd" : "even"));


// =============================================================================
// SIGNATURE: .after(content, [content])
$jqList.after(markupString);

elm.insertAdjacentHTML("afterend", markupString);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .after(function)
$jqList.after(func);

// TODO

// ---------------------------------
// SIGNATURE: .after(function-html)
$jqList.after();

// TODO


// =============================================================================
// SIGNATURE: .ajaxComplete(handler)
$jqList.ajaxComplete(func);

// TODO


// =============================================================================
// SIGNATURE: .ajaxError(handler)
$jqList.ajaxError(func);

// TODO


// =============================================================================
// SIGNATURE: .ajaxSend(handler)
$jqList.ajaxSend(func);

// TODO


// =============================================================================
// SIGNATURE: .ajaxStart(handler)
$jqList.ajaxStart(func);

// TODO


// =============================================================================
// SIGNATURE: .ajaxStop(handler)
$jqList.ajaxStop(func);

// TODO


// =============================================================================
// SIGNATURE: .ajaxSuccess(handler)
$jqList.ajaxSuccess(func);

// TODO


// =============================================================================
// SIGNATURE: .andSelf()
$jqList.andSelf();

// TODO


// =============================================================================
// SIGNATURE: .animate(properties, [duration], [easing], [complete])
$jqList.animate(cssObject, duration, easing, func);

elm.style.transition = `all ${duration} ${easing}`;
Object.keys(cssObject).forEach(key => elm.style[key] = cssObject[key]);
setTimeout(() => {elm.style.transition = ""; func()}, duration);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .animate(properties, options)
$jqList.animate(cssObject, opt);

elm.style.transition = `all ${opt.duration} ${opt.easing}`;
Object.keys(cssObject).forEach(key => elm.style[key] = cssObject[key]);
setTimeout(() => {elm.style.transition = ""; opt.complete()}, opt.duration);

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIMILAR METHOD: #append(), #prepend()

    // ---------------------------------
    // SIGNATURE: .append(content, [content])
    $jqList.append(otherElm || nonMarkupString);

    elm.append(otherElm || nonMarkupString);

    elmList.forEach(elm => elm.append(otherElm.cloneNode(true)));
    otherElm.remove();

    elmList.forEach(elm => elm.append(nonMarkupString));

    // ---------------------------------
    // SIGNATURE: .append(content, [content])
    $jqList.append(markupString);

    elm.append((new Range).createContextualFragment(markupString).firstElementChild);

    newElm = (new Range).createContextualFragment(markupString).firstElementChild;
    elmList.forEach(elm => elm.append(newElm.cloneNode(true)));

    // ---------------------------------
    // SIGNATURE: .append(content, [content])
    $jqList.append(otherElm1, otherElm2, otherElm3 /* and any another params */);

    [otherElm1, otherElm2, otherElm3 /* and any another params */].forEach(item => elm.append(item));

    [otherElm1, otherElm2, otherElm3 /* and any another params */]
        .forEach(item1 => elmList.forEach(item2 => item2.append(item1.cloneNode(true))))
        .forEach(item => item.remove());

    // ---------------------------------
    // SIGNATURE: .append(content, [content])
    $jqList.append(markupString1, markupString2, markupString3 /* and any another params */);

    [markupString1, markupString2, markupString3 /* and any another params */]
        .map(item => (new Range).createContextualFragment(item).firstElementChild)
        .forEach(item => elm.append(item));

    [markupString1, markupString2, markupString3 /* and any another params */]
        .map(item => (new Range).createContextualFragment(item).firstElementChild)
        .forEach(item1 => elmList.forEach(item2 => item2.append(item1.cloneNode(true))));

    // ---------------------------------
    // SIGNATURE: .append(function)
    $jqList.append(func);

    // TODO


// =============================================================================
// SIGNATURE: .appendTo(target)
$jqList.appendTo(otherElm);

otherElm.appendChild(elm);


// =============================================================================
// SIGNATURE: .attr(attributeName)
$jqList.attr("placeholder");

elm.getAttribute("placeholder");

elmList[0].getAttribute("placeholder");

// ---------------------------------
// SIGNATURE: .attr(attributeName, value)
$jqList.attr(attributeName, nonMarkupString);

elm.setAttribute(attributeName, nonMarkupString);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .attr(attributes)
$jqList.attr();

// TODO

// ---------------------------------
// SIGNATURE: .attr(attributeName, function)
$jqList.attr();

// TODO


// =============================================================================
// SIGNATURE: .before(content, [content])
$jqList.before(markupString);

elm.insertAdjacentHTML("beforebegin", markupString);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .before(function)
$jqList.before(func);

// TODO

// ---------------------------------
// SIGNATURE: .before(function-html)
$jqList.before();

// TODO


// =============================================================================
// SIGNATURE: .bind(eventType, [eventData], handler)
$jqList.bind(eventName, func);

elm.addEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .bind(eventType, [eventData], [preventBubble])
$jqList.bind();

// TODO

// ---------------------------------
// SIGNATURE: .bind(events)
$jqList.bind();

// TODO


// =============================================================================
// SIGNATURE: .children([selector])
$jqList.children();

elm.children;


// =============================================================================
// SIGNATURE: .clearQueue([queueName])
$jqList.clearQueue();

// TODO


// =============================================================================
// SIGNATURE: .clone([withDataAndEvents])
$jqList.clone();

// TODO

// ---------------------------------
// SIGNATURE: .clone([withDataAndEvents], [deepWithDataAndEvents])
$jqList.clone();

// TODO


// =============================================================================
// SIGNATURE: .closest(selector)
$jqList.closest();

// TODO

// ---------------------------------
// SIGNATURE: .closest(selector, [context])
$jqList.closest();

// TODO

// ---------------------------------
// SIGNATURE: .closest(selection)
$jqList.closest();

// TODO

// ---------------------------------
// SIGNATURE: .closest(element)
$jqList.closest();

// TODO

// ---------------------------------
// SIGNATURE: .closest(selectors, [context])
$jqList.closest();

// TODO


// =============================================================================
// SIGNATURE: .contents()
$jqList.contents();

// TODO


// =============================================================================
// SIGNATURE: .css(propertyName)
$jqList.css();

// TODO

// ---------------------------------
// SIGNATURE: .css(propertyNames)
$jqList.css();

// TODO

// ---------------------------------
// SIGNATURE: .css(propertyName, value)
$jqList.css("border-width", "20px");

elm.style.borderWidth = "20px";

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .css(propertyName, function)
$jqList.css();

// TODO


// =============================================================================
// SIGNATURE: .data(key, value)
$jqList.data();

// TODO

// ---------------------------------
// SIGNATURE: .data(obj)
$jqList.data();

// TODO

// ---------------------------------
// SIGNATURE: .data(key)
$jqList.data();

// TODO

// ---------------------------------
// SIGNATURE: .data()
$jqList.data();

// TODO


// =============================================================================
// SIGNATURE: .delay(duration, [queueName])
$jqList.delay();

// TODO


// =============================================================================
// SIGNATURE: .delegate(selector, eventType, handler)
$jqList.delegate();

// TODO

// ---------------------------------
// SIGNATURE: .delegate(selector, eventType, eventData, handler)
$jqList.delegate();

// TODO

// ---------------------------------
// SIGNATURE: .delegate(selector, events)
$jqList.delegate();

// TODO


// =============================================================================
// SIGNATURE: .dequeue([queueName])
$jqList.dequeue();

// TODO


// =============================================================================
// SIGNATURE: .detach([selector])
$jqList.detach();

// TODO


// =============================================================================
// SIGNATURE: .die()
$jqList.die();

elm.parentNode.replaceChild(elm.cloneNode(true), elm);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .die(eventType, [handler])
$jqList.die(eventName, func);

elm.removeEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .die(events)
$jqList.die();

// TODO


// =============================================================================
// SIGNATURE: .each(function)
$jqList.each(func);

// TODO


// =============================================================================
// SIGNATURE: .empty()
$jqList.empty();

// TODO


// =============================================================================
// SIGNATURE: .end()
$jqList.end();

// TODO


// =============================================================================
// SIGNATURE: .eq(index)
$jqList.eq();

// TODO

// ---------------------------------
// SIGNATURE: .eq(indexFromEnd)
$jqList.eq();

// TODO


// =============================================================================
// SIGNATURE: .fadeIn([duration], [complete])
$jqList.fadeIn();

elm.style.transition = `opacity ${number}ms`;
elm.style.display = "block";
setTimeout(() => {elm.style.opacity = "1"; setTimeout(() => elm.style.transition = "", 1)}, number);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .fadeIn(options)
$jqList.fadeIn();

// TODO

// ---------------------------------
// SIGNATURE: .fadeIn([duration], [easing], [complete])
$jqList.fadeIn();

// TODO


// =============================================================================
// SIGNATURE: .fadeOut([duration], [complete])
$jqList.fadeOut();

elm.style.transition = `opacity 1000ms`;
elm.style.opacity = "0";
setTimeout(() => {elm.style.display = "none"; setTimeout(() => elm.style.transition = "", 1)}, 1000);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .fadeOut(options)
$jqList.fadeOut();

// TODO

// ---------------------------------
// SIGNATURE: .fadeOut([duration], [easing], [complete])
$jqList.fadeOut();

// TODO


// =============================================================================
// SIGNATURE: .fadeTo(duration, opacity, [complete])
$jqList.fadeTo();

// TODO

// ---------------------------------
// SIGNATURE: .fadeTo(duration, opacity, [easing], [complete])
$jqList.fadeTo();

// TODO


// =============================================================================
// SIGNATURE: .fadeToggle([duration], [easing], [complete])
$jqList.fadeToggle();

// TODO

// ---------------------------------
// SIGNATURE: .fadeToggle(options)
$jqList.fadeToggle();

// TODO


// =============================================================================
// SIGNATURE: .filter(selector)
$jqList.filter();

// TODO

// ---------------------------------
// SIGNATURE: .filter(function)
$jqList.filter(func);

// TODO

// ---------------------------------
// SIGNATURE: .filter(elements)
$jqList.filter();

// TODO

// ---------------------------------
// SIGNATURE: .filter(selection)
$jqList.filter();

// TODO


// =============================================================================
// SIGNATURE: .find(selector)
$jqList.find();

// TODO

// ---------------------------------
// SIGNATURE: .find(element)
$jqList.find();

// TODO


// =============================================================================
// SIGNATURE: .finish([queue])
$jqList.finish();

// TODO


// =============================================================================
// SIGNATURE: .first()
$jqList.first();

// TODO


// =============================================================================
// SIGNATURE: .get(index)
$jqList.get();

// TODO

// ---------------------------------
// SIGNATURE: .get()
$jqList.get();

// TODO


// =============================================================================
// SIGNATURE: .has(selector)
$jqList.has();

// TODO

// ---------------------------------
// SIGNATURE: .has(contained)
$jqList.has();

// TODO


// =============================================================================
// SIGNATURE: .hasClass(className)
$jqList.hasClass();

// TODO


// =============================================================================
// SIGNATURE: .height()
$jqList.height();

parseFloat(getComputedStyle(elm).height);

parseFloat(getComputedStyle(elmList[0]).height);

// ---------------------------------
// SIGNATURE: .height(value)
$jqList.height(number);

elm.style.height = `${number}px`;

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .height(function)
$jqList.height((idx, height) => idx * 5 + height);

elmList.forEach((elm, idx) => elm.style.height = (idx * 5 + height) + 'px');


// =============================================================================
// SIGNATURE: .hover(handlerIn, handlerOut)
$jqList.hover();

// TODO

// ---------------------------------
// SIGNATURE: .hover(handlerInOut)
$jqList.hover();

// TODO


// =============================================================================
// SIGNATURE: .html()
$jqList.html();

// TODO

// ---------------------------------
// SIGNATURE: .html(htmlString)
$jqList.html(markupString);

elm.innerHTML = markupString;

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .html(function)
$jqList.html(func);

// TODO


// =============================================================================
// SIGNATURE: .index()
$jqList.index();

// TODO

// ---------------------------------
// SIGNATURE: .index(selector)
$jqList.index();

// TODO

// ---------------------------------
// SIGNATURE: .index(element)
$jqList.index();

// TODO


// =============================================================================
// SIGNATURE: .innerHeight()
$jqList.innerHeight();

// TODO

// ---------------------------------
// SIGNATURE: .innerHeight(value)
$jqList.innerHeight();

// TODO

// ---------------------------------
// SIGNATURE: .innerHeight(function)
$jqList.innerHeight(func);

// TODO


// =============================================================================
// SIGNATURE: .innerWidth()
$jqList.innerWidth();

// TODO

// ---------------------------------
// SIGNATURE: .innerWidth(value)
$jqList.innerWidth();

// TODO

// ---------------------------------
// SIGNATURE: .innerWidth(function)
$jqList.innerWidth(func);

// TODO


// =============================================================================
// SIGNATURE: .insertAfter(target)
$jqList.insertAfter();

// TODO


// =============================================================================
// SIGNATURE: .insertBefore(target)
$jqList.insertBefore();

// TODO


// =============================================================================
// SIGNATURE: .is(selector)
$jqList.is();

// TODO

// ---------------------------------
// SIGNATURE: .is(function)
$jqList.is(func);

// TODO

// ---------------------------------
// SIGNATURE: .is(selection)
$jqList.is();

// TODO

// ---------------------------------
// SIGNATURE: .is(elements)
$jqList.is();

// TODO


// =============================================================================
// SIGNATURE: .last()
$jqList.last();

// TODO


// =============================================================================
// SIGNATURE: .live(events, handler)
$jqList.live(eventName, func);

elm.addEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .live(events, [data], handler)
$jqList.live();

// TODO

// ---------------------------------
// SIGNATURE: .live(events)
$jqList.live();

// TODO


// =============================================================================
// SIGNATURE: .load(url, [data], [complete])
$jqList.load();

// TODO


// =============================================================================
// SIGNATURE: .map(callback)
$jqList.map();

// TODO


// =============================================================================
// SIGNATURE: .next([selector])
$jqList.next();

elm.nextElementSibling;

// ---------------------------------
// SIGNATURE: .next([selector])
$jqList.next(selector);

[...elm.parentNode.children].reduce((acc, item, idx, self) => (!acc && idx > self.indexOf(elm) && item.matches(selector)) ? item : acc, null);


// =============================================================================
// SIGNATURE: .nextAll([selector])
$jqList.nextAll();

[...elm.parentNode.children].filter((item, idx, self) => idx > self.indexOf(elm));


// =============================================================================
// SIGNATURE: .nextUntil([selector], [filter])
$jqList.nextUntil(selector);

const children = elm.parentNode.children;
const boundary = Array.prototype.reduce.call(children, (acc, item, idx) => item.matches(selector) ? idx : acc, NaN);
[...children].filter((item, idx, self) => idx > self.indexOf(elm) && boundary > self.indexOf(item));

// ---------------------------------
// SIGNATURE: .nextUntil([selector], [filter])
$jqList.nextUntil(selector1, selector2);

const children = elm.parentNode.children;
const boundary = Array.prototype.reduce.call(children, (acc, item, idx) => item.matches(selector1) ? idx : acc, NaN);
[...children].filter((item, idx, self) => idx > self.indexOf(elm) && boundary > self.indexOf(item) && item.matches(selector2));

// ---------------------------------
// SIGNATURE: .nextUntil([element], [filter])
$jqList.nextUntil();

// TODO


// =============================================================================
// SIGNATURE: .not(selector)
$jqList.not();

// TODO

// ---------------------------------
// SIGNATURE: .not(function)
$jqList.not(func);

// TODO

// ---------------------------------
// SIGNATURE: .not(selection)
$jqList.not();

// TODO


// =============================================================================
// SIGNATURE: .off(events, [selector], [handler])
$jqList.off(eventName, func);

elm.removeEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .off(events, [selector])
$jqList.off();

// TODO

// ---------------------------------
// SIGNATURE: .off(event)
$jqList.off();

// TODO

// ---------------------------------
// SIGNATURE: .off()
$jqList.off();

elm.parentNode.replaceChild(elm.cloneNode(true), elm);

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .offset()
$jqList.offset();

// TODO

// ---------------------------------
// SIGNATURE: .offset(coordinates)
$jqList.offset();

// TODO

// ---------------------------------
// SIGNATURE: .offset(function)
$jqList.offset(func);

// TODO


// =============================================================================
// SIGNATURE: .offsetParent()
$jqList.offsetParent();

// TODO


// =============================================================================
// SIGNATURE: .on(events, [selector], [data], handler)
$jqList.on(eventName, func);

elm.addEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .on(events, [selector], [data])
$jqList.on();

// TODO


// =============================================================================
// SIGNATURE: .one(events, [data], handler)
$jqList.one(eventName, func);

// TODO

// ---------------------------------
// SIGNATURE: .one(events, [selector], [data], handler)
$jqList.one(eventName, func);

// TODO

// ---------------------------------
// SIGNATURE: .one(events, [selector], [data])
$jqList.one(eventName, func);

// TODO


// =============================================================================
// SIGNATURE: .outerHeight([includeMargin])
$jqList.outerHeight();

// TODO

// ---------------------------------
// SIGNATURE: .outerHeight(value [includeMargin])
$jqList.outerHeight();

// TODO

// ---------------------------------
// SIGNATURE: .outerHeight(function)
$jqList.outerHeight(func);

// TODO


// =============================================================================
// SIGNATURE: .outerWidth([includeMargin])
$jqList.outerWidth();

// TODO

// ---------------------------------
// SIGNATURE: .outerWidth(value, [includeMargin])
$jqList.outerWidth();

// TODO

// ---------------------------------
// SIGNATURE: .outerWidth(function)
$jqList.outerWidth(func);

// TODO


// =============================================================================
// SIGNATURE: .parent([selector])
$jqList.parent();

// TODO


// =============================================================================
// SIGNATURE: .parents([selector])
$jqList.parents();

// TODO


// =============================================================================
// SIGNATURE: .parentsUntil([selector], [filter])
$jqList.parentsUntil();

// TODO

// ---------------------------------
// SIGNATURE: .parentsUntil([element], [filter])
$jqList.parentsUntil();

// TODO


// =============================================================================
// SIGNATURE: .position()
$jqList.position();

// TODO


// =============================================================================
// SIGNATURE: .prependTo(target)
$jqList.prependTo();

// TODO


// =============================================================================
// SIGNATURE: .prev([selector])
$jqList.prev();

el.previousElementSibling;

// ---------------------------------
// SIGNATURE: .prev([selector])
$jqList.prev(selector);

[...elm.parentNode.children].reduceRight((acc, item, idx, self) => (!acc && idx < self.indexOf(elm) && item.matches(selector)) ? item : acc, null);


// =============================================================================
// SIGNATURE: .prevAll([selector])
$jqList.prevAll();

[...elm.parentNode.children].filter((item, idx, self) => idx < self.indexOf(elm));


// =============================================================================
// SIGNATURE: .prevUntil([selector], [filter])
$jqList.prevUntil(selector);

const children = elm.parentNode.children;
const boundary = Array.prototype.reduce.call(children, (acc, item, idx) => item.matches(selector) ? idx : acc, NaN);
[...children].filter((item, idx, self) => idx < self.indexOf(elm) && boundary < self.indexOf(item));

// ---------------------------------
// SIGNATURE: .prevUntil([selector], [filter])
$jqList.prevUntil(selector1, selector2);

const children = elm.parentNode.children;
const boundary = Array.prototype.reduce.call(children, (acc, item, idx) => item.matches(selector1) ? idx : acc, NaN);
[...children].filter((item, idx, self) => idx < self.indexOf(elm) && boundary < self.indexOf(item) && item.matches(selector2));

// ---------------------------------
// SIGNATURE: .prevUntil([element], [filter])
$jqList.prevUntil();

// TODO


// =============================================================================
// SIGNATURE: .promise([type], [target])
$jqList.promise();

// TODO


// =============================================================================
// SIGNATURE: .prop(propertyName)
$jqList.prop();

// TODO

// ---------------------------------
// SIGNATURE: .prop(propertyName, value)
$jqList.prop();

// TODO

// ---------------------------------
// SIGNATURE: .prop(properties)
$jqList.prop();

// TODO

// ---------------------------------
// SIGNATURE: .prop(propertyName, function)
$jqList.prop();

// TODO


// =============================================================================
// SIGNATURE: .pushStack(elements)
$jqList.pushStack($otherJqList);

[...elmList, ...otherElmList];

// ---------------------------------
// SIGNATURE: .pushStack(elements, name, arguments)
$jqList.pushStack();

// TODO


// =============================================================================
// SIGNATURE: .queue([queueName])
$jqList.queue();

// TODO

// ---------------------------------
// SIGNATURE: .queue([queueName], newQueue)
$jqList.queue();

// TODO

// ---------------------------------
// SIGNATURE: .queue([queueName], callback)
$jqList.queue();

// TODO


// =============================================================================
// SIGNATURE: .ready(handler)
$jqList.ready(func);

(document.readyState !== "loading") ? func() : document.addEventListener("DOMContentLoaded", func);


// =============================================================================
// SIGNATURE: .remove([selector])
$jqList.remove();

elm.parentNode.removeChild(elm);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .remove([selector])
$jqList.remove(selector);

elm.match(selector) && elm.parentNode.removeChild(elm);

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .removeAttr(attributeName)
$jqList.removeAttr(attrName);

elm.removeAttribute(attrName);

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .removeClass([className])
$jqList.removeClass();

elm.className = "";

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .removeClass([className])
$jqList.removeClass(className);

elm.classList.remove(className);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .removeClass(function)
$jqList.removeClass((idx, className) => (idx % 2) ? "odd" : "even");

elmList.forEach((elm, idx) => elm.classList.remove((idx % 2) ? "odd" : "even"));


// =============================================================================
// SIGNATURE: .removeData([name])
$jqList.removeData();

// TODO

// ---------------------------------
// SIGNATURE: .removeData([list])
$jqList.removeData();

// TODO


// =============================================================================
// .removeProp(propertyName)
$jqList.removeProp();

// TODO


// =============================================================================
// SIGNATURE: .replaceAll(target)
$jqList.replaceAll(otherElm);

otherElm.replaceWith(elm);


// =============================================================================
// SIGNATURE: .replaceWith(newContent)
$jqList.replaceWith(markupString);

elm.replaceWith(markupString);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .replaceWith(function)
$jqList.replaceWith(func);

// TODO


// =============================================================================
// SIGNATURE: .scrollLeft()
$jqList.scrollLeft();

// TODO

// ---------------------------------
// SIGNATURE: .scrollLeft(value)
$jqList.scrollLeft();

// TODO


// =============================================================================
// SIGNATURE: .scrollTop()
$jqList.scrollTop();

// TODO

// ---------------------------------
// SIGNATURE: .scrollTop(value)
$jqList.scrollTop();

// TODO


// =============================================================================
// SIGNATURE: .serialize()
$jqList.serialize();

// TODO


// =============================================================================
// SIGNATURE: .serializeArray()
$jqList.serializeArray();

// TODO


// =============================================================================
// SIGNATURE: .siblings([selector])
$jqList.siblings();

[...elm.parentNode.children].filter(item => item !== elm);

// ---------------------------------
// SIGNATURE: .siblings([selector])
$jqList.siblings(selector);

[...elm.parentNode.children].filter(item => item !== elm && item.match(selector));


// =============================================================================
// SIGNATURE: .size()
$jqList.size();

elmList.length;


// =============================================================================
// SIGNATURE: .slice(start, [end])
$jqList.slice(start);

Array.prototype.slice.call(elmList, start);

// ---------------------------------
// SIGNATURE: .slice(start, [end])
$jqList.slice(start, end);

Array.prototype.slice.call(elmList, start, end);


// =============================================================================
// SIMILAR METHOD: #slideDown(), #slideUp()

    // ---------------------------------
    // SIGNATURE: .slideDown([duration], [complete])
    $jqList.slideDown();

    elm.style.transition = `height 1000ms`;
    elm.style.height = "200px";
    setTimeout(() => elm.style.transition = "", 1000);

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .slideDown([duration], [complete])
    $jqList.slideDown(number);

    elm.style.transition = `height ${number}ms`;
    elm.style.height = "200px";
    setTimeout(() => elm.style.transition = "", number);

    elmList.forEach(elm => {/* same as above */});

    // ---------------------------------
    // SIGNATURE: .slideDown(options)
    $jqList.slideDown();

    // TODO

    // ---------------------------------
    // SIGNATURE: .slideDown([duration], [easing], [complete])
    $jqList.slideDown();

    // TODO


// =============================================================================
// SIGNATURE: .slideToggle([duration], [complete])
$jqList.slideToggle();

elm.style.transition = `height 1000ms`;
elm.style.height = (elm.style.height == "0px") ? "200px" : "0px";
setTimeout(() => elm.style.transition = "", 1000);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .slideToggle([duration], [complete])
$jqList.slideToggle(number);

elm.style.transition = `height ${number}ms`;
elm.style.height = (elm.style.height == "0px") ? "200px" : "0px";
setTimeout(() => elm.style.transition = "", number);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .slideToggle(options)
$jqList.slideToggle();

// TODO

// ---------------------------------
// SIGNATURE: .slideToggle([duration], [easing], [complete])
$jqList.slideToggle();

// TODO


// =============================================================================
// SIGNATURE: .stop([clearQueue], [jumpToEnd])
$jqList.stop();

// TODO

// ---------------------------------
// SIGNATURE: .stop([queue], [clearQueue], [jumpToEnd])
$jqList.stop();

// TODO


// =============================================================================
// SIGNATURE: .text()
$jqList.text();

el.textContent;

elmList[0].textContent;

// ---------------------------------
// SIGNATURE: .text(text)
$jqList.text(nonMarkupString);

elm.textContent = nonMarkupString;

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .text(function)
$jqList.text((idx, text) => `line ${idx} has ${text.length} chars.`);

elmList.forEach((elm, idx) => elm.textContent = `line ${idx} has ${elm.textContent.length} chars.`);


// =============================================================================
// SIGNATURE: .toArray()
$jqList.toArray();

[...elmList];


// =============================================================================
// SIGNATURE: .toggle([duration], [complete])
$jqList.toggle();

elm.style.display = (elm.style.display == "none") ? "block" : "none";

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .toggle([duration], [complete])
// see: .toggle(duration, [easing], [complete])

// ---------------------------------
// SIGNATURE: .toggle(options)
$jqList.toggle(options);

elm.style.transition = `all ${options.duration}ms ${options.easing}`;
elm.style.height = (elm.style.height == "0px") ? "200px" : "0px";
elm.style.width = (elm.style.width == "0px") ? "200px" : "0px";
elm.style.opacity = (elm.style.opacity == "0") ? "1" : "0";
setTimeout(() => {elm.style.transition = ""; options.complete()}, options.duration);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .toggle(duration, [easing], [complete])
$jqList.toggle(duration, easing, complete);

elm.style.transition = `all ${duration}ms ${easing}`;
elm.style.height = (elm.style.height == "0px") ? "200px" : "0px";
elm.style.width = (elm.style.width == "0px") ? "200px" : "0px";
elm.style.opacity = (elm.style.opacity == "0") ? "1" : "0";
setTimeout(() => {elm.style.transition = ""; complete()}, duration);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .toggle(display)
$jqList.toggle(display);

elm.style.display = display ? "block" : "none";

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .toggle( handler, handler, [handler])
$jqList.toggle();

// TODO


// =============================================================================
// SIGNATURE: .toggleClass(className)
$jqList.toggleClass(className);

elm.classList.toggle(className);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .toggleClass(className, state)
$jqList.toggleClass();

state ? elm.classList.add(className) : elm.classList.remove(className);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .toggleClass(function, [state])
$jqList.toggleClass();

// TODO

// ---------------------------------
// SIGNATURE: .toggleClass([state])
$jqList.toggleClass();

// TODO


// =============================================================================
// SIGNATURE: .trigger(eventType, [extraParameters])
$jqList.trigger(eventType);

elm.dispatchEvent(new Event(eventType));

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .trigger(eventType, [extraParameters])
$jqList.trigger(eventType, {key1: 'data1', key2: 'data2'});

elm.dispatchEvent(new CustomEvent(eventType), {detail: {key1: 'data1', key2: 'data2'}});

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .trigger(event, [extraParameters])
$jqList.trigger();

// TODO


// =============================================================================
// SIGNATURE: .triggerHandler(eventType, [extraParameters])
$jqList.triggerHandler();

// TODO

// ---------------------------------
// SIGNATURE: .triggerHandler(event, [extraParameters])
$jqList.triggerHandler();

// TODO


// =============================================================================
// SIGNATURE: .unbind(eventType, [handler])
$jqList.unbind(eventName, func);

elm.removeEventListener(eventName, func);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .unbind(eventType, false)
$jqList.unbind();

// TODO

// ---------------------------------
// SIGNATURE: .unbind(event)
$jqList.unbind();

// TODO

// ---------------------------------
// SIGNATURE: .unbind()
$jqList.unbind();

elm.parentNode.replaceChild(elm.cloneNode(true), elm);

elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .undelegate()
$jqList.undelegate();

// TODO

// ---------------------------------
// SIGNATURE: .undelegate(selector, eventType)
$jqList.undelegate();

// TODO

// ---------------------------------
// SIGNATURE: .undelegate(selector, eventType, handler)
$jqList.undelegate();

// TODO

// ---------------------------------
// SIGNATURE: .undelegate(selector, events)
$jqList.undelegate();

// TODO

// ---------------------------------
// SIGNATURE: .undelegate(namespace)
$jqList.undelegate();

// TODO


// =============================================================================
// SIGNATURE: .unwrap()
$jqList.unwrap();

parent = elm.parentNode;
(parent != document.body) && parent.parentNode.insertBefore(elm, parent).parentNode.removeChild(parent);

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .unwrap([selector])
$jqList.unwrap(selector);


current = elm;
parent = elm.parentNode;
while (!parent.matches(selector) && parent != document.body) {
    current = parent;
    parent = parent.parentNode;
}
(parent != document.body) && parent.parentNode.insertBefore(current, parent).parentNode.removeChild(parent);


elmList.forEach(elm => {/* same as above */});


// =============================================================================
// SIGNATURE: .val()
$jqList.val();

elm.value;

elmList[0].value;

// ---------------------------------
// SIGNATURE: .val(value)
$jqList.val(nonMarkupString);

elm.value = nonMarkupString;

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .val(function)
$jqList.val((idx, val) => `input ${idx} has ${val.length} chars.`);

elmList.forEach((elm, idx) => elm.value = `input ${idx} has ${elm.value.length} chars.`);


// =============================================================================
// SIGNATURE: .width()
$jqList.width();

parseFloat(getComputedStyle(elm).width);

parseFloat(getComputedStyle(elmList[0]).width);

// ---------------------------------
// SIGNATURE: .width(value)
$jqList.width(number);

elm.style.width = `${number}px`;

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .width(function)
$jqList.width((idx, width) => idx * 5 + width);

elmList.forEach((elm, idx) => elm.style.width = (idx * 5 + width) + 'px');


// =============================================================================
// SIGNATURE: .wrap(wrappingElement)
$jqList.wrap(otherElm || markupString);

elm.parentNode.insertBefore(otherElm.cloneNode(true), elm).appendChild(elm);

elmList.forEach(elm => {/* same as above */});

newElm = (new Range).createContextualFragment(markupString).firstElementChild;
elm.parentNode.insertBefore(newElm, elm).appendChild(elm);

newElm = (new Range).createContextualFragment(markupString).firstElementChild;
elmList.forEach(elm => elm.parentNode.insertBefore(newElm.cloneNode(true), elm).appendChild(elm));

// ---------------------------------
// SIGNATURE: .wrap(function)
$jqList.wrap(idx => (idx % 2) ? markupString1 : markupString2);

elmList.forEach((elm, idx) => {
    wrapper = (idx % 2) ? markupString1 : markupString2;
    newElm = (new Range).createContextualFragment(wrapper).firstElementChild;
    elm.parentNode.insertBefore(newElm, elm).appendChild(elm);
});


// =============================================================================
// SIGNATURE: .wrapAll(wrappingElement)
$jqList.wrapAll(otherElm);

newElm = elmList[0].parentNode.insertBefore(otherElm.cloneNode(true), elmList[0]);
elmList.forEach(elm => newElm.append(elm));

// ---------------------------------
// SIGNATURE: .wrapAll(function)
$jqList.wrapAll(func);

// TODO


// =============================================================================
// SIGNATURE: .wrapInner(wrappingElement)
$jqList.wrapInner(otherElm);

newElm = otherElm.cloneNode(true);
elm.prepend(newElm);
[...elm.childNodes].forEach(item => (newElm !== item) && newElm.append(item));

elmList.forEach(elm => {/* same as above */});

// ---------------------------------
// SIGNATURE: .wrapInner(function)
$jqList.wrapInner(idx => (idx % 2) ? markupString1 : markupString2);

elmList.forEach((elm, idx) => {
    wrapper = (idx % 2) ? markupString1 : markupString2;
    newElm = (new Range).createContextualFragment(wrapper).firstElementChild;
    elm.prepend(newElm);
    [...elm.childNodes].forEach(item => (newElm !== item) && newElm.append(item));
});


```
