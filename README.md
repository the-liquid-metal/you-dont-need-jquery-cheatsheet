# "You don't need jQuery" Cheatsheet

**Why another "You don't need jQuery" article?**
* They are too verbose: use of wasteful pharenthesis, new line, semicolon, etc;
  create less concise variable; or even function. Present of function means they
  don't realize they replace jQuery with "myQuery" :yum:. They don't realize jQuery
  is so elegance that they fail to replace it.
* The solution is out of context. jQuery solves problems only by javascript. If
  any solution force you to write CSS (or anykind except javascript), it means it
  fails to replace jQuery.
* They still mention IE :disappointed:. Ask your users to throw away IE and use
  newest open source browser, you will be free from pain.

**Credit:**
* https://github.com/nefe/You-Dont-Need-jQuery
* http://youmightnotneedjquery.com/

**How to jump to the point immediately:**
1. press `[CTRL]+[F]`
2. then type `[.]`, then type the keyword, then type `[(]`
3. then press `[ENTER]`

**How to read:**
* This script is designed to be self documented. Rather than written like this:
  ```js
  $(param).attr(attribute); // param is CSS selector, HTMLElement, HTMLElement collection
  ```
  it would be more elegance and natural if it written like this:
  ```js
  $(selector || elm || elmList).attr(attribute);
  ```
  You have to interpret it as `$(selector).attr(attribute);` or as
  `$(elm).attr(attribute);` or as `$(elmList).attr(attribute);`

* One unit of solution is defined as a consecutive number of lines and ended
  with blank line. The example of problem below has 3 solutions.
  ```js
  $(selector || elm || elmList).attr(attribute);

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
bellow, you will see many getter written like this one `$(selector || elm || elmList).attr(attribute);`.
But there is no such thing like that, right?!. The realistic is like this one
`let pocket = $(selector || elm || elmList).attr(attribute);` or like this one
`if ($(selector || elm || elmList).attr(attribute)) {/* ... */}`. The reason we
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
Unless you are sure with what you are dealing with, every solution in this article
are not safe. The exact solutions are like this:
```js
$(selector || elm || elmList).attr(attribute);

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
$(elm).add(elm);

[...elmList].push(elm);


// =============================================================================
$(elm).addBack();

[...elmList].filter((item, idx, self) => idx >= self.indexOf(elm));


// =============================================================================
$(selector || elm || elmList).addClass("new-class");

elm.classList.add("new-class");
elmList.forEach(item => item.classList.add("new-class"));


// =============================================================================
$(selector || elm || elmList).after(markupString);

elm.insertAdjacentHTML("afterend", markupString);
elmList.forEach(item => item.insertAdjacentHTML("afterend", markupString));


// =============================================================================
$(elm).ajaxComplete(func);

// TODO


// =============================================================================
$(elm).ajaxError(func);

// TODO


// =============================================================================
$(elm).ajaxSend(func);

// TODO


// =============================================================================
$(elm).ajaxStart(func);

// TODO


// =============================================================================
$(elm).ajaxStop(func);

// TODO


// =============================================================================
$(elm).ajaxSuccess(func);

// TODO


// =============================================================================
$(elm).andSelf();

// TODO


// =============================================================================
$(elm).animate();

// TODO


// =============================================================================
$(selector || elm || elmList).append(otherElm);

elm.appendChild(otherElm);
elm.append(otherElm || nonMarkupString);


// =============================================================================
$(elm).appendTo(otherElm);

otherElm.appendChild(elm);


// =============================================================================
$(selector || elm || elmList).attr("placeholder");

elm.getAttribute("placeholder");
elmList[0].getAttribute("placeholder");

// ---------------------------------

$(selector || elm || elmList).attr("placeholder", "price");

elm.setAttribute("placeholder", "price");
elmList.forEach(item => item.setAttribute("placeholder"));


// =============================================================================
$(selector || elm || elmList).before(markupString);

elm.insertAdjacentHTML("beforebegin", markupString);
elmList.forEach(item => item.insertAdjacentHTML("beforebegin", markupString));


// =============================================================================
$(selector || elm || elmList).bind(eventName, func);

elm.addEventListener(eventName, func);
elmList.forEach(item => item.addEventListener(eventName, func));


// =============================================================================
$(selector || elm || elmList).blur(func);

elm.addEventListener("blur", func);
elmList.forEach(item => item.addEventListener("blur", func));

// ---------------------------------

$(selector || elm || elmList).blur();

let blur = new Event("blur");
elm.dispatchEvent(blur);
elmList.forEach(item => item.dispatchEvent(blur));


