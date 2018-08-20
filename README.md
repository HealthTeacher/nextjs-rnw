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

- Using the `commonjs: true` for [`babel-plugin-react-native-web`](https://github.com/necolas/react-native-web/tree/master/packages/babel-plugin-react-native-web#usage) rather than compiling `react-native-web` with webpack fixes the missing styles (i.e. revert [this change](https://github.com/HealthTeacher/nextjs-rnw/commit/b0a9843c1b490f3a5d0ce6f7b0edff8626e24b8b)).
