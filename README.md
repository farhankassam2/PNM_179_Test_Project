# PNM_179_Test_Project

This repository should be primarily used to reproduce the issue desribed in this Github issue link: https://github.com/facebook/react-native/issues/30221. Since our project is confidential and material cannot be shared publicly, I wanted to reproduce the bug I was experiencing linking the `react-native-branch` npm package with a sample RN project public repo, which can be used for testing and reproducing of the issue.

In this sample repo, I simply underwent the process of initializing a new react native project using the basic CLI commands provided by React, with iOS being the target. After that, I followed the following steps to link the `react-native-branch` package:

pod deintegrate
rm Podfile
yarn add react-native-branch
react-native link react-native-branch
git checkout -- Podfile
pod install

A word of note is that I followed the above steps as a workaround for another bug with linking the branch package mentioned above. I am manually linking the package using `react-native link react-native-branch` because the way the package is structured is slightly outdated as it was created before React 0.60 was released. Please refer to this Github comment for further details: https://github.com/BranchMetrics/react-native-branch-deep-linking-attribution/issues/361#issuecomment-415149270.

After doing the above, RNBranch.h was successfully linked to the this fresh react native project. 

Now to reproduce the issue, follow the steps below precisely:
1) Ensure you have the necessary tools installed globally such as `node` and `npm` as well as `cocoapods` and `watchman`. If you do not have any of these installed, you can follow the steps highlighted in [HERE](https://reactnative.dev/docs/0.60/getting-started) up until you reach "React Native Command Line Interface".
2) Ensure that you have these pods in the `Podfile`: 
`  pod 'react-native-branch', path: '../node_modules/react-native-branch'
   pod 'Branch'
`
3) If you did not have them before for some reason, run `pod install` from within the `ios` directory.
4) Navigate to the project's `ios` directory in your finder and open up `PNM_179_Test_Project.xcworkspace` using `Xcode 11.4`.
5) Make sure you have `Generic iOS Device` selected as the device on which to build.
6) Run `Product > Clean Build Folder` from the menu at the top.
7) Run `Product > Archive ` or `Product > Build` from the menu at the top. The `RCTLog.h file not found` error should be visible after you tap on the red exclamation mark at the top right. Due to this, the build will fail.
8) Or instead of steps 5-7 above, simply change the target device to an `iPhone X`, `iPhone 8` or for that matter, any other device simulator.
9) Click on the run triangle at the top left to build and then run the current scheme. Once again, the `RCTLog.h file not found` error should be visible and will cause the build to fail.


Thank you.
