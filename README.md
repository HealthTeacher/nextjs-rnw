# nextjs-rnw

Test case for integrating [Next.js](https://github.com/zeit/next.js) and [`react-native-web`](https://github.com/necolas/react-native-web). The current approach breaks server rendering the critical styles.

## Steps to Reproduce

1.  Clone this repository.
1.  `yarn install`
1.  `yarn start`
1.  Open http://localhost:3000
1.  Disable JavaScript in your browser.
1.  Refresh the page.

## Expected Result

The "critical" styles for the page are rendered by the server.

## Actual Result

The "critical" styles for the page are missing.

## Notes

- This seems related to [a previous `react-native-web` issue](https://github.com/necolas/react-native-web/issues/778#issuecomment-360385264), but I am failing to determine how to properly integrate Next.js as [the app renderer](https://github.com/necolas/react-native-web/issues/778#issuecomment-360704308).
- Next.js provides a way to define a [custom document](https://github.com/zeit/next.js#custom-document) that is often utilized integrate CSS-in-JS server rendering (e.g. [style-components](https://github.com/zeit/next.js/blob/canary/examples/with-styled-components/pages/_document.js#L7), [glamorous](https://github.com/zeit/next.js/blob/canary/examples/with-glamorous/pages/_document.js#L7), [emotion](https://github.com/zeit/next.js/blob/canary/examples/with-emotion/pages/_document.js#L7), [aphrodite](https://github.com/zeit/next.js/blob/canary/examples/with-aphrodite/pages/_document.js#L6)).
- Server rendered styles worked prior to the `react-native-web` [changing the default exports to ES6 modules in `0.7.0`](https://github.com/necolas/react-native-web/releases/tag/0.7.0).
- Using the `commonjs: true` for [`babel-plugin-react-native-web`](https://github.com/necolas/react-native-web/tree/master/packages/babel-plugin-react-native-web#usage) rather than compiling `react-native-web` with webpack fixes the missing styles (i.e. revert [this change](https://github.com/HealthTeacher/nextjs-rnw/commit/b0a9843c1b490f3a5d0ce6f7b0edff8626e24b8b)).
