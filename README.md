# animatedModal.js
animatedModal.js is a javascript plugin to create a fullscreen modal with CSS3 transitions. You can use the transitions from animate.css or create your own transitions.
This is a fork of [João Pereira's jquery plugin](http://joaopereirawd.github.io/animatedModal.js/) without the need for jQuery.
It also brings basic IE9 support (without animations) and modals can be closed using the escape key.

_Note that I've removed a lot of the inline styling that the original jQuery plugin added. As such you'll need to do a little more work to get it operational, trade off means more control regarding styling._

## Installation

If you're rocking bower then `bower install jsanimatedmodal --save`

Otherwise either clone or download to add to your project like any other javascript file.

## Usage

#### HTML
Whatever element you're using for the modal you'll likely want to add `animated` and `animated-modal` classes by default.

    <div id="your-modal" class="animated animated-modal">
        <div class="close-modal">Close</div>
        <!-- your content -->
    </div>

#### CSS
If you plan to use with [Dan Eden's animate css](https://github.com/daneden/animate.css) (which you do) then you'll need to include animate.css
If you're rocking libsass then checkout Tom Gillard's [Sass port](https://github.com/tgdev/animate-sass).

The following is required for hiding and showing the modal.

    .animated-modal {
        animation-duration: 0.5s;
        background-color: rgb(57, 190, 185);
        height: 100%;
        left: 0;
        opacity: 0;
        overflow-y: auto;
        position: fixed;
        top: 0;
        visibility: hidden;
        width: 100%;
        z-index: -10;
    }

    .animated-modal-on {
        opacity: 1;
        visibility: visible;
        z-index: 10;
    }


#### Javascript
First create an instance of a modal and supply your [Options].

    var modal = new AnimatedModal({
        color:'#39BEB9'
    });

Then use a click event attached to an element to open the modal.

    document.getElementById('my-modal-button').addEventListener('click', function(ev) {
        ev.preventDefault();
        modal.open();
    });

## Options
The following options can be declared when creating a new AnimatedModal:

    animatedIn: 'zoomIn', // the animate.css / animation class name to apply for open animation.
    animatedOut: 'zoomOut', // the animate.css / animation class name to apply for close animation.
    closeBtn: '.close-modal', // A reference to the element in your content that closes the modal.
    // closeBtn can be false to handle closing externally e.g. using a framework like Knockout.
    modalBaseClass: 'animated-modal', // used for applying 'on' and 'off' classes to the modal
    modalTarget: 'animated-modal', // the ID of the modal or a DOM element.

## Callbacks
The following callbacks are available:

    afterClose: null, // function to fire when the animation has completed on close
    afterOpen: null, // function to fire when the animation has completed on open
    beforeClose: null, // function to fire before the close animation starts
    beforeOpen: null, // function to fire before the open animation starts
    escClose: null, // function to fire on esc key close.
