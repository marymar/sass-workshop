# Dots Example

The dots example renders an amount of dots into the body of the `index.html`.
There the base background color is configured over a variable.
With every dot, the background color has to be lighten a bit.

_Steps to go:_

1. Download the [index.html](https://github.com/marymar/sass-workshop/blob/master/examples/dots/index.html) into your own examples/dots folder.
It generates some dots, when document is ready. So that you only have to worry about the Sass.

2. Create a Sass file called `dots.scss` in the same folder where the index.html is.

3. Start your Sass watch task with `sass --watch --scss *.scss` within your examples/dots. It watches all Sass files and generates the css if the `.scss` changes.

3. Write the `.dot` selector, which defines the dot.

    - It should have a size of `2em` and a margin in all direction of quarter of `2em`. Try to use variables therefore.
    - To get a well rounded dot use `border-radius with 50%`. Don't forget to set the display property properly.
    - The background color should be managable over a variable too.

    Now you should have a lot of dots all of the same background color.

4. The background color has to be arranged now in a way, so that the background color with each dot lightens a bit.
    To get this done, we need two addional things. We have to define, how many dots we want to lighten and then we need a loop, which generates the selector, which actually is used in the `index.html`

    - Define the variable `$amount` and set it to 150.

    - Now we need to use a `for`-loop to loop from `0` to `$amount` and within the loop to define a selector, which just set the background  color of a specific dot. Here we use the BEM syntax and introduce a — so called — modifier,
    e.g.: `.dot--1`.


          @for $i from 0 through $amount {
            ...
          }

      Keep in mind using the nesting together with the parent-selector `&`.

          .dot {
            ....

            @for $i from 0 through $amount {
              &--#{$i} {
                background-color: .....;
              }
            }
          }

      To lighten a background-color a bit just use addition `+`, e.g. `background-color: $color + 1;`


5. If you made it so far. Try to add a nice keyframe animation to the dots.
