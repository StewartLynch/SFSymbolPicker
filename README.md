# SFSymbolPicker

`SFSymbolPicker` is a Swift Package that provides a customizable UI component for browsing and selecting [Apple's SF Symbols](https://developer.apple.com/sf-symbols/). This package includes access to symbol metadata and offers flexible presentation options for symbol pickers.

## 📦 Installation

You can add `SFSymbolPicker` to your project using [Swift Package Manager](https://swift.org/package-manager/).

### In Xcode:

1. Open your project.
2. Go to **File > Add Packages…**
3. Enter the package URL:
   ```
   https://github.com/StewartLynch/SFSymbolPicker
   ```
4. Select the version range you want to use (recommend "Up to Next Major").
5. Import `SFSymbolPicker` in the files where you need it:
   ```swift
   import SFSymbolPicker
   ```
6. Each presenting view must instantiate an instance of the SymbolLoader class as a @State property or be able to fetch it from the Environment as this is passed on to the SymbolView when being presented.

   ```swift
   @State private var loader = SymbolLoader()
   ```

---

## 🧩 Features

- ✅ Access thousands of SF Symbols across multiple categories.
- ✅ Filter symbols by category or custom arrays of categories.
- ✅ Present the picker as a modal sheet or popover.
- ✅ Includes built-in search for symbols and terms.
- ✅ Customize behavior to match your UI needs.

---

## 🚀 Usage

Here's a quick example of how to use `SFSymbolPicker`:

### Presenting the Symbol Picker

```swift
import SFSymbolPicker

@State private var allCategoriesImage = "square.grid.2x2" // Symbol to update
@State private var showPicker = false
@State private var loader = SymbolLoader()

var body: some View {
    VStack {
        Button("Pick a Symbol") {
            showPicker = true
        }
    }
    .sheet(isPresented: $showPicker) {
        SymbolPickerView(
            loader: loader
            selectedSymbol: $allCategoriesImage
        )
    }
}
```

### Customizing Categories

You can restrict the symbols shown using  specific category filters:

```swift
SymbolView(
    loader: loader,
    selectedSymbol: $mixedCategoriesImage,
    limitedCategories: [.transportation, .objectsandtools]
)
```

Or use just one specific category:

```swift
SymbolView(
    loader: loader,
    selectedSymbol: $singleCategoryImage,
    limitedCategories: [.human]
)
```

### Search Terms

Or provide your own search term and pass that in as a String:

```swift
SymbolView(
    loader: loader,
    selectedSymbol: $searchTermImage,
    searchTerm: "sport"
)
```

### Presenting as a Popover

Instead of a sheet presentation, you may wish to present the picker as a popover.

On iOS this requires the `.presentationCompactAdaptation(.popover)` modifier

```swift
.popover(isPresented: $showSingle) {
    SymbolView(
        loader: loader,
        selectedSymbol: $singleCategoryImage,
        limitedCategories: [.human]
    )
    .frame(width: 300, height: 300)
    .presentationCompactAdaptation(.popover)
}
```

---

## 🔍 Requirements

- iOS 18+, iPadOS 18+, macOS 15+
- Xcode 16+
- Swift 5.10+

---

## 📁 Included Resources

This package includes the following resources:

- `categories.plist`
- `name_availability.plist`
- `symbol_categories.plist`
- `symbol_search.plist`

These are decoded internally to provide metadata and search capability for SF Symbols.

---

## 💻 Demo App

This repository includes a fully working **demo app** to showcase how to use `SFSymbolPicker` in a real SwiftUI project.

### How to run it

1. Clone this repository:

   ```bash
   git clone https://github.com/StewartLynch/SFSymbolPicker.git
   ```

2. Open the demo app project:

   ```
   DemoApp/SFSymbolPickerDemo/SFSymbolPickerDemo.xcodeproj
   ```

3. Select a simulator or your device and build & run.

The demo app illustrates multiple use cases, including presenting the picker as a sheet or popover, and filtering by category or search term.  
Feel free to explore or modify it to experiment with different configurations.

## 

## 📄 License

This project is licensed under the MIT License.

---

## 🔗 More Info

To learn how this package was built and how to customize it, check out the accompanying [YouTube tutorial](https://youtu.be/mdQqWy0Vk_w) by [@StewartLynch](https://github.com/StewartLynch).
