# QML Components

A growing collection of reusable, customizable UI components for **Qt Quick (QML)**.

Each component is a self-contained `.qml` file with smooth animations and a modern dark look, ready to drop into any Qt 6 project.

## Components

| Component | Description |
|-----------|-------------|
| [`FloatingLabelInput`](FloatingLabelInput.qml) | Text input with a Material-style floating label, animated states and inline error messages |

More components coming soon.

## Requirements

- Qt 6.x
- Modules: `QtQuick`, `QtQuick.Controls`, `QtQuick.Layouts`

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

3. Use the component by its file name:

   ```qml
   FloatingLabelInput {
       width: 300
       inputLabel.text: qsTr("Email")
   }
   ```

## Customization

Components expose their inner elements through property aliases, so you can tweak colors, fonts, sizes and behavior without editing the source files.

## Contributing

Ideas, bug reports and pull requests are welcome.
