# DraggableBottomSheet

This is a bottom sheet that is partially visible onto the screen and can be dragged from there into the screen to occupy the fullscreen.

This package is adaptation of [draggable_bottom_sheet](https://pub.dev/packages/draggable_bottom_sheet) with added support for null safety.

## Get Started

Add to dependencies

```yaml
draggable_bottom_sheet_nullsafety: ^1.0.1
```

and import package

```dart
import 'package:draggable_bottom_sheet_nullsafety/draggable_bottom_sheet_nullsafety.dart';
```

## Arguments

Description of DraggableBottomSheet arguments.

| Argument           | Type        | Description                                                                                       |
| ------------------ | ----------- | ------------------------------------------------------------------------------------------------- |
| `backgroundWidget` | `Widget`    | This widget will hide behind the sheet when expanded.                                             |
| `previewChild`     | `Widget`    | Child to be displayed when sheet is not expended                                                  |
| `expandedChild`    | `Widget`    | Child of expended sheet                                                                           |
| `alignment`        | `Alignment` | Alignment of the sheet                                                                            |
| `blurBackground`   | `bool`      | Whether to blur the background while sheet expnasion (true: modal-sheet, false: persistent-sheet) |
| `expansionExtent`  | `double`    | Extent from the min-height to change from previewChild to expandedChild                           |
| `maxEntent`        | `double`    | Max-extent for sheetexpansion                                                                     |
| `minEntent`        | `double`    | Min-extent for the sheet, also the original height of the sheet                                   |
| `scrollDirection`  | `Axis`      | Scroll direction of the sheet                                                                     |

## Example

![Draggable Bottom Sheet gif](misc/ezgif.com-gif-maker.gif)

```dart
import 'package:draggable_bottom_sheet_nullsafety/draggable_bottom_sheet_nullsafety.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: const DraggableBottomSheetExample(
        title: 'Draggable Bottom Sheet Example',
      ),
      debugShowCheckedModeBanner: false,
    );
  }
}

class DraggableBottomSheetExample extends StatelessWidget {
  final String title;

  const DraggableBottomSheetExample({
    Key? key,
    required this.title,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    const List<IconData> icons = <IconData>[
      Icons.ac_unit,
      Icons.account_balance,
      Icons.adb,
      Icons.add_photo_alternate,
      Icons.format_line_spacing
    ];

    return Scaffold(
      body: DraggableBottomSheet(
        backgroundWidget: Scaffold(
          backgroundColor: Colors.white,
          appBar: AppBar(
            title: Text(title),
            backgroundColor: Colors.deepOrange,
          ),
          body: SizedBox(
            height: 400,
            child: ListView.separated(
              scrollDirection: Axis.horizontal,
              padding: const EdgeInsets.symmetric(vertical: 32),
              itemCount: icons.length,
              itemBuilder: (BuildContext context, int index) => Container(
                width: MediaQuery.of(context).size.width * 0.7,
                height: 200,
                decoration: BoxDecoration(
                  color: Colors.grey,
                  borderRadius: BorderRadius.circular(20),
                ),
                child: Icon(
                  icons[index],
                  color: Colors.white,
                  size: 60,
                ),
              ),
              separatorBuilder: (BuildContext context, int index) =>
                  const SizedBox(width: 10),
            ),
          ),
        ),
        previewChild: Container(
          padding: const EdgeInsets.all(16),
          decoration: const BoxDecoration(
            color: Colors.pink,
            borderRadius: BorderRadius.only(
              topLeft: Radius.circular(20),
              topRight: Radius.circular(20),
            ),
          ),
          child: Column(
            children: <Widget>[
              Container(
                width: 40,
                height: 6,
                decoration: BoxDecoration(
                  color: Colors.white,
                  borderRadius: BorderRadius.circular(10),
                ),
              ),
              const SizedBox(height: 8),
              const Text(
                'Drag Me',
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 16,
                  fontWeight: FontWeight.bold,
                ),
              ),
              const SizedBox(height: 16),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: icons.map((icon) {
                  return Container(
                    width: 50,
                    height: 50,
                    margin: const EdgeInsets.only(right: 16),
                    child: Icon(
                      icon,
                      color: Colors.pink,
                      size: 40,
                    ),
                    decoration: BoxDecoration(
                      color: Colors.white,
                      borderRadius: BorderRadius.circular(10),
                    ),
                  );
                }).toList(),
              )
            ],
          ),
        ),
        expandedChild: Container(
          padding: const EdgeInsets.all(16),
          decoration: const BoxDecoration(
            color: Colors.pink,
            borderRadius: BorderRadius.only(
              topLeft: Radius.circular(20),
              topRight: Radius.circular(20),
            ),
          ),
          child: Column(
            children: <Widget>[
              const Icon(
                Icons.keyboard_arrow_down,
                size: 30,
                color: Colors.white,
              ),
              const SizedBox(height: 8),
              const Text(
                'Hey...I\'m expanding!!!',
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 16,
                  fontWeight: FontWeight.bold,
                ),
              ),
              const SizedBox(height: 16),
              Expanded(
                child: GridView.builder(
                  itemCount: icons.length,
                  gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                    crossAxisCount: 2,
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                  ),
                  itemBuilder: (BuildContext context, int index) {
                    return Container(
                      decoration: BoxDecoration(
                        color: Colors.white,
                        borderRadius: BorderRadius.circular(10),
                      ),
                      child: Icon(
                        icons[index],
                        color: Colors.pink,
                        size: 40,
                      ),
                    );
                  },
                ),
              )
            ],
          ),
        ),
        minExtent: 150,
        maxExtent: MediaQuery.of(context).size.height * 0.8,
      ),
    );
  }
}
```
