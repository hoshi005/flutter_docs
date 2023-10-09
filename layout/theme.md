# Theme

## Themeの設定方法

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: _themeData(Brightness.light),
      darkTheme: _themeData(Brightness.dark),
      home: const ThemeSampleHomeWidget(),
    );
  }
}

ThemeData _themeData(Brightness brightness) {
  final colorScheme = ColorScheme.fromSeed(
    seedColor: Colors.deepPurple,
    brightness: brightness,
  );
  return ThemeData(
    brightness: brightness,
    colorScheme: colorScheme,
    appBarTheme: AppBarTheme(
      backgroundColor: colorScheme.inversePrimary,
    ),
    useMaterial3: true,
    scaffoldBackgroundColor: colorScheme.background,
  );
}
```