# Writing Animation App

This Flutter application demonstrates a simple writing animation where text is gradually displayed on the screen, with each character being animated in a different color.

## Features

- Animated text display
- Multi-colored text animation

## Getting Started

These instructions will help you set up and run the project on your local machine.

### Prerequisites

- [Flutter](https://flutter.dev/docs/get-started/install) (version 2.0.0 or later)

### Installation

1. **Clone the repository:**

   ```sh
   git clone https://github.com/yourusername/writing_animation_app.git
   cd writing_animation_app
   ```

2. **Install dependencies:**

   ```sh
   flutter pub get
   ```

### Running the App

1. **Start an emulator or connect a physical device.**

2. **Run the app:**

   ```sh
   flutter run
   ```

## Code Overview

### Main Application

The main entry point of the application is defined in `main.dart`. The `MyApp` class sets up a basic `MaterialApp` with a `Scaffold` containing an `AppBar` and the `WritingAnimation` widget.

```dart
void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Writing Animation')),
        body: const Center(
          child: WritingAnimation(),
        ),
      ),
    );
  }
}
```

### Writing Animation Widget

The `WritingAnimation` widget is a `StatefulWidget` that manages the text animation.

```dart
class WritingAnimation extends StatefulWidget {
  const WritingAnimation({super.key});

  @override
  _WritingAnimationState createState() => _WritingAnimationState();
}
```

### State Management

The `_WritingAnimationState` class handles the animation using an `AnimationController` and an `IntTween` to animate the display of characters one by one.

```dart
class _WritingAnimationState extends State<WritingAnimation>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<int> _animation;

  final String _text = "Flutter is fun";
  final List<Color> _colors = [
    Colors.red, Colors.orange, Colors.yellow, Colors.green, Colors.blue,
    Colors.indigo, Colors.purple, Colors.pink, Colors.teal, Colors.brown,
    Colors.cyan, Colors.lime, Colors.amber, Colors.deepOrange,
  ];

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 3),
      vsync: this,
    );
    _animation = IntTween(begin: 0, end: _text.length).animate(_controller)
      ..addListener(() {
        setState(() {});
      });
    _controller.forward();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return RichText(
      text: TextSpan(
        style: const TextStyle(fontSize: 32.0),
        children: _buildTextSpans(),
      ),
    );
  }

  List<TextSpan> _buildTextSpans() {
    List<TextSpan> textSpans = [];
    for (int i = 0; i < _animation.value; i++) {
      textSpans.add(
        TextSpan(
          text: _text[i],
          style: TextStyle(color: _colors[i % _colors.length]),
        ),
      );
    }
    return textSpans;
  }
}
```

### Animation Details

- The animation lasts for 3 seconds (`Duration(seconds: 3)`).
- The `IntTween` animates the length of the text being displayed.
- Each character is assigned a color from the `_colors` list in a cyclic manner.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- [Flutter](https://flutter.dev) for providing an amazing framework to build cross-platform apps.
- [Google](https://google.com) for the Material Design guidelines and components.
