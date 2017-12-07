# Icon Link
In this example you learn how to use links with an icon in front of it.
You will learn to extend your css rule by further rules and to include mixins into your css rule.

For this example you need a static webserver, otherwise the webfonts wouldn't be loaded. You can use ruby for it which actually is installed on your system.


## Given

- The HTML structure

        <!DOCTYPE html>
        <html lang="en">

          <head>
            <title>Icon Link Example</title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <link href="main.css" rel="stylesheet">
          </head>
          <body>
            <a href="mailto:mary@vomar.de">Send me a mail.</a>
          </body>
        </html>

## Steps to go:

1. Create a new project folder named `icon-link`.

2. Create the `index.html` with the html content given here above.

3. Download the font-awesome from http://fontawesome.io/ into the `icon-link` folder and extract the folder.
It should now contain a folder called `font-awesome-4.7.0` or similar.

3. Create a `main.scss` and import the `font-awesome.scss` from `font-awesome-4.7.0/scss/`
    Additional to that, you have to reset the fonts path of the awesome fonts.
    The fonts are stored under `font-awesome-4.7.0/fonts;`. To reference the right folder you have to reset the fonts path with `$fa-font-path: './font-awesome-4.7.0/fonts';` before you include the font awesome.

    The main.scss should look like that:

            $fa-font-path: './font-awesome-4.7.0/fonts';
            @import 'font-awesome-4.7.0/scss/font-awesome.scss';


4. Start the sass watch task from the console: `sass --watch --scss [scss-file]`
It should generate the `main.css`in the same folder and it should now contain all the css from font-awesome.

5. Now try to use one of those icons (i.g. the mail/envelope icon `fa-envelope`).
    The easiest way to do, is to just use the icon provided by font-awesome directly in a class. For instance you could add a span into the link, where you set the icon class selector for.

    To get started with font awesome check out: http://fontawesome.io/get-started/

    You can find the proper class names in the cheatsheet of font awesome: http://fontawesome.io/cheatsheet/

    Maybe your code of the link looks now like that:

      <a href="mailto:mary@vomar.de" class="link">
        <span class="fa fa-envelope"></span>
        Send me a mail.</a>

    To see the result in the browser we need to access the index.html via localhost. To do so, go into your examples folder `icon-link` and type `ruby -run -e httpd -- -p 8000 .` After the server started you can open `http://localhost:8000` in your browser and you should see your mail link.

    Here you used used directly the font awesome classes directly.
    But you can also use your rules which extends the font awesome rules within sass, so that you would only use your own class names in html (see next steps).

6. Now, you don't want to use the additional span in your link, but you want extend your link class, which is used in the link itself.
    You have to use the `@extends` directive from sass (http://sass-lang.com/documentation/file.SASS_REFERENCE.html#_extend__extend).

    Your code might look now like this one. Here a second rule is used, to just apply the envelope before the link text.

      `html`:

        <a href="mailto:mary@vomar.de" class="link link--envelope">
          Send me a mail.</a>

      `scss`:

        .link {
          &::before {
            @extend .fa;
          }

          &--envelope {
            @extend .fa-envelope;
          }
        }

    Look into the compiled code. What you will see, that your class was actually added to the rules of font-awesome itself. So you extended the font awesome rules.

        ...
        .fa-envelope:before, .link--envelope:before {content: ""; }
        ...

7. Instead of using the `@extend` sass provides also the directive `@mixin`. Mixins are used by font awesome too.
    You can just use one mixin called `fa-icon();` from font awesome to define a third link class rule `.link-mail` which uses the mixin from font awesome directly.

    Additional to that you also need to define the content for your pseudo element `::before`. Here you can access the variable `$fa-var-envelope` also defined within the `sass` implementation of font awesome.

    More about the directive `@mixin` you can find here:
    http://sass-lang.com/documentation/file.SASS_REFERENCE.html#Including_a_Mixin___include__including_a_mixin

    Your code might look like that now:

      `html`:

          <a href="mailto:mary@vomar.de" class="link-mail">
            Send me a third mail.</a>

      `scss`:

        .link-mail {
          @include fa-icon();

          &::before {
            content: $fa-var-envelope;
          }
        }
