# QML Components

A growing collection of reusable UI components for **Qt Quick (QML)**.

Each component is a single `.qml` file with smooth animations and a modern dark look, ready to drop into a Qt 6 project.

## Components

| Component | Description |
|-----------|-------------|
| [`FloatingLabelInput`](FloatingLabelInput.qml) | Text input with a Material-style floating label, animated states and inline error messages |
| [`ErrorBanner`](ErrorBanner.qml) | Popup banner with a title, a message and an "Ok" button that slides in and out |
| [`ExitDialog`](ExitDialog.qml) | "Close the app?" confirmation dialog that dims and blurs the content behind it |
| [`NetworkStatusBanner`](NetworkStatusBanner.qml) | Collapsible strip that shows "No internet" / "Internet restored" and hides itself |

More components coming soon.

## Requirements

- Qt 6.x
- Modules: `QtQuick`, `QtQuick.Controls`, `QtQuick.Layouts`, `QtQuick.Window`, `QtQuick.Effects`

Some components also expect things that are not part of this repository — see the notes for each component below.

## Usage

1. Copy the `.qml` file(s) you need into your project.
2. Put them next to the QML files that use them, or register them in a QML module:

   ```cmake
   qt_add_qml_module(app
       URI MyApp
       QML_FILES
           Main.qml
           FloatingLabelInput.qml
   )
   ```

3. Use the component by its file name.

### FloatingLabelInput

```qml
FloatingLabelInput {
    id: email

    width: 300
    inputLabel.text: qsTr("Email")
}
```

Show or clear an error under the field with `error(isError, message)`:

```qml
email.error(true, qsTr("Invalid email address"))
email.error(false, "")
```

The error is cleared automatically when the text or focus changes.

| Alias | Target |
|-------|--------|
| `inputField` | the inner `TextField` (`inputField.text`, `inputField.echoMode`, …) |
| `inputLabel` | the floating label |
| `inputContainer` | the `Pane` around the field |
| `errorText` | the error message under the field |

Requires a `TextContextMenu` type (used for the right-click menu) to be available in your project; it is not included here.

### ErrorBanner

```qml
ErrorBanner {
    id: errorBanner

    anchors.horizontalCenter: parent.horizontalCenter
    anchors.bottom: parent.bottom
}
```

```qml
errorBanner.show(qsTr("Login failed"), qsTr("Check your email and password"))
```

The banner stays open until the user presses "Ok". Its width is capped at 40% of the window width, and long text is elided.

Requires the icon `qrc:/assets/circle_alert.svg`.

### ExitDialog

```qml
ExitDialog {
    id: exitDialog

    anchors.fill: parent
    content: mainContent
}
```

```qml
exitDialog.openManual()
exitDialog.closeManual()
```

"Exit" calls `Qt.quit()`; "Cancel" or a click outside the dialog closes it.

`content` is the item to blur while the dialog is open. It must have a `blurAmount` property (the dialog sets it to `1` on open and `0` on close) — bind it to your own blur effect, for example a `MultiEffect`. The inner `Popup` is available through the `dialog` alias.

### NetworkStatusBanner

```qml
NetworkStatusBanner {
    width: parent.width
}
```

The banner expands when the connection is lost, switches to "Internet restored" when it comes back, and collapses after 2 seconds.

This component is tied to the app it was written for: it imports `ParmigianoDesktop.CoreUI` and reads the state from a `UIStateManager` singleton. To reuse it, replace the import and provide an object with:

- a `networkStatusChanged(bool status)` signal
- a `getNetworkStatus()` method returning `bool`

Requires the icons `qrc:/assets/no_internet.svg` and `qrc:/assets/internet_restored.svg`.

## Customization

Where a component exposes its inner elements through property aliases, you can tweak text, fonts and behavior without editing the source file. Colors and sizes are otherwise defined inside each file — edit them there to match your theme.

## Contributing

Ideas, bug reports and pull requests are welcome.

## License

[MIT](LICENSE)
