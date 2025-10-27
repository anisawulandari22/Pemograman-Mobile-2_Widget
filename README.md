1. Struktur Project
lib/
 ├── main.dart
 ├── screens/
 │    └── profile_page.dart
 │    └── about_page.dart
 └── theme/
      └── app_theme.dart

2. File app_theme.dart
import 'package:flutter/material.dart';

class AppTheme {
  static final lightTheme = ThemeData(
    brightness: Brightness.light,
    primarySwatch: Colors.teal,
    fontFamily: 'Poppins',
  );

  static final darkTheme = ThemeData(
    brightness: Brightness.dark,
    primarySwatch: Colors.teal,
    fontFamily: 'Poppins',
  );
}
