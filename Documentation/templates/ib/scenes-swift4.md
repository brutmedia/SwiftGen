## Template Information

| Name      | Description       |
| --------- | ----------------- |
| File name | ib/scenes-swift4.stencil |
| Invocation example | `swiftgen ib -t scenes-swift4 …` |
| Language | Swift 4 |
| Author | Olivier Halligon |

## When to use it

- When you need to generate *Swift 4* code for your storyboard *scenes*.
- The generated code supports both UIKit platforms (iOS, tvOS and watchOS) and AppKit platform (macOS).

## Customization

You can customize some elements of this template by overriding the following parameters when invoking `swiftgen` in the command line, using `--param <paramName>=<newValue>`

| Parameter Name | Default Value | Description |
| -------------- | ------------- | ----------- |
| `enumName` | `StoryboardScene` | Allows you to change the name of the generated `enum` containing all storyboard scenes. |
| `module` | N/A | By default, the template will import the needed modules for custom classes, but won’t import the target’s module to avoid an import warning — using the `PRODUCT_MODULE_NAME` environment variable to detect it. Should you need to ignore an additional module, you can provide it here. |
| `ignoreTargetModule` | N/A | Setting this parameter will disable the behaviour of prefixing classes with their module name for (only) the target module. |
| `publicAccess` | N/A | If set, the generated constants will be marked as `public`. Otherwise, they'll be declared `internal`. |

## Generated Code

Note: the generated code may look differently depending on the platform the storyboard file is targeting.

**Extract:**

```swift
enum StoryboardScene {
  enum Dependency: StoryboardType {
    static let storyboardName = "Dependency"

    static let dependent = SceneType<ExtraModule.ValidatePasswordViewController>(storyboard: Dependency.self, identifier: "Dependent")
  }
  enum Message: StoryboardType {
    static let storyboardName = "Message"

    internal static let initialScene = InitialSceneType<UIKit.UIViewController>(storyboard: Message.self)

    static let messagesList = SceneType<UITableViewController>(storyboard: Message.self, identifier: "MessagesList")
  }
}
```

[Full generated code](https://github.com/SwiftGen/templates/blob/master/Tests/Fixtures/Generated/IB-iOS/scenes-swift4-context-all.swift)

## Usage example

```swift
// You can instantiate scenes using the `instantiate` method:
let vc = StoryboardScene.Dependency.dependent.instantiate()

// The initial scene of a storyboard can be instantiated using:
let initial = StoryboardScene.Message.initialScene.instantiate()
```
