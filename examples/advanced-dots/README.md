# Dots Example

The dots example renders an amount of dots into the body of the `index.html`.
There the base background color is configured over a variable `$background-color`.
With every dot, the background color has to be lighten a bit.

## Given:

- The HTML structure

      <html lang="en"><head>
        <title>Dots Example</title>
        ...
      </head>
        <body>
          <div class="dot dot--0"></div>
          <div class="dot dot--1"></div>
          <div class="dot dot--2"></div>
          <div class="dot dot--3"></div>
          ....
        </body>
      </html>

  Here a class selector `.dot` is used to define the overall structure of a dot.
  Than additional class selectors like `dot--0` are used to apply the background color to a dot. This class-selectors (`dot--0`, `dot--1`, `dot--3`, ....) have to be used within the `.scss` to apply the design to the dots.


## Steps to go:

1. Download the [index.html](https://github.com/marymar/sass-workshop/blob/master/examples/dots/index.html) into your own `examples/dots` folder.

2. Create a Sass file called `dots.scss` in the same folder where the `index.html` is.

3. Put the following code into the `dots.scss`.

        .dot {
          background-color: #ccc;
          border-radius: 50%;
          display: inline-block;
          height: 2em;
          margin: 1em;
          width: 2em;
        }

        .dot--0 {
          background-color: #090;
        }

3. Open your console and go into your example folder `examples/dots`.

4. Start your Sass watch task with `sass --watch --scss *.scss`.
It watches your Sass file and generates the css if the `.scss` changes.

3. Rewrite the `.dot` selector, which defines the dot.
It should use a variable `$dot-size`, which can be used for `width` and `height` instead of `2em`.

4. Do the same for the margin and define a variable for setting the size of the dot margin.
The margin should always be a quarter of the dot size `$dot-size`. You can do calculations in Sass, i.g. `$dot-size/4` and that has to be assigned to the new margin variable. You are free to name the margin variable as you want.

5. The background color has to be arranged now in a way, so that the background color with each dot lightens a bit.
There are `10` dots in the `index.html` which needs to lighten.
To lighten a background color a bit just use addition `+`, e.g. `background-color: $background-color + 1;`


    We could come around with the following solution, just by enhancing the `dots.scss` with following:

        .dot--0 {
          background-color: $background-color + 10;
        }
        .dot--1 {
          background-color: $background-color + 20;
        }
        .dot--2 {
          background-color: $background-color + 30;
        }
        .dot--3 {
          background-color: $background-color + 40;
        }
        ...

    That would be the normal css approach. But with Sass you have the advantage to write loops. To do that you can use the `@for`directive.

    The loop goes from `0` to `10`. The step is normally `1`. To use the current number in the loop, we define a new variable in the `@for` statement. It is called `$i` in this example. But you are free to use your own prefered name. This variable name can then be used within the loop. It contains always the current loop step.

        @for $i from 0 through 10 {
          ...
        }

    Within the loop we need to define our css rule for the background colors.
    All class selectors which defines each dots background colors start with `.dot--` and at the end the number is set, e.g. `dot--1`.

    You can use the `$i` variable for it. But to use it within a css rule you have to interpolate this variable. Otherwise it couldn't be used for defining the class selectors name. Interpolation in Sass is done with `#{}`. In our example you have to use it that way: `dot--#{$i}`

    Your code should now look close to this:

        .dot {
          background-color: #ccc;
          border-radius: 50%;
          display: inline-block;
          height: 2em;
          margin: 1em;
          width: 2em;
        }

        @for $i from 0 through 10 {
          .dot--#{$i} {
            background-color: $background-color;
          }
        }

    If so, all dots would still have the same color. You still need to do something with the background color. You need to calculate the background color in every loop step to lighten the background color for every dot.
    We could use our `$i` again and add `$i` to the background color:

        background-color: $background-color + $i * 10;

    The factor `10` is used here, to make the color changes better visible.

6. Try to nest the whole `@for` part into the `.dot` and use the parent-selector `&` within the the class selector for the rules of each dot, defined within the `@for'.

        .dot {
          ....
          @for {
            &--#{$i} {
              background-color: .....;
            }
          }
        }

## Result of `dots.scss`

Finished? Than your `dots.scss` might look similar to that:

    $color-start: #060;
    $dot-size: 2em;
    $dot-space: $dot-size / 4;
    $color-shift: 1;

    .dot {
      background-color: #ccc;
      border-radius: 50%;
      display: inline-block;
      height: $dot-size;
      margin: $dot-space;
      width: $dot-size;

      @for $i from 0 through 10 {
        &--#{$i} {
          background-color: $color-start + $i * 10;
        }
      }
    }
