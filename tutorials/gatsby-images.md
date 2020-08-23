# Adding Images to A Gatsby Site

## Ben Allan-Rahill

Taken from [here](https://egghead.io/lessons/gatsby-use-gatsby-image-with-an-image-from-a-relative-path?pl=using-gatsby-image-with-gatsby-ea85129e)

### Install Packages

First install these packages using npm:

1. gatsby-image
2. gatsby-source-filesystem
3. gatsby-plugin-sharp
4. gatsby-transformer-sharp

_e.g._

```bash
npm i --save gatsby-image
```

### Gatsby-config.js

The gatsby and sharp plugins need to be included in the `Gatsby-config.js`

The file system plugin needs to be told where the images are. For me that is usually in src/images

```js
"gatsby-transformer-sharp",
  "gatsby-plugin-sharp",
  {
    resolve: "gatsby-source-filesystem",
    options: {
      name: "images",
      path: "${__dirname}/src/images",
    },
  };
```

### Restart the server

```bash
gatsby develope
```

## Importing a Local Image into a Gatsby Component with webpack

1. Import into component using path
2. Pass import to the `src` attr of the regular `<Img>` tag

```js
import Logo from "../images/plain@0.5x.png"

img src={Logo} style={{ width: 200 }} alt="The logo" />
```

## Use gatsby-image with an image from a relative path
