# "You don't need jQuery" Cheatsheet

Why another "You don't need jQuery" article?
* they are to verbose
* they still mention IE

Ask your user to throw away IE and use newest open source browser, you will be free from pain.

Credit:
* https://github.com/nefe/You-Dont-Need-jQuery
* http://youmightnotneedjquery.com/

How ro read:
* if 1st and 2nd line are similar, than pick one, than pick one of 3rd or 4th line which has similar term.
```js
    $(elm).on(eventName, func);
    $(elmList).on(eventName, func);

    elm.addEventListener(eventName, func);
    elmList.forEach(item => item.addEventListener(eventName, func));
```

* if pair of 1st line is missing, than the rest of code is a replacement as a whole, until separator line (if present).
```js
    $(elm).fadeOut();

    elm.style.transition = "opacity 300 ms";
    elm.addEventListener("transitionend", () => elm.style.display = "none", {capture: false, once: true});
    elm.style.opacity = "0";
```

<br/><br/>

## Here we are:

```js
    /** @type {NodeList} */
    let elmList = document.querySelectorAll("div");

    /** @type {HTMLElement} */
    let elm = document.createElement("div");

    /** @type {HTMLElement} */
    let otherElm = document.createElement("div");

    /** @type {string} */
    let eventName = "any";

    /** @type {string} */
    let markupString = "<div>hello</div>";

    /**
     * @type {Function}
     */
    let func = function(){};

    // Create a new jQuery object with elements added to the set of matched elements.
        $(elm).add(elm);

        [...elmList].push(elm);


    // Add the previous set of elements on the stack to the current set, optionally
    // filtered by a selector.
        $(elm).addBack();

        [...elmList].filter((item, idx, self) => idx >= self.indexOf(elm));


    // Adds the specified class(es) to each element in the set of matched elements.
        $(elm).addClass("new-class");
        $(elmList).addClass("new-class");

        elm.classList.add("new-class");
        elmList.forEach(item => item.classList.add("new-class"));

    // Insert content, specified by the parameter, after each element in the set
    // of matched elements.
        $(elm).after(markupString);
        $(elmList).after(markupString);

        elm.insertAdjacentHTML("afterend", markupString);
        elmList.forEach(item => item.insertAdjacentHTML("afterend", markupString));

    // Register a handler to be called when Ajax requests complete. This is an
    // AjaxEvent.
        $(elm).ajaxComplete(func);


    // Register a handler to be called when Ajax requests complete with an error.
    // This is an Ajax Event.
        $(elm).ajaxError(func);


    // Attach a function to be executed before an Ajax request is sent. This is
    // an Ajax Event.
        $(elm).ajaxSend(func);


    // Register a handler to be called when the first Ajax request begins. This
    // is an Ajax Event.
        $(elm).ajaxStart(func);


    // Register a handler to be called when all Ajax requests have completed.
    // This is an Ajax Event.
        $(elm).ajaxStop(func);


    // Attach a function to be executed whenever an Ajax request completes
    // successfully. This is an Ajax Event.
        $(elm).ajaxSuccess(func);


    // Add the previous set of elements on the stack to the current set.
        $(elm).andSelf();


    // Perform a custom animation of a set of CSS properties.
        $(elm).animate();


    // Insert content, specified by the parameter, to the end of each element in
    // the set of matched elements.
        $(elm).append(otherElm);

        elm.appendChild(otherElm);


    // Insert every element in the set of matched elements to the end of the target.
        $(elm).appendTo(otherElm);

        otherElm.appendChild(elm);

    // Get the value of an attribute for the first element in the set of matched
    // elements or set one or more attributes for every matched element.
        $(elm).attr("placeholder");
        $(elmList).attr("placeholder");

        elm.getAttribute("placeholder");
        elmList[0].getAttribute("placeholder");

        // --------------------------------------

        $(elm).attr("placeholder", "price");
        $(elmList).attr("placeholder", "price");

        elm.setAttribute("placeholder", "price");
        elmList.forEach(item => item.setAttribute("placeholder"));


    // Insert content, specified by the parameter, before each element in the set
    // of matched elements.
        $(elm).before(markupString);
        $(elmList).before(markupString);

        elm.insertAdjacentHTML("beforebegin", markupString);
        elmList.forEach(item => item.insertAdjacentHTML("beforebegin", markupString));


    // Attach a handler to an event for the elements.
        $(elm).bind(eventName, func);
        $(elmList).bind(eventName, func);

        elm.addEventListener(eventName, func);
        elmList.forEach(item => item.addEventListener(eventName, func));


    // Bind an event handler to the “blur” JavaScript event, or trigger that event
    // on an element.
        $(elm).blur(func);
        $(elmList).blur(func);

        elm.addEventListener("blur", func);
        elmList.forEach(item => item.addEventListener("blur", func));

        // --------------------------------------------------

        $(elm).blur();
        $(elmList).blur();

        let blur = new Event("blur");
        elm.dispatchEvent(blur);
        elmList.forEach(item => item.dispatchEvent(blur));


    // Bind an event handler to the “change” JavaScript event, or trigger that
    // event on an element.
        $(elm).change(func);
        $(elmList).change(func);

        elm.addEventListener("change", func);
        elmList.forEach(item => item.addEventListener("change", func));

        // --------------------------------------

        $(elm).change();
        $(elmList).change();

        let change = new Event("change");
        elm.dispatchEvent(change);
        elmList.forEach(item => item.dispatchEvent(change));


    // Get the children of each element in the set of matched elements, optionally
    // filtered by a selector.
        $(elm).children();

        elm.children;

    // Remove from the queue all items that have not yet been run.
        $(elm).clearQueue();


    // Bind an event handler to the “click” JavaScript event, or trigger that
    // event on an element.
        $(elm).click(func);
        $(elmList).click(func);

        elm.addEventListener("click", func);
        elmList.forEach(item => item.addEventListener("click", func));

        // --------------------------------------

        $(elm).click(func);
        $(elmList).click(func);

        let click = new Event("click");
        elm.dispatchEvent(click);
        elmList.forEach(item => item.dispatchEvent(click));

    // Create a deep copy of the set of matched elements.
        $(elm).clone();


    // For each element in the set, get the first element that matches the selector
    // by testing the element itself and traversing up through its ancestors in the DOM tree.
        $(elm).closest();


    // Get the children of each element in the set of matched elements, including
    // text and comment nodes.
        $(elm).contents();


    // Bind an event handler to the “contextmenu” JavaScript event, or trigger that
    // event on an element.
        $(elm).contextmenu();


    // Get the value of a computed style property for the first element in the set
    // of matched elements or set one or more CSS properties for every matched element.
        $(elm).css("border-width", "20px");
        $(elmList).css("border-width", "20px");

        elm.style.borderWidth = "20px";
        elmList.forEach(item => item.style.borderWidth = "20px");


    // Store arbitrary data associated with the matched elements or return the value
    // at the named data store for the first element in the set of matched elements.
        $(elm).data();


    // Bind an event handler to the “dblclick” JavaScript event, or trigger that
    // event on an element.
        $(elm).dblclick(func);
        $(elmList).dblclick(func);

        elm.addEventListener("dblclick", func);
        elmList.forEach(item => item.addEventListener("dblclick", func));

        // --------------------------

        $(elm).dblclick();
        $(elmList).dblclick();

        let dblclick = new Event("dblclick");
        elm.dispatchEvent(dblclick);
        elmList.forEach(item => item.dispatchEvent(dblclick));


    // Set a timer to delay execution of subsequent items in the queue.
        $(elm).delay();


    // Attach a handler to one or more events for all elements that match the
    // selector, now or in the future, based on a specific set of root elements.
        $(elm).delegate();


    // Execute the next function on the queue for the matched elements.
        $(elm).dequeue();


    // Remove the set of matched elements from the DOM.
        $(elm).detach();


    // Remove event handlers previously attached using .live(); from the elements.
        $(elm).die();


    // Iterate over a jQuery object, executing a function for each matched element.
        $(elm).each();


    // Remove all child nodes of the set of matched elements from the DOM.
        $(elm).empty();


    // End the most recent filtering operation in the current chain and return
    // the set of matched elements to its previous state.
        $(elm).end();


    // Reduce the set of matched elements to the one at the specified index.
        $(elm).eq();


    // Bind an event handler to the “error” JavaScript event.
        $(elm).error();


    // Display the matched elements by fading them to opaque.
        $(elm).fadeIn();


    // Hide the matched elements by fading them to transparent.
        $(elm).fadeOut();

        elm.style.transition = "opacity 300 ms";
        elm.addEventListener("transitionend", () => elm.style.display = "none", {capture: false, once: true});
        elm.style.opacity = "0";


    // Adjust the opacity of the matched elements.
        $(elm).fadeTo();


    // Display or hide the matched elements by animating their opacity.
        $(elm).fadeToggle();


    // Reduce the set of matched elements to those that match the selector or pass
    // the function’s test.
        $(elm).filter();


    // Get the descendants of each element in the current set of matched elements,
    // filtered by a selector, jQuery object, or element.
        $(elm).find();


    // Stop the currently-running animation, remove all queued animations, and
    // complete all animations for the matched elements.
        $(elm).finish();


    // Reduce the set of matched elements to the first in the set.
        $(elm).first();


    // Bind an event handler to the “focus” JavaScript event, or trigger that
    // event on an element.
        $(elm).focus(func);
        $(elmList).focus(func);

        elm.addEventListener("focus", func);
        elmList.forEach(item => item.addEventListener("focus", func));

        // --------------------------

        $(elm).focus();
        $(elmList).focus();

        let focus = new Event("focus");
        elm.dispatchEvent(focus);
        elmList.forEach(item => item.dispatchEvent(focus));


    // Bind an event handler to the “focusin” event.
        $(elm).focusin(func);
        $(elmList).focusin(func);

        elm.addEventListener("focusin", func);
        elmList.forEach(item => item.addEventListener("focusin", func));

        // --------------------------

        $(elm).focusin();
        $(elmList).focusin();

        let focusin = new Event("focusin");
        elm.dispatchEvent(focusin);
        elmList.forEach(item => item.dispatchEvent(focusin));


    // Bind an event handler to the “focusout” JavaScript event.
        $(elm).focusout(func);
        $(elmList).focusout(func);

        elm.addEventListener("focusout", func);
        elmList.forEach(item => item.addEventListener("focusout", func));

        // --------------------------

        $(elm).focusout();
        $(elmList).focusout();

        let focusout = new Event("focusout");
        elm.dispatchEvent(focusout);
        elmList.forEach(item => item.dispatchEvent(focusout));


    // Retrieve the DOM elements matched by the jQuery object.
        $(elm).get();


    // Reduce the set of matched elements to those that have a descendant that
    // matches the selector or DOM element.
        $(elm).has();


    // Determine whether any of the matched elements are assigned the given class.
        $(elm).hasClass();


    // Get the current computed height for the first element in the set of matched
    // elements or set the height of every matched element.
        $(elm).height();


    // Hide the matched elements.
        $(elm).hide();
        $(elmList).hide();

        elm.style.display = "none";
        elmList.forEach(item => item.style.display = "none");


    // Bind one or two handlers to the matched elements, to be executed when the
    // mouse pointer enters and leaves the elements.
        $(elm).hover(func);
        $(elmList).hover(func);

        elm.addEventListener("hover", func);
        elmList.forEach(item => item.addEventListener("hover", func));

        // --------------------------

        $(elm).hover();
        $(elmList).hover();

        let hover = new Event("hover");
        elm.dispatchEvent(hover);
        elmList.forEach(item => item.dispatchEvent(hover));


    // Get the HTML contents of the first element in the set of matched elements
    // or set the HTML contents of every matched element.
        $(elm).html(markupString);
        $(elmList).html(markupString);

        elm.innerHTML = markupString;
        elmList.forEach(item => item.innerHTML = markupString);


    // Search for a given element from among the matched elements.
        $(elm).index();


    // Get the current computed inner height (including padding but not border)
    // for the first element in the set of matched elements or set the inner height
    // of every matched element.
        $(elm).innerHeight();


    // Get the current computed inner width (including padding but not border)
    // for the first element in the set of matched elements or set the inner width
    // of every matched element.
        $(elm).innerWidth();


    // Insert every element in the set of matched elements after the target.
        $(elm).insertAfter();


    // Insert every element in the set of matched elements before the target.
        $(elm).insertBefore();


    // Check the current matched set of elements against a selector, element, or
    // jQuery object and return true if at least one of these elements matches
    // the given arguments.
        $(elm).is();


    // Bind an event handler to the “keydown” JavaScript event, or trigger that
    // event on an element.
        $(elm).keydown(func);
        $(elmList).keydown(func);

        elm.addEventListener("keydown", func);
        elmList.forEach(item => item.addEventListener("keydown", func));

        // --------------------------

        $(elm).keydown();
        $(elmList).keydown();

        let keydown = new Event("keydown");
        elm.dispatchEvent(keydown);
        elmList.forEach(item => item.dispatchEvent(keydown));


    // Bind an event handler to the “keypress” JavaScript event, or trigger that
    // event on an element.
        $(elm).keypress(func);
        $(elmList).keypress(func);

        elm.addEventListener("keypress", func);
        elmList.forEach(item => item.addEventListener("keypress", func));

        // --------------------------

        $(elm).keypress();
        $(elmList).keypress();

        let keypress = new Event("keypress");
        elm.dispatchEvent(keypress);
        elmList.forEach(item => item.dispatchEvent(keypress));


    // Bind an event handler to the “keyup” JavaScript event, or trigger that
    // event on an element.
        $(elm).keyup(func);
        $(elmList).keyup(func);

        elm.addEventListener("keyup", func);
        elmList.forEach(item => item.addEventListener("keyup", func));

        // --------------------------

        $(elm).keyup();
        $(elmList).keyup();

        let keyup = new Event("keyup");
        elm.dispatchEvent(keyup);
        elmList.forEach(item => item.dispatchEvent(keyup));


    // Reduce the set of matched elements to the final one in the set.
        $(elm).last();


    // Attach an event handler for all elements which match the current selector,
    // now and in the future.
        $(elm).live(eventName, func);
        $(elmList).live(eventName, func);

        elm.addEventListener(eventName, func);
        elmList.forEach(item => item.addEventListener(eventName, func));


    // Load data from the server and place the returned HTML into the matched
    // elements.
        $(elm).load();


    // Bind an event handler to the “load” JavaScript event.
        $(elm).load();


    // Pass each element in the current matched set through a function, producing
    // a new jQuery object containing the return values.
        $(elm).map();


    // Bind an event handler to the “mousedown” JavaScript event, or trigger that
    // event on an element.
        $(elm).mousedown(func);
        $(elmList).mousedown(func);

        elm.addEventListener("mousedown", func);
        elmList.forEach(item => item.addEventListener("mousedown", func));

        // --------------------------

        $(elm).mousedown();
        $(elmList).mousedown();

        let mousedown = new Event("mousedown");
        elm.dispatchEvent(mousedown);
        elmList.forEach(item => item.dispatchEvent(mousedown));


    // Bind an event handler to be fired when the mouse enters an element, or
    // trigger that handler on an element.
        $(elm).mouseenter(func);
        $(elmList).mouseenter(func);

        elm.addEventListener("mouseenter", func);
        elmList.forEach(item => item.addEventListener("mouseenter", func));

        // --------------------------

        $(elm).mouseenter();
        $(elmList).mouseenter();

        let mouseenter = new Event("mouseenter");
        elm.dispatchEvent(mouseenter);
        elmList.forEach(item => item.dispatchEvent(mouseenter));


    // Bind an event handler to be fired when the mouse leaves an element, or
    // trigger that handler on an element.
        $(elm).mouseleave(func);
        $(elmList).mouseleave(func);

        elm.addEventListener("mouseleave", func);
        elmList.forEach(item => item.addEventListener("mouseleave", func));

        // --------------------------

        $(elm).mouseleave();
        $(elmList).mouseleave();

        let mouseleave = new Event("mouseleave");
        elm.dispatchEvent(mouseleave);
        elmList.forEach(item => item.dispatchEvent(mouseleave));


    // Bind an event handler to the “mousemove” JavaScript event, or trigger that
    // event on an element.
        $(elm).mousemove(func);
        $(elmList).mousemove(func);

        elm.addEventListener("mousemove", func);
        elmList.forEach(item => item.addEventListener("mousemove", func));

        // --------------------------

        $(elm).mousemove();
        $(elmList).mousemove();

        let mousemove = new Event("mousemove");
        elm.dispatchEvent(mousemove);
        elmList.forEach(item => item.dispatchEvent(mousemove));


    // Bind an event handler to the “mouseout” JavaScript event, or trigger that
    // event on an element.
        $(elm).mouseout(func);
        $(elmList).mouseout(func);

        elm.addEventListener("mouseout", func);
        elmList.forEach(item => item.addEventListener("mouseout", func));

        // --------------------------

        $(elm).mouseout();
        $(elmList).mouseout();

        let mouseout = new Event("mouseout");
        elm.dispatchEvent(mouseout);
        elmList.forEach(item => item.dispatchEvent(mouseout));


    // Bind an event handler to the “mouseover” JavaScript event, or trigger that
    // event on an element.
        $(elm).mouseover(func);
        $(elmList).mouseover(func);

        elm.addEventListener("mouseover", func);
        elmList.forEach(item => item.addEventListener("mouseover", func));

        // --------------------------

        $(elm).mouseover();
        $(elmList).mouseover();

        let mouseover = new Event("mouseover");
        elm.dispatchEvent(mouseover);
        elmList.forEach(item => item.dispatchEvent(mouseover));


    // Bind an event handler to the “mouseup” JavaScript event, or trigger that
    // event on an element.
        $(elm).mouseup(func);
        $(elmList).mouseup(func);

        elm.addEventListener("mouseup", func);
        elmList.forEach(item => item.addEventListener("mouseup", func));

        // --------------------------

        $(elm).mouseup();
        $(elmList).mouseup();

        let mouseup = new Event("mouseup");
        elm.dispatchEvent(mouseup);
        elmList.forEach(item => item.dispatchEvent(mouseup));


    // Get the immediately following sibling of each element in the set of matched
    // elements. If a selector is provided, it retrieves the next sibling only if
    // it matches that selector.
        $(elm).next();


    // Get all following siblings of each element in the set of matched elements,
    // optionally filtered by a selector.
        $(elm).nextAll();


    // Get all following siblings of each element up to but not including the
    // element matched by the selector, DOM node, or jQuery object passed.
        $(elm).nextUntil();


    // Remove elements from the set of matched elements.
        $(elm).not();


    // Remove an event handler.
        $(elm).off();


    // Get the current coordinates of the first element, or set the coordinates
    // of every element, in the set of matched elements, relative to the document.
        $(elm).offset();


    // Get the closest ancestor element that is positioned.
        $(elm).offsetParent();


    // Attach an event handler function for one or more events to the selected elements.
        $(elm).on(eventName, func);
        $(elmList).on(eventName, func);

        elm.addEventListener(eventName, func);
        elmList.forEach(item => item.addEventListener(eventName, func));


    // Attach a handler to an event for the elements. The handler is executed at
    // most once per element per event type.
        $(elm).one(eventName, func);
        $(elmList).one(eventName, func);


    // Get the current computed outer height (including padding, border, and
    // optionally margin) for the first element in the set of matched elements
    // or set the outer height of every matched element.
        $(elm).outerHeight();


    // Get the current computed outer width (including padding, border, and
    // optionally margin) for the first element in the set of matched elements
    // or set the outer width of every matched element.
        $(elm).outerWidth();


    // Get the parent of each element in the current set of matched elements,
    // optionally filtered by a selector.
        $(elm).parent();


    // Get the ancestors of each element in the current set of matched elements,
    // optionally filtered by a selector.
        $(elm).parents();


    // Get the ancestors of each element in the current set of matched elements,
    // up to but not including the element matched by the selector, DOM node, or
    // jQuery object.
        $(elm).parentsUntil();


    // Get the current coordinates of the first element in the set of matched
    // elements, relative to the offset parent.
        $(elm).position();


    // Insert content, specified by the parameter, to the beginning of each
    // element in the set of matched elements.
        $(elm).prepend();


    // Insert every element in the set of matched elements to the beginning of
    // the target.
        $(elm).prependTo();


    // Get the immediately preceding sibling of each element in the set of matched
    // elements. If a selector is provided, it retrieves the previous sibling only
    // if it matches that selector.
        $(elm).prev();


    // Get all preceding siblings of each element in the set of matched elements,
    // optionally filtered by a selector.
        $(elm).prevAll();


    // Get all preceding siblings of each element up to but not including the
    // element matched by the selector, DOM node, or jQuery object.
        $(elm).prevUntil();


    // Return a Promise object to observe when all actions of a certain type
    // bound to the collection, queued or not, have finished.
        $(elm).promise();


    // Get the value of a property for the first element in the set of matched
    // elements or set one or more properties for every matched element.
        $(elm).prop();


    // Add a collection of DOM elements onto the jQuery stack.
        $(elm).pushStack();


    // Show or manipulate the queue of functions to be executed on the matched
    // elements.
        $(elm).queue();


    // Specify a function to execute when the DOM is fully loaded.
        $(elm).ready();


    // Remove the set of matched elements from the DOM.
        $(elm).remove();


    // Remove an attribute from each element in the set of matched elements.
        $(elm).removeAttr();


    // Remove a single class, multiple classes, or all classes from each element
    // in the set of matched elements.
        $(elm).removeClass();


    // Remove a previously-stored piece of data.
        $(elm).removeData();


    // Remove a property for the set of matched elements.
        $(elm).removeProp();


    // Replace each target element with the set of matched elements.
        $(elm).replaceAll();


    // Replace each element in the set of matched elements with the provided new
    // content and return the set of elements that was removed.
        $(elm).replaceWith();


    // Bind an event handler to the “resize” JavaScript event, or trigger that
    // event on an element.
        $(elm).resize(func);


    // Bind an event handler to the “scroll” JavaScript event, or trigger that
    // event on an element.
        $(elm).scroll(func);


    // Get the current horizontal position of the scroll bar for the first element
    // in the set of matched elements or set the horizontal position of the scroll
    // bar for every matched element.
        $(elm).scrollLeft();


    // Get the current vertical position of the scroll bar for the first element
    // in the set of matched elements or set the vertical position of the scroll
    // bar for every matched element.
        $(elm).scrollTop();


    // Bind an event handler to the “select” JavaScript event, or trigger that
    // event on an element.
        $(elm).select(func);


    // Encode a set of form elements as a string for submission.
        $(elm).serialize();


    // Encode a set of form elements as an array of names and values.
        $(elm).serializeArray();


    // Display the matched elements.
        $(elm).show();


    // Get the siblings of each element in the set of matched elements, optionally
    // filtered by a selector.
        $(elm).siblings();


    // Return the number of elements in the jQuery object.
        $(elm).size();


    // Reduce the set of matched elements to a subset specified by a range of indices.
        $(elm).slice();


    // Display the matched elements with a sliding motion.
        $(elm).slideDown();


    // Display or hide the matched elements with a sliding motion.
        $(elm).slideToggle();


    // Hide the matched elements with a sliding motion.
        $(elm).slideUp();


    // Stop the currently-running animation on the matched elements.
        $(elm).stop();


    // Bind an event handler to the “submit” JavaScript event, or trigger that
    // event on an element.
        $(elm).submit(func);


    // Get the combined text contents of each element in the set of matched elements,
    // including their descendants, or set the text contents of the matched elements.
        $(elm).text("any text");
        $(elmList).text("any text");

        elm.textContent = "any text";
        elmList.forEach(item => item.textContent = "any text");


    // Retrieve all the elements contained in the jQuery set, as an array.
        $(elm).toArray();


    // Display or hide the matched elements.
        $(elm).toggle();


    // Bind two or more handlers to the matched elements, to be executed on
    // alternate clicks.
        $(elm).toggle();


    // Add or remove one or more classes from each element in the set of matched
    // elements, depending on either the class’s presence or the value of the
    // state argument.
        $(elm).toggleClass();


    // Execute all handlers and behaviors attached to the matched elements for
    // the given event type.
        $(elm).trigger();


    // Execute all handlers attached to an element for an event.
        $(elm).triggerHandler();


    // Remove a previously-attached event handler from the elements.
        $(elm).unbind();


    // Remove a handler from the event for all elements which match the current
    // selector, based upon a specific set of root elements.
        $(elm).undelegate();


    // Bind an event handler to the “unload” JavaScript event.
        $(elm).unload();


    // Remove the parents of the set of matched elements from the DOM, leaving
    // the matched elements in their place.
        $(elm).unwrap();


    // Get the current value of the first element in the set of matched elements
    // or set the value of every matched element.
        $(elm).val();


    // Get the current computed width for the first element in the set of matched
    // elements or set the width of every matched element.
        $(elm).width();


    // Wrap an HTML structure around each element in the set of matched elements.
        $(elm).wrap();


    // Wrap an HTML structure around all elements in the set of matched elements.
        $(elm).wrapAll();


    // Wrap an HTML structure around the content of each element in the set of
    // matched elements.
        $(elm).wrapInner();


```
