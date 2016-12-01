# \<mf-ptjs\>

A Polymer Web Component wrapper for the PTJS library.

## How to use

Add the project to Bower:
```
bower install https://github.com/MentallyFriendly/mf-ptjs.git --save
```

Import the element:
```
<link rel="import" href="../bower_components/mf-ptjs/mf-ptjs.html">
```

Add the event handler attribute:
```
<div on-ptjsready="onPtjsReady">
    <mf-ptjs></mf-ptjs>
</div>
```

Add the event handler function:
```
onPtjsReady: function(e, detail) {
    var space = detail.space;
    var form = detail.form;
    var dot = new Circle(250, 250).setRadius(50);
    var another = new Circle(100, 100).setRadius(50);

    var bot = {
        animate: function(time, fs, context) {
            form.fill("#5AF").stroke(false);
            dot.setRadius(Math.abs(500 - time % 1000) / 50 + 50);
            form.circle(dot);
            form.fill(false).stroke("#fc0", 5);
            form.circle(another);

            var hits = another.intersectCircle(dot);

            if (hits.length > 0) {
                form.stroke("#fff").fill("#0C9");
                form.line(new Line(hits[0]).to(hits[1]));
                form.points(hits, 5, true);
            }
        },
        onMouseAction: function(type, x, y, evt) {
            if (type == 'move') {
                another.set(x, y);
            }
        }
    };

    space.add(bot);
    space.bindMouse();
    space.play();
},
```

## Development

### Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your application locally.

### Viewing the Component

```
$ polymer serve
```

### Building the Component

```
$ polymer build
```

This will create a `build/` folder with `bundled/` and `unbundled/` sub-folders
containing a bundled (Vulcanized) and unbundled builds, both run through HTML,
CSS, and JS optimizers.

You can serve the built versions by giving `polymer serve` a folder to serve
from:

```
$ polymer serve build/bundled
```

### Running Tests

```
$ polymer test
```

The component is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run the component's test suite locally.
