# eslint-indent-range
repro of eslint indent rule bug

see [eslint#8893](https://github.com/eslint/eslint/issues/8893)

```
PS> .\node_modules\.bin\eslint .\index.js

Cannot read property 'range' of undefined
TypeError: Cannot read property 'range' of undefined
    at SourceCode.getTokensBetween (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\token-store\index.js:557:17)
    at parenPairs.forEach.pair (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\rules\indent.js:932:68)
    at Array.forEach (native)
    at addParensIndent (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\rules\indent.js:926:24)
    at Linter.Program:exit (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\rules\indent.js:1379:17)
    at emitOne (events.js:115:13)
    at Linter.emit (events.js:210:7)
    at NodeEventGenerator.applySelector (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\util\node-event-generator.js:265:26)
    at NodeEventGenerator.applySelectors (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\util\node-event-generator.js:294:22)
    at NodeEventGenerator.leaveNode (C:\Users\peet\git\eslint-indent-range\node_modules\eslint\lib\util\node-event-generator.js:317:14)
```

## pre-reduced code
<details>
<summary>Code</summary>

```js

const rgbToHex = rgb => `#${rgb.map(x => {
  const hex = x.toString(16);
  return hex.length === 1 ? `0${hex}` : hex;
}).join('')}`;

function addOpacity(color, coefficient, ...args) {
  if (typeof color !== 'string') {
    throw new Error('color should be a string');
  }
  const opacity = limit(coefficient, 0, 1);

  let hex;
  if (testHexColor.test(color)) {
    hex = color;
  } else {
    hex = lookupColor(color, args);
  }

  const hex6 = colorToHex6(hex);
  const rgb = hexToRgb(hex6);

  return `rgba(${rgb[0]}, ${rgb[1]}, ${rgb[2]}, ${opacity})`;
}

```

</details>
