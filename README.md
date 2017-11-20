# js-helpers
Some Javascript Helpers that I use day to day



### VUE.JS HELPERS
```
// Register All Components
import * as Components from "./components/**/*";
Object.values(Components).map( (component) => component.name && Vue.component( component.name, component ) );
```


### JAVASCRIPT HELPERS

```
// GET / SET TEXT
const $_text = ( _this, me ) => ( newval = '' ) => {

    // if new val is null
    // return this innerHTML
    if ( newval === '' ) return _this.e.innerHTML;

    // otherwise set the new text
    _this.e.innerHTML = newval;

    return me;

};
```

```
// GET / SET VAL
const $_val = ( _this, me ) => ( newval = undefined ) => {

    // if new val is undefined
    // return this val
    if ( newval === undefined ) return _this.e.value;

    // otherwise set the new val
    _this.e.value = newval;

    return me;

};
```

```
// ADD CLASS HELPER
const $_addClass = ( _this, me ) => (cls) => {

    let elements = _this.e;

    elements.forEach(el => {

        el.classList.add(cls);

    });

    return me
};
```
```

// REMOVE CLASS HELPER
const $_removeClass = ( _this, me ) => (cls) => {

    let elements = _this.e;

    elements.forEach(el => {

        el.classList.remove(cls);

    });

    return me;
};
```

```

// ADD / REMOVE CLASSES TO SIBLINGS
const $_siblings = ( _this, me ) => (action, cls) => {


    let elements = _this.e;

    if( !action || action != 'addClass' &&  action != 'removeClass'){

        return `[[ ALERT ]] Action must be 'addClass' or 'removeClass' -> $(el).siblings('addClass', 'my-super-class')`;

    }


    elements.forEach(e => {

        let el = e.parentNode.firstChild;

        // While the first child has next siblings
        do {

            // If action = addCLass => lest add the class
            if( action && action == 'addClass') el.classList.add(cls);

            // If action = removeCLass => lest remove the class
            if( action && action == 'removeClass') el.classList.remove(cls);

        } while (el = el.nextSibling);

    });


    return me;

};

```
```

// QUERY SELECT ELEMENT
const getBySelector = ( selector, context = document ) => Array.prototype.slice.call( context.querySelectorAll( selector ) );


// EMULATES JQUERY's $ FUNCTION
function $$ ( selector ) {

    this.e = getBySelector( selector );

    let me = this;

    if ( this.e.length === 1 ) this.e = this.e[ 0 ];


    this.siblings = $_siblings( this , me );

    // TEXT
    this.text = $_text( this , me );

    // VAL
    this.val = $_val( this , me );

    // ADD CLASS
    this.addClass = $_addClass( this , me );

    // REMOVE CLASS
    this.removeClass = $_removeClass( this , me );

    return this; //  <- Important
}
```
```
const $ = ( selector ) => new $$( selector );
```
