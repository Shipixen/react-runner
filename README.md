# React Runner

Run your React code on the go [https://react-runner.vercel.app](https://react-runner.vercel.app)

## Features

- Inline element
- Function component
- Class component, **with class fields support**
- Composing components with `render` or `export default`
- Server Side Rendering
- `import` statement
- [Multi files](https://react-runner.vercel.app/#multi-files)
- Typescript

With React Runner, you can write your live code in the real world way, check out Hacker News [in react-runner](https://react-runner.vercel.app/#hacker-news) vs [in real world](https://react-runner.vercel.app/examples/hacker-news), with the same code

You can even build your own async runner to support dynamic imports, try [Play React](https://play-react.vercel.app)

## Install

```bash
# Yarn
yarn add react-runner

# NPM
npm install --save react-runner
```

## Options

- **code** `string`, _required_ the code to be ran
- **scope** `object` globals that could be used in `code`

## Usage

```jsx
import { Runner } from 'react-runner'

const element = <Runner code={code} scope={scope} onRendered={handleRendered} />
```

or use hook `useRunner` with cache support

```jsx
import { useRunner } from 'react-runner'

const { element, error } = useRunner({ code, scope })
```

### `import` statement and multi files

```js
import { importCode } from 'react-runner'
import * as YourPkg from 'your-pkg'

const baseScope = {
  /* base globals */
}

const scope = {
  ...baseScope,
  // scope used by import statement
  import: {
    constants: { A: 'a' },
    'your-pkg': YourPkg,
    './local-file': importCode(localFileContent, baseScope),
  },
}
```

then in your live code you can import them

```js
import { A } from 'constants'
import Foo, { Bar } from 'your-pkg'
import What, { Ever } from './local-file'

export default function Demo() {
  /* render */
}
```

## Browser support

```
"browserslist": [
  "Chrome > 61",
  "Edge > 16",
  "Firefox > 60",
  "Safari > 10.1"
]
```

## Resources

- [Play React](https://play-react.vercel.app/)
- [CodeMirror for React Runner](https://react-runner-codemirror.vercel.app/)
- [Storybook Addon](https://storybook.js.org/addons/storybook-addon-react-runner/)

## react-live-runner

`react-runner` is inspired by [react-live](https://github.com/FormidableLabs/react-live) heavily,
I love it, but I love arrow functions for event handlers instead of bind them manually as well as other modern features,
and I don't want to change my code to be compliant with restrictions, so I created this project,
use [Sucrase](https://github.com/alangpierce/sucrase) instead of [Bublé](https://github.com/bublejs/buble) to transpile the code.

If you are using `react-live` in your project and want a smooth transition, `react-live-runner` is there for you which provide the identical way to play with, and `react-live-runner` re-exports `react-runner` so you can use everything in `react-runner` by importing `react-live-runner`

```jsx
import {
  LiveProvider,
  LiveEditor,
  LiveError,
  LivePreview,
} from 'react-live-runner'

...
<LiveProvider code={code} scope={scope}>
  <LiveEditor />
  <LivePreview />
  <LiveError />
</LiveProvider>
...
```

or hooks for better custom rendering

```jsx
import { useLiveRunner, CodeEditor } from 'react-live-runner'

const { element, error, code, onChange } = useLiveRunner({
  initialCode,
  scope,
  transformCode,
})

...
<>
  <CodeEditor value={code} onChange={onChange}>
  <div>{element}</div>
  {error && <pre>{error}</pre>}
</>
...
```

or use `react-runner` directly

```jsx
import { useState, useEffect } from 'react'
import { useRunner } from 'react-runner'

const [code, onChange] = useState(initialCode)
const { element, error } = useRunner({ code, scope })

useEffect(() => {
  onChange(initialCode)
}, [initialCode])

...
<>
  <textarea value={code} onChange={event => onChange(event.target.value)}>
  <div>{element}</div>
  {error && <pre>{error}</pre>}
</>
...
```

Check the real world usage here https://github.com/nihgwu/react-runner/blob/master/website/src/components/LiveRunner.tsx

## License

MIT © [Neo Nie](https://github.com/nihgwu)


-----------------

Save 100s of hours of work by using Page AI to generate a beautiful website. In just minutes!

| | |
| :- | :- |
| <a href="https://pageai.pro" target="_blank"><img height="60px" src="https://pageai.pro/static/images/logo-square.png" alt="Page AI Logo" /></a> <br/> <b>Page AI</b> <br/> AI Website Generator that designs and writes clean code. <br/><br/> Try the app on <a href="https://pageai.pro">pageai.pro</a>. | <a href="https://pageai.pro" target="_blank"><img width="300px" src="https://user-images.githubusercontent.com/1515742/281077548-57b24773-3c2a-4e89-b088-cc3945d7037b.png" alt="Page AI Logo" /></a> |

-----------------

Apihustle is a collection of tools to test, improve and get to know your API inside and out. <br/>
[apihustle.com](https://apihustle.com) <br/>

|                                                                                                                                                                                        |              |                                                          |                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------- | :------------------------------------------------------- | :------------------------------------------- |
| <a href="https://pageai.pro" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/9bfbfe6f-add9-45de-aaf2-5c6043a47e41" alt="Page AI Logo" /></a>        | **Page AI**  | AI Website Generator that designs and writes clean code. | [pageai.pro](https://pageai.pro)             |
| <a href="https://shipixen.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/e1deba72-328e-4d3c-9c62-11ab77184561" alt="Shipixen Logo" /></a>     | **Shipixen** | Create a personalized blog & landing page in minutes     | [shipixen.com](https://shipixen.com)         |
| <a href="https://pageui.dev" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/b8815b62-598a-4fca-bc27-c03e66c8b105" alt="Page UI Logo" /></a>        | **Page UI**  | Landing page UI components for React & Next.js           | [pageui.dev](https://pageui.dev)             |
| <a href="https://clobbr.app" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/cb3e64e2-efaa-436b-ae6d-0ea4b47e4004" alt="Clobbr Logo" /></a>         | **Clobbr**   | Load test your API endpoints.                            | [clobbr.app](https://clobbr.app)             |
| <a href="https://crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/38a3d734-d1ca-4f92-9cfb-ada52b9f2ffb" alt="Crontap Logo" /></a>       | **Crontap**  | Schedule API calls using cron syntax.                    | [crontap.com](https://crontap.com)           |
| <a href="https://tool.crontap.com" target="_blank"><img  width="54px" src="https://github.com/user-attachments/assets/545f7618-ff2c-47fa-ad17-e17e38155f55" alt="CronTool Logo" /></a> | **CronTool** | Debug multiple cron expressions on a calendar.           | [tool.crontap.com](https://tool.crontap.com) |

-----------------

<a href="https://apihustle.com" target="_blank">
  <img height="60px" src="https://user-images.githubusercontent.com/1515742/215217833-c07183d2-f688-4d1c-86ea-329f3b28f81c.svg" alt="Apihustle Logo" />
</a>

-----------------