// =============================================================================
$(selector || elm || elmList).change(func);

elm.addEventListener("change", func);
elmList.forEach(item => item.addEventListener("change", func));

// ---------------------------------

$(selector || elm || elmList).change();

let change = new Event("change");
elm.dispatchEvent(change);
elmList.forEach(item => item.dispatchEvent(change));


// =============================================================================
$(elm).children();

elm.children;


// =============================================================================
$(elm).clearQueue();

// TODO


// =============================================================================
$(selector || elm || elmList).click(func);

elm.addEventListener("click", func);
elmList.forEach(item => item.addEventListener("click", func));

// ---------------------------------

$(selector || elm || elmList).click(func);

let click = new Event("click");
elm.dispatchEvent(click);
elmList.forEach(item => item.dispatchEvent(click));


// =============================================================================
$(elm).clone();

// TODO


// =============================================================================
$(elm).closest();

// TODO


// =============================================================================
$(elm).contents();

// TODO


// =============================================================================
$(elm).contextmenu();

// TODO


// =============================================================================
$(selector || elm || elmList).css("border-width", "20px");

elm.style.borderWidth = "20px";
elmList.forEach(item => item.style.borderWidth = "20px");


// =============================================================================
$(elm).data();

// TODO


// =============================================================================
$(selector || elm || elmList).dblclick(func);

elm.addEventListener("dblclick", func);
elmList.forEach(item => item.addEventListener("dblclick", func));

// ---------------------------------

$(selector || elm || elmList).dblclick();

let dblclick = new Event("dblclick");
elm.dispatchEvent(dblclick);
elmList.forEach(item => item.dispatchEvent(dblclick));


// =============================================================================
$(elm).delay();

// TODO


// =============================================================================
$(elm).delegate();

// TODO


// =============================================================================
$(elm).dequeue();

// TODO


// =============================================================================
$(elm).detach();

// TODO


// =============================================================================
$(elm).die();

// TODO


// =============================================================================
$(elm).each();

// TODO


// =============================================================================
$(elm).empty();

// TODO


// =============================================================================
$(elm).end();

// TODO


// =============================================================================
$(elm).eq();

// TODO


// =============================================================================
$(elm).error();

// TODO


// =============================================================================
$(selector || elm || elmList).fadeIn();

elm.style.transition = `opacity ${number}ms`;
elm.style.display = "block";
setTimeout(() => {elm.style.opacity = "1"; setTimeout(() => elm.style.transition = "", 1)}, 1000);


// =============================================================================
$(selector || elm || elmList).fadeOut();

elm.style.transition = `opacity ${number}ms`;
elm.addEventListener("transitionend", () => {elm.style.display = "none"; elm.style.transition = ""}, {once: true});
elm.style.opacity = "0";


// =============================================================================
$(elm).fadeTo();

// TODO


// =============================================================================
$(elm).fadeToggle();

// TODO


// =============================================================================
$(elm).filter();

// TODO


// =============================================================================
$(elm).find();

// TODO


// =============================================================================
$(elm).finish();

// TODO


// =============================================================================
$(elm).first();

// TODO


// =============================================================================
$(selector || elm || elmList).focus(func);

elm.addEventListener("focus", func);
elmList.forEach(item => item.addEventListener("focus", func));

// ---------------------------------

$(selector || elm || elmList).focus();

let focus = new Event("focus");
elm.dispatchEvent(focus);
elmList.forEach(item => item.dispatchEvent(focus));


// =============================================================================
$(selector || elm || elmList).focusin(func);

elm.addEventListener("focusin", func);
elmList.forEach(item => item.addEventListener("focusin", func));

// ---------------------------------

$(selector || elm || elmList).focusin();

let focusin = new Event("focusin");
elm.dispatchEvent(focusin);
elmList.forEach(item => item.dispatchEvent(focusin));


// =============================================================================
$(selector || elm || elmList).focusout(func);

elm.addEventListener("focusout", func);
elmList.forEach(item => item.addEventListener("focusout", func));

// ---------------------------------

$(selector || elm || elmList).focusout();

let focusout = new Event("focusout");
elm.dispatchEvent(focusout);
elmList.forEach(item => item.dispatchEvent(focusout));


// =============================================================================
$(elm).get();

// TODO


// =============================================================================
$(elm).has();

// TODO


// =============================================================================

// TODO


// =============================================================================
$(elm).height();

// TODO


// =============================================================================
$(selector || elm || elmList).hide();

elm.style.display = "none";
elmList.forEach(item => item.style.display = "none");


// =============================================================================
$(selector || elm || elmList).hover(func);

