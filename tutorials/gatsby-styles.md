# Gatsby Styles

## Ben Allan-Rahill

## Working with Styled Components (CSS-in-JS)

the documentation is [here](https://www.gatsbyjs.com/docs/styled-components/)

### Install plugins

```bash
npm install --save gatsby-plugin-styled-components styled-components babel-plugin-styled-components
```

### Gatsby-config.js

```js
module.exports = {
  plugins: [`gatsby-plugin-styled-components`],
};
```

### Create a component with styles

For example this creates an H1 with these styles

```js
const Title = styled.h1`
  font-family: sans-serif;
  font-weight: lighter;
  color: black;
`;
```
