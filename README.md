# React Native Schemes Manager

XCode environments without the stress. Use XCode schemes with React Native without pulling your hair out.

[![Supported by Thinkmill](https://thinkmill.github.io/badge/heart.svg)](http://thinkmill.com.au/?utm_source=github&utm_medium=badge&utm_campaign=react-native-schemes-manager)

If your app has multiple environments, you'd probably like to be able to manage these the way native developers have been doing for years, XCode schemes and build configurations.

By default, React Native doesn't handle these particularly well, and the ability to launch dev tools or run in debug mode is impacted. This package fixes these problems.

*Made by [Kevin Brown](https://twitter.com/kevinbrowntech), supported by [Thinkmill](http://thinkmill.com.au/). Thank you for making this project possible!*

## Installation

```
yarn add --dev react-native-schemes-manager
```
or
```
npm install --save-dev react-native-schemes-manager
```

Once the package is installed in your project, you just need to configure it by adding a `schemes` section to your `package.json` and adding a `postinstall` script which will re-run the script whenever you add or remove packages to/from your project:

```json
{
  "name": "your-awesome-app",
  "version": "1.0.0",
	"scripts": {
		"postinstall": "react-native-schemes-manager all"
	},
  "xcodeSchemes": {
      "Debug": ["Staging", "Preflight"]
  }
}
```

This configuration will copy the "Debug" build configuration to "Staging" and "Preflight" build configurations in all your dependent library projects.

## What Then?

The package is able to do three things:
- Swap its own version of react-native-xcode.sh in instead of the stock on that assumes all debug schemes are named 'Debug'.
- Add your build configurations to all library xcode projects.
- Hide any schemes that come from your library projects so they don't show up in the menu.

As long as `react-native-schemes-manager all` has run whenever you add react native modules, you should be good to go.

## It's not working!

A good starting point for troubleshooting is:
- Completely quit XCode.
- `rm -rf node_modules`
- `yarn` or `npm i`
- Re open XCode
- Product -> Clean
- Run

If you're still having trouble, post an issue so we can look into it.

## Running Manually

You can run the three parts of this package on demand by running either:

- `react-native-schemes-manager fix-libraries`: Adds your build configurations to all library xcode projects.
- `react-native-schemes-manager fix-script`: Swaps a schemes aware build script in instead of the stock react native one.
- `react-native-schemes-manager hide-library-schemes`: Hides any build schemes that come from your node_modules folder xcodeproj files as you don't usually want to see them anyway.

And of course you can run all 3 easily if you'd prefer:

- `react-native-schemes-manager all`: Runs all the scripts above.

The best way to give yourself a manual trigger for this is add to your `package.json` scripts section like so:

```json
{
  "name": "your-awesome-app",
  "version": "1.0.0",
  "scripts": {
      "fix-xcode": "react-native-schemes-manager all",
      "postinstall": "react-native-schemes-manager all"
  }
}
```

You can then `yarn run fix-xcode` or `npm run fix-xcode` which will run the cleanup scripts on demand.

## Further Reading

These are some great articles about related topics in case you're hungry for more:

- [📝 Migrating iOS App Through Multiple Environments](http://www.blackdogfoundry.com/blog/migrating-ios-app-through-multiple-environments/): Explains how XCode is handling this situation in a detailed way.
- [📝 How to set up multiple schemes & configurations in Xcode for your React Native iOS app](https://zeemee.engineering/how-to-set-up-multiple-schemes-configurations-in-xcode-for-your-react-native-ios-app-7da4b5237966#.vsq9mlgv8): The inspiration and approach for this package, unfortunately written in Ruby. I wanted a pure Node build pipeline and I didn't want to have to muck around with per package configuration.

## License

Licensed under the MIT License, Copyright © 2017 Kevin Brown.

See [LICENSE](./LICENSE) for more information.

## Acknowledgements

This project builds on a lot of earlier work by clever folks all around the world. We'd like to thank Alek Hurst and Craig Edwards who contributed ideas and inspiration, without which this project woudln't have been possible.