elm.addEventListener("hover", func);
elmList.forEach(item => item.addEventListener("hover", func));

// ---------------------------------

$(selector || elm || elmList).hover();

let hover = new Event("hover");
elm.dispatchEvent(hover);
elmList.forEach(item => item.dispatchEvent(hover));


// =============================================================================
$(selector || elm || elmList).html(markupString);

elm.innerHTML = markupString;
elmList.forEach(item => item.innerHTML = markupString);


// =============================================================================
$(elm).index();

// TODO


// =============================================================================
$(elm).innerHeight();

// TODO


// =============================================================================
$(elm).innerWidth();

// TODO


// =============================================================================
$(elm).insertAfter();

// TODO


// =============================================================================
$(elm).insertBefore();

// TODO


// =============================================================================
$(elm).is();

// TODO


// =============================================================================
$(selector || elm || elmList).keydown(func);

elm.addEventListener("keydown", func);
elmList.forEach(item => item.addEventListener("keydown", func));

// ---------------------------------

$(selector || elm || elmList).keydown();

let keydown = new Event("keydown");
elm.dispatchEvent(keydown);
elmList.forEach(item => item.dispatchEvent(keydown));


// =============================================================================
$(selector || elm || elmList).keypress(func);

elm.addEventListener("keypress", func);
elmList.forEach(item => item.addEventListener("keypress", func));

// ---------------------------------

$(selector || elm || elmList).keypress();

let keypress = new Event("keypress");
elm.dispatchEvent(keypress);
elmList.forEach(item => item.dispatchEvent(keypress));


// =============================================================================
$(selector || elm || elmList).keyup(func);

elm.addEventListener("keyup", func);
elmList.forEach(item => item.addEventListener("keyup", func));

// ---------------------------------

$(selector || elm || elmList).keyup();

let keyup = new Event("keyup");
elm.dispatchEvent(keyup);
elmList.forEach(item => item.dispatchEvent(keyup));


// =============================================================================
$(elm).last();

// TODO


// =============================================================================
$(selector || elm || elmList).live(eventName, func);

elm.addEventListener(eventName, func);
elmList.forEach(item => item.addEventListener(eventName, func));


// =============================================================================
$(elm).load();

// TODO


// =============================================================================
$(elm).load();

// TODO


// =============================================================================
$(elm).map();

// TODO


// =============================================================================
$(selector || elm || elmList).mousedown(func);

elm.addEventListener("mousedown", func);
elmList.forEach(item => item.addEventListener("mousedown", func));

// ---------------------------------

$(selector || elm || elmList).mousedown();

let mousedown = new Event("mousedown");
elm.dispatchEvent(mousedown);
elmList.forEach(item => item.dispatchEvent(mousedown));


// =============================================================================
$(selector || elm || elmList).mouseenter(func);

elm.addEventListener("mouseenter", func);
elmList.forEach(item => item.addEventListener("mouseenter", func));

// ---------------------------------

$(selector || elm || elmList).mouseenter();

let mouseenter = new Event("mouseenter");
elm.dispatchEvent(mouseenter);
elmList.forEach(item => item.dispatchEvent(mouseenter));


// =============================================================================
$(selector || elm || elmList).mouseleave(func);

elm.addEventListener("mouseleave", func);
elmList.forEach(item => item.addEventListener("mouseleave", func));

// ---------------------------------

$(selector || elm || elmList).mouseleave();

let mouseleave = new Event("mouseleave");
elm.dispatchEvent(mouseleave);
elmList.forEach(item => item.dispatchEvent(mouseleave));


// =============================================================================
$(selector || elm || elmList).mousemove(func);

elm.addEventListener("mousemove", func);
elmList.forEach(item => item.addEventListener("mousemove", func));

// ---------------------------------

$(selector || elm || elmList).mousemove();

let mousemove = new Event("mousemove");
elm.dispatchEvent(mousemove);
elmList.forEach(item => item.dispatchEvent(mousemove));


// =============================================================================
$(selector || elm || elmList).mouseout(func);

elm.addEventListener("mouseout", func);
elmList.forEach(item => item.addEventListener("mouseout", func));

// ---------------------------------

$(selector || elm || elmList).mouseout();

let mouseout = new Event("mouseout");
elm.dispatchEvent(mouseout);
elmList.forEach(item => item.dispatchEvent(mouseout));


// =============================================================================
$(selector || elm || elmList).mouseover(func);

elm.addEventListener("mouseover", func);
elmList.forEach(item => item.addEventListener("mouseover", func));

// ---------------------------------

$(selector || elm || elmList).mouseover();

