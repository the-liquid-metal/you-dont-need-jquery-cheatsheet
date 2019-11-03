# "You don't need jQuery" Cheatsheet

Why another "You don't need jQuery" article?
* They are too verbose: use of wasteful pharenthesis, new line, semicolon, etc;
  create less concise variable; or even function. Present of function means they
  don't realize they replace jQuery with "myQuery" :yum:. They don't realize jQuery
  is so elegance that they fail to replace it.
* The solution is out of context. jQuery solves problems only by javascript. If
  any solution force you to write CSS (or anykind except javascript), it means it
  fails to replace jQuery.
* They still mention IE :disappointed:. Ask your users to throw away IE and use
  newest open source browser, you will be free from pain.

Credit:
* https://github.com/nefe/You-Dont-Need-jQuery
* http://youmightnotneedjquery.com/

How to jump to the point immediately:
1. press [CTRL]+[F]
2. then type [.], then type the keyword, then type [(]
3. then press [ENTER]

How ro read:
* if 1st and 2nd line are similar, than pick one, than pick one of 3rd or 4th line which has similar term.
  ```js
  $(elm).on(eventName, func);
  $(elmList).on(eventName, func);
  
  elm.addEventListener(eventName, func);
  elmList.forEach(item => item.addEventListener(eventName, func));
  ```

* If there is additional line before 3rd line, include it whichever your choice.
  ```js
  $(elm).blur();
  $(elmList).blur();
  
  let blur = new Event("blur");
  elm.dispatchEvent(blur);
  elmList.forEach(item => item.dispatchEvent(blur));
  ```

* If pair of 1st line is missing, than the rest of code is a replacement as a whole, until blank line.
  If there is another line(s) after blank line, it acts as alternative solution of previous one.
  ```js
  $(elm).fadeOut();
  
  elm.style.transition = `opacity ${number}ms`;
  elm.addEventListener("transitionend", () => {elm.style.display = "none"; elm.style.transition = ""}, {once: true});
  elm.style.opacity = "0";
  ```

* If operand appears as hardcoded value (whether it is string, number, boolean, or null),
  than you shoud not change it with anykind, otherwise the behaviour/output is unpredictable.
  ```js
  elm.addEventListener("click", func); // in this case is "click"
  ```
  If operand appears as variable, than you could change it with any value with same type.
  Confirm its type at the declaration line (at the topmost).
  ```js
  elm.addEventListener("click", func); // in this case is func
  ```

* This script is designed to be self documented. Rather than written like this:
  ```js
  elm.append(param); // param is HTMLElement or non markup string
  ```
  it would be more elegance and natural if it written like this:
  ```js
  elm.append(otherElm || nonMarkupString);
  ```
  than you have to interpret it as ```elm.append(otherElm);``` or as
  ```elm.append(nonMarkupString);```

* If you see ``` // TODO``` this means i need your help to fill this space.

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
$(elm).addClass("new-class");
$(elmList).addClass("new-class");

elm.classList.add("new-class");
elmList.forEach(item => item.classList.add("new-class"));


// =============================================================================
$(elm).after(markupString);
$(elmList).after(markupString);

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
$(elm).append(otherElm);

elm.appendChild(otherElm);
elm.append(otherElm || nonMarkupString);


// =============================================================================
$(elm).appendTo(otherElm);

otherElm.appendChild(elm);


// =============================================================================
$(elm).attr("placeholder");
$(elmList).attr("placeholder");

elm.getAttribute("placeholder");
elmList[0].getAttribute("placeholder");

// ---------------------------------

$(elm).attr("placeholder", "price");
$(elmList).attr("placeholder", "price");

elm.setAttribute("placeholder", "price");
elmList.forEach(item => item.setAttribute("placeholder"));


// =============================================================================
$(elm).before(markupString);
$(elmList).before(markupString);

elm.insertAdjacentHTML("beforebegin", markupString);
elmList.forEach(item => item.insertAdjacentHTML("beforebegin", markupString));


// =============================================================================
$(elm).bind(eventName, func);
$(elmList).bind(eventName, func);

elm.addEventListener(eventName, func);
elmList.forEach(item => item.addEventListener(eventName, func));


// =============================================================================
$(elm).blur(func);
$(elmList).blur(func);

elm.addEventListener("blur", func);
elmList.forEach(item => item.addEventListener("blur", func));

// ---------------------------------

$(elm).blur();
$(elmList).blur();

let blur = new Event("blur");
elm.dispatchEvent(blur);
elmList.forEach(item => item.dispatchEvent(blur));


// =============================================================================
$(elm).change(func);
$(elmList).change(func);

elm.addEventListener("change", func);
elmList.forEach(item => item.addEventListener("change", func));

// ---------------------------------

$(elm).change();
$(elmList).change();

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
$(elm).click(func);
$(elmList).click(func);

elm.addEventListener("click", func);
elmList.forEach(item => item.addEventListener("click", func));

// ---------------------------------

$(elm).click(func);
$(elmList).click(func);

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
$(elm).css("border-width", "20px");
$(elmList).css("border-width", "20px");

elm.style.borderWidth = "20px";
elmList.forEach(item => item.style.borderWidth = "20px");


// =============================================================================
$(elm).data();

// TODO


// =============================================================================
$(elm).dblclick(func);
$(elmList).dblclick(func);

elm.addEventListener("dblclick", func);
elmList.forEach(item => item.addEventListener("dblclick", func));

// ---------------------------------

$(elm).dblclick();
$(elmList).dblclick();

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
$(elm).fadeIn();

elm.style.transition = `opacity ${number}ms`;
elm.style.display = "block";
setTimeout(() => {elm.style.opacity = "1"; setTimeout(() => elm.style.transition = "", 1)}, 1000);


// =============================================================================
$(elm).fadeOut();

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
$(elm).focus(func);
$(elmList).focus(func);

elm.addEventListener("focus", func);
elmList.forEach(item => item.addEventListener("focus", func));

// ---------------------------------

$(elm).focus();
$(elmList).focus();

let focus = new Event("focus");
elm.dispatchEvent(focus);
elmList.forEach(item => item.dispatchEvent(focus));


// =============================================================================
$(elm).focusin(func);
$(elmList).focusin(func);

elm.addEventListener("focusin", func);
elmList.forEach(item => item.addEventListener("focusin", func));

// ---------------------------------

$(elm).focusin();
$(elmList).focusin();

let focusin = new Event("focusin");
elm.dispatchEvent(focusin);
elmList.forEach(item => item.dispatchEvent(focusin));


// =============================================================================
$(elm).focusout(func);
$(elmList).focusout(func);

elm.addEventListener("focusout", func);
elmList.forEach(item => item.addEventListener("focusout", func));

// ---------------------------------

$(elm).focusout();
$(elmList).focusout();

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
$(elm).hide();
$(elmList).hide();

elm.style.display = "none";
elmList.forEach(item => item.style.display = "none");


// =============================================================================
$(elm).hover(func);
$(elmList).hover(func);

elm.addEventListener("hover", func);
elmList.forEach(item => item.addEventListener("hover", func));

// ---------------------------------

$(elm).hover();
$(elmList).hover();

let hover = new Event("hover");
elm.dispatchEvent(hover);
elmList.forEach(item => item.dispatchEvent(hover));


// =============================================================================
$(elm).html(markupString);
$(elmList).html(markupString);

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
$(elm).keydown(func);
$(elmList).keydown(func);

elm.addEventListener("keydown", func);
elmList.forEach(item => item.addEventListener("keydown", func));

// ---------------------------------

$(elm).keydown();
$(elmList).keydown();

let keydown = new Event("keydown");
elm.dispatchEvent(keydown);
elmList.forEach(item => item.dispatchEvent(keydown));


// =============================================================================
$(elm).keypress(func);
$(elmList).keypress(func);

elm.addEventListener("keypress", func);
elmList.forEach(item => item.addEventListener("keypress", func));

// ---------------------------------

$(elm).keypress();
$(elmList).keypress();

let keypress = new Event("keypress");
elm.dispatchEvent(keypress);
elmList.forEach(item => item.dispatchEvent(keypress));


// =============================================================================
$(elm).keyup(func);
$(elmList).keyup(func);

elm.addEventListener("keyup", func);
elmList.forEach(item => item.addEventListener("keyup", func));

// ---------------------------------

$(elm).keyup();
$(elmList).keyup();

let keyup = new Event("keyup");
elm.dispatchEvent(keyup);
elmList.forEach(item => item.dispatchEvent(keyup));


// =============================================================================
$(elm).last();

// TODO


// =============================================================================
$(elm).live(eventName, func);
$(elmList).live(eventName, func);

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
$(elm).mousedown(func);
$(elmList).mousedown(func);

elm.addEventListener("mousedown", func);
elmList.forEach(item => item.addEventListener("mousedown", func));

// ---------------------------------

$(elm).mousedown();
$(elmList).mousedown();

let mousedown = new Event("mousedown");
elm.dispatchEvent(mousedown);
elmList.forEach(item => item.dispatchEvent(mousedown));


// =============================================================================
$(elm).mouseenter(func);
$(elmList).mouseenter(func);

elm.addEventListener("mouseenter", func);
elmList.forEach(item => item.addEventListener("mouseenter", func));

// ---------------------------------

$(elm).mouseenter();
$(elmList).mouseenter();

let mouseenter = new Event("mouseenter");
elm.dispatchEvent(mouseenter);
elmList.forEach(item => item.dispatchEvent(mouseenter));


// =============================================================================
$(elm).mouseleave(func);
$(elmList).mouseleave(func);

elm.addEventListener("mouseleave", func);
elmList.forEach(item => item.addEventListener("mouseleave", func));

// ---------------------------------

$(elm).mouseleave();
$(elmList).mouseleave();

let mouseleave = new Event("mouseleave");
elm.dispatchEvent(mouseleave);
elmList.forEach(item => item.dispatchEvent(mouseleave));


// =============================================================================
$(elm).mousemove(func);
$(elmList).mousemove(func);

elm.addEventListener("mousemove", func);
elmList.forEach(item => item.addEventListener("mousemove", func));

// ---------------------------------

$(elm).mousemove();
$(elmList).mousemove();

let mousemove = new Event("mousemove");
elm.dispatchEvent(mousemove);
elmList.forEach(item => item.dispatchEvent(mousemove));


// =============================================================================
$(elm).mouseout(func);
$(elmList).mouseout(func);

elm.addEventListener("mouseout", func);
elmList.forEach(item => item.addEventListener("mouseout", func));

// ---------------------------------

$(elm).mouseout();
$(elmList).mouseout();

let mouseout = new Event("mouseout");
elm.dispatchEvent(mouseout);
elmList.forEach(item => item.dispatchEvent(mouseout));


// =============================================================================
$(elm).mouseover(func);
$(elmList).mouseover(func);

elm.addEventListener("mouseover", func);
elmList.forEach(item => item.addEventListener("mouseover", func));

// ---------------------------------

$(elm).mouseover();
$(elmList).mouseover();

let mouseover = new Event("mouseover");
elm.dispatchEvent(mouseover);
elmList.forEach(item => item.dispatchEvent(mouseover));


// =============================================================================
$(elm).mouseup(func);
$(elmList).mouseup(func);

elm.addEventListener("mouseup", func);
elmList.forEach(item => item.addEventListener("mouseup", func));

// ---------------------------------

$(elm).mouseup();
$(elmList).mouseup();

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
$(elm).on(eventName, func);
$(elmList).on(eventName, func);

elm.addEventListener(eventName, func);
elmList.forEach(item => item.addEventListener(eventName, func));


// =============================================================================
$(elm).one(eventName, func);
$(elmList).one(eventName, func);

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
$(elm).slideDown();

// TODO


// =============================================================================
$(elm).slideToggle();

// TODO


// =============================================================================
$(elm).slideUp();

// TODO


// =============================================================================
$(elm).stop();

// TODO


// =============================================================================
$(elm).submit(func);

// TODO


// =============================================================================
$(elm).text("any text");
$(elmList).text("any text");

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
