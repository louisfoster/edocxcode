# edocxcode

Starter for creating documentation projects/modules/tutes in xcode. It is primarily for scenekit-based projects.


## Reqs

- Swift 4
- Xcode 9
- iOS 11
- Git, Cocoapods, Jekyll


## Setup

But for now, it has some simple instructions to reference for when setting up my projects a certain way.

1. Create a new repo in github, create it with a `readme` and `.gitignore` for swift
2. Open terminal, clone repo to your code directory
3. Open root directory and `mkdir docs ios`
4. Ensure jekyll is installed and add the `Gemfile`, `_config.xml` and `index.md` from this repo to the project's `docs` directory
4. Run `bundle install` to setup the docs site server and assets, run `bundle exec jekyll serve` to view the site locally at [localhost:4000](http://localhost:4000/)
5. Open Xcode and create a single page ios project in the ios directory, give it any name and don't initialise with version control
6. Remove the main storyboard file and remove its entry from the `info.plist` file
7. Add an Asset catalogue named `art.scnassets`
8. Remove contents of `AppDelegate` class and add this:
```swift
var window: UIWindow?

var mainViewController: MainViewController?

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {

    self.window = UIWindow(frame: UIScreen.main.bounds)

    self.mainViewController = MainViewController()

    self.window?.rootViewController = self.mainViewController

    self.window?.makeKeyAndVisible()

    return true
}
```
9. Create a new group called `Main` and add a cocoa touch file, a UIViewController with xib named `MainViewController`
10. Add a scenekit view to the Main xib
11. Create an outlet to the view in the Main class file
12. Add a scene, camera, light, object to the view and setup the view (running this should load with no problems)
13. Exit xcode, return to the newly created xcode directory in the ios directory
14. Ensure cocoapods is installed and run `pod init`
15. In the newly created `Podfile` add these lines directly under the `# Pods for <project name>` line:
```ruby
inhibit_all_warnings!
pod 'SwiftLint'
```
15. Run `pod install`
16. Add the `.swiftlint.yml` file to the directory
17. In the newly created xcworkspace directory, open the contents.xcworkspacedata file and in the <Workspace..> tag add this item:
```xml
<FileRef
    location = "group:.swiftlint.yml">
</FileRef>
```
18. Open the xcode workspace: `open <project name>.xcworkspace`
19. In the main project's `Build Phases` after the `Check Pods..` entry add a new `Run Script..` with this line: `"${PODS_ROOT}/SwiftLint/swiftlint"`
20. Build the project, lint errors should now be visible (if there are any). Project should also run as before.
22. Add these lines to the `.gitignore` for preventing future commiting of unnecessary items (yes I understand the irony of repeating certain lines in this file unnecessarily but I was having issues with not including certain file and don't have time to figure it out):
```
.idea
docs/_site
xcuserdata
*/xcuserdata/*
.DS_Store
*.xcuserdata*
*xcworkspace/xcuserdata/*
*.blend1
*.kra-autosave.kra
.DS_Store
*.app.dSYM.zip
build/
*.xcuserdatad
xcuserdata
Pods/
*.ipa
*.xcuserstate
*.xcworkspace/xcuserdata/*.xcuserdatad/
*/*.xcodeproj/xcuserdata/
fastlane/report.xml
```
23. In the root directory, run `git add .` and commit+push all the new stuff
24. Back in github, go to settings, github pages -> source -> master branch /docs folder, then save.


## Future

This project _should_ evolve over time to include:

- readme
    - install xcode template, create projects+workspace in ios dir
    - run docs script
    - setup new git and repo w/ docs setting
- docs dir basic setup w/ gemfile
- xcode template
- .gitignore for swift etc
- script for checking/getting jekyll for docs & running gemfile
- one script to rule them all?