let mouseover = new Event("mouseover");
elm.dispatchEvent(mouseover);
elmList.forEach(item => item.dispatchEvent(mouseover));


// =============================================================================
$(selector || elm || elmList).mouseup(func);

elm.addEventListener("mouseup", func);
elmList.forEach(item => item.addEventListener("mouseup", func));

// ---------------------------------

$(selector || elm || elmList).mouseup();

let mouseup = new Event("mouseup");
elm.dispatchEvent(mouseup);
elmList.forEach(item => item.dispatchEvent(mouseup));


// =============================================================================
$(elm).next();

// TODO


// =============================================================================
$(elm).nextAll();

// TODO


// =============================================================================
$(elm).nextUntil();

// TODO


// =============================================================================
$(elm).not();

// TODO


// =============================================================================
$(elm).off();

// TODO


// =============================================================================
$(elm).offset();

// TODO


// =============================================================================
$(elm).offsetParent();

// TODO


// =============================================================================
$(selector || elm || elmList).on(eventName, func);

elm.addEventListener(eventName, func);

elmList.forEach(item => item.addEventListener(eventName, func));


// =============================================================================
$(selector || elm || elmList).one(eventName, func);

// TODO


// =============================================================================
$(elm).outerHeight();

// TODO


// =============================================================================
$(elm).outerWidth();

// TODO


// =============================================================================
$(elm).parent();

// TODO


// =============================================================================
$(elm).parents();

// TODO


// =============================================================================
$(elm).parentsUntil();

// TODO


// =============================================================================
$(elm).position();

// TODO


// =============================================================================
$(elm).prepend();

// TODO


// =============================================================================
$(elm).prependTo();

// TODO


// =============================================================================
$(elm).prev();

// TODO


// =============================================================================
$(elm).prevAll();

// TODO


// =============================================================================
$(elm).prevUntil();

// TODO


// =============================================================================
$(elm).promise();

// TODO


// =============================================================================
$(elm).prop();

// TODO


// =============================================================================
$(elm).pushStack();

// TODO


// =============================================================================
$(elm).queue();

// TODO


// =============================================================================
$(elm).ready();

// TODO


// =============================================================================
$(elm).remove();

// TODO


// =============================================================================
$(elm).removeAttr();

// TODO


// =============================================================================
$(elm).removeClass();

// TODO


// =============================================================================
$(elm).removeData();

// TODO


// =============================================================================
$(elm).removeProp();

// TODO


// =============================================================================
$(elm).replaceAll();

// TODO


// =============================================================================
$(elm).replaceWith();

// TODO


// =============================================================================
$(elm).resize(func);

// TODO


// =============================================================================
$(elm).scroll(func);

// TODO


// =============================================================================
$(elm).scrollLeft();

// TODO


// =============================================================================
$(elm).scrollTop();

// TODO


// =============================================================================
$(elm).select(func);

// TODO


// =============================================================================
$(elm).serialize();

// TODO


// =============================================================================
$(elm).serializeArray();

// TODO


// =============================================================================
$(elm).show();

// TODO


// =============================================================================
$(elm).siblings();

// TODO


// =============================================================================
$(elm).size();

// TODO


// =============================================================================
$(elm).slice();

// TODO


// =============================================================================
$(selector || elm || elmList).slideDown();

// TODO


// =============================================================================
$(selector || elm || elmList).slideToggle();

// TODO


// =============================================================================
$(selector || elm || elmList).slideUp();

// TODO


// =============================================================================
$(elm).stop();

// TODO


// =============================================================================
$(elm).submit(func);

// TODO


// =============================================================================
$(selector || elm || elmList).text("any text");

elm.textContent = "any text";
elmList.forEach(item => item.textContent = "any text");


// =============================================================================
$(elm).toArray();

// TODO


// =============================================================================
$(elm).toggle();

// TODO


// =============================================================================
$(elm).toggle();

// TODO


// =============================================================================
$(elm).toggleClass();

// TODO


// =============================================================================
$(elm).trigger();

// TODO


// =============================================================================
$(elm).triggerHandler();

// TODO


// =============================================================================
$(elm).unbind();

// TODO


// =============================================================================
$(elm).undelegate();

// TODO


// =============================================================================
$(elm).unload();

// TODO


// =============================================================================
$(elm).unwrap();

// TODO


// =============================================================================
$(elm).val();

// TODO


// =============================================================================
$(elm).width();

// TODO


// =============================================================================
$(elm).wrap();

// TODO


// =============================================================================
$(elm).wrapAll();

// TODO


// =============================================================================
$(elm).wrapInner();

// TODO


```
