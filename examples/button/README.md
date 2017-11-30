# Button Example
The Button example contains different kinds of buttons and links which looks like an button.
In this example you will learn, how  button could be styled and what pseudo classes are and how to use these.

## Given
- The HTML structure

        <!DOCTYPE html>
        <html lang="en">

          <head>
            <title>Button Example</title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <link href="button.css" rel="stylesheet">
          </head>
          <body>

            <button class="button">klick mich</button>

          </body>
        </html>

The button uses the `.button` class selector.

## Steps to go:

1. Create a `button-example` folder and a file called `index.html` within the `button-example` folder.
2. Put the given html content above into te `index.html`and save.
3. Besides the html file we need the `button.scss` in the same folder. The button.scss will be compiled by the sass compiler to the resulting `button.css`, which is actually referenced in the `index.html`.
4. Now we need to style our button in the page. It uses the `.button`
Therefore it is needed to define a new rule called `.button` in the `button.scss`.

        .button {
          ...
        }

5. To apply more space between the text in the button and the corner set a padding for button to 1em.
6. Apply your preferred `background-color` to the button. The color itself should be defined within a variable `$button-color1`, because we want to reuse the color later on.
7. You should also define the text colour in the same manner. Name the second color variable e.g. `$button-color2`.
Your `button.scss`should look like that now:

        $button-color1: #e6e6e6;
        $button-color2: #d00ddd;

        .button {
          background-color: $button-color1;
          color: $button-color2;
          padding: 1em;
        }

8. Now, define a second button `.button-secondary`, where the background has the color of `$button-color2` and the text color of `$button-color1` and put your new button below your first in the html.

        <body>
            <button class="button">klick mich</button>
            <button class="button-secondary">klick mich 2</button>
        </body>

9. To use the hand instead of the arrow for the mouse icon, we have to use the property `cursor` and set it to `pointer`.

10. Let's apply now the design of our button, then the mouse is hovering it.

    Here we need to understand what `pseudo classes` are handy for.
    You can find here and introduction: https://developer.mozilla.org/Learn/CSS/Introduction_to_CSS/Pseudo-classes_and_pseudo-elements.

    Exchange the `background-color` with the color from `.button` then hovering this element and vise versa.

    Your `.scss` should now look like that:

      .button {
        background-color: $button-color1;
        color: $button-color2;
        cursor: pointer;
        padding: 1em;

        &:hover {
          background-color: $button-color2;
          color: $button-color1;
        }
      }


## References

- https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/
- https://developer.mozilla.org/Learn/CSS/Introduction_to_CSS/Pseudo-classes_and_pseudo-elements
