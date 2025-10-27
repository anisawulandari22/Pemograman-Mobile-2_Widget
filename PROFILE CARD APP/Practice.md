# **MINI PROJEK: PROFILE CARD APP**

## **1. Struktur Project**

```
assets/images
 ├── flutter_logo.png
 ├── fonts/
 │    └── Poppins-Bold.ttf
 │    └── Poppins-Regular.ttf

lib/
 ├── main.dart
 ├── screens/
 │    └── profile_page.dart
 │    └── about_page.dart
 └── theme/
      └── app_theme.dart
```

---

## **2. File `app_theme.dart`**

```dart
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
```

---

## **3. File `profile_page.dart`**

```dart
import 'package:flutter/material.dart';

class ProfilePage extends StatefulWidget {
  const ProfilePage({super.key});

  @override
  State<ProfilePage> createState() => _ProfilePageState();
}

class _ProfilePageState extends State<ProfilePage> {
  late TextEditingController _nameController;
  late TextEditingController _emailController;
  late TextEditingController _phoneController;
  String title = 'Scrolling Engineer';
  String description = 'Scrol Fesnuk, Yapping';
  bool isEditing = false;

  @override
  void initState() {
    super.initState();
    // Inisialisasi controller dengan nilai awal
    _nameController = TextEditingController(text: 'Tekno');
    _emailController = TextEditingController(text: 'tekno@test.com');
    _phoneController = TextEditingController(text: '+62 812 3456 7890');
  }

  @override
  void dispose() {
    // Bersihkan controller saat widget dihapus
    _nameController.dispose();
    _emailController.dispose();
    _phoneController.dispose();
    super.dispose();
  }

  void _toggleEdit() {
    setState(() {
      isEditing = !isEditing;
    });
    // Simpan data jika mode edit dimatikan
    if (!isEditing) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('Data profil berhasil diperbarui!')),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
      child: Center(
        child: Card(
          elevation: 3,
          margin: const EdgeInsets.all(24),
          shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(16)),
          child: Padding(
            padding: const EdgeInsets.all(24),
            child: Column(
              mainAxisSize: MainAxisSize.min,
              children: [
                Image.asset('assets/images/flutter_logo.png', width: 100),
                const SizedBox(height: 16),

                // Nama (Dapat diubah)
                isEditing
                    ? TextField(
                        controller: _nameController,
                        decoration: const InputDecoration(labelText: 'Nama'),
                        textAlign: TextAlign.center,
                        style: Theme.of(context).textTheme.titleLarge,
                      )
                    : Text(_nameController.text, style: Theme.of(context).textTheme.titleLarge),

                Text(title, style: const TextStyle(color: Colors.grey)),
                const SizedBox(height: 8),
                Text(description, textAlign: TextAlign.center),
                const Divider(height: 30),

                // Form Email (Dapat diubah)
                TextField(
                  controller: _emailController,
                  decoration: const InputDecoration(
                    labelText: 'Email',
                    border: OutlineInputBorder(),
                    isDense: true,
                  ),
                  enabled: isEditing,
                  keyboardType: TextInputType.emailAddress,
                ),
                const SizedBox(height: 16),

                // Form Telepon (Dapat diubah)
                TextField(
                  controller: _phoneController,
                  decoration: const InputDecoration(
                    labelText: 'Telepon',
                    border: OutlineInputBorder(),
                    isDense: true,
                  ),
                  enabled: isEditing,
                  keyboardType: TextInputType.phone,
                ),
                const SizedBox(height: 24),

                // Tombol Edit/Simpan
                ElevatedButton.icon(
                  onPressed: _toggleEdit,
                  icon: Icon(isEditing ? Icons.save : Icons.edit),
                  label: Text(isEditing ? 'Simpan' : 'Ubah Data'),
                  style: ElevatedButton.styleFrom(
                    backgroundColor: Theme.of(context).primaryColor,
                    foregroundColor: Colors.white,
                  ),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

---

## **4. File `about_page.dart`**

```dart
import 'package:flutter/material.dart';

class AboutPage extends StatelessWidget {
  const AboutPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Tentang Aplikasi')),
      body: const Padding(
        padding: EdgeInsets.all(24),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Profile Card App',
              style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 12),
            Text(
              'Aplikasi ini dibuat untuk menampilkan kartu profil sederhana dengan fitur mengganti tema (gelap/terang), '
              'serta memungkinkan pengguna mengubah data profil seperti nama, email, dan nomor telepon secara langsung. '
              'Proyek ini juga mendemonstrasikan penggunaan StatefulWidget, Theme, dan Navigator.',
              textAlign: TextAlign.justify,
            ),
          ],
        ),
      ),
    );
  }
}

```

---

## **5. File `main.dart`**

```dart
import 'package:flutter/material.dart';
import 'screens/profile_page.dart';
import 'theme/app_theme.dart';

void main() {
  runApp(ProfileCardApp());
}

class ProfileCardApp extends StatefulWidget {
  @override
  State<ProfileCardApp> createState() => _ProfileCardAppState();
}

class _ProfileCardAppState extends State<ProfileCardApp> {
  bool isDark = false;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Profile Card App',
      theme: isDark ? AppTheme.darkTheme : AppTheme.lightTheme,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Profile Card App'),
          actions: [
            TextButton(
              onPressed: () {
                setState(() {
                  isDark = !isDark;
                });
              },
              child: Text(
                isDark ? 'Light' : 'Dark',
                style: TextStyle(color: Colors.white),
              ),
            ),
          ],
        ),
        body: ProfilePage(),
      ),
    );
  }
}

```
---

## **6. File `pubspec.yaml`**

```yaml
name: latihan_dasar_widgets
description: "A new Flutter project."
# The following line prevents the package from being accidentally published to
# pub.dev using `flutter pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev

# The following defines the version and build number for your application.
# A version number is three numbers separated by dots, like 1.2.43
# followed by an optional build number separated by a +.
# Both the version and the builder number may be overridden in flutter
# build by specifying --build-name and --build-number, respectively.
# In Android, build-name is used as versionName while build-number used as versionCode.
# Read more about Android versioning at https://developer.android.com/studio/publish/versioning
# In iOS, build-name is used as CFBundleShortVersionString while build-number is used as CFBundleVersion.
# Read more about iOS versioning at
# https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html
# In Windows, build-name is used as the major, minor, and patch parts
# of the product and file versions while build-number is used as the build suffix.
version: 1.0.0+1

environment:
  sdk: ^3.10.0-287.0.dev

# Dependencies specify other packages that your package needs in order to work.
# To automatically upgrade your package dependencies to the latest versions
# consider running `flutter pub upgrade --major-versions`. Alternatively,
# dependencies can be manually updated by changing the version numbers below to
# the latest version available on pub.dev. To see which dependencies have newer
# versions available, run `flutter pub outdated`.
dependencies:
  flutter:
    sdk: flutter

  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.8

dev_dependencies:
  flutter_test:
    sdk: flutter

  # The "flutter_lints" package below contains a set of recommended lints to
  # encourage good coding practices. The lint set provided by the package is
  # activated in the `analysis_options.yaml` file located at the root of your
  # package. See that file for information about deactivating specific lint
  # rules and activating additional ones.
  flutter_lints: ^6.0.0

# For information on the generic Dart part of this file, see the
# following page: https://dart.dev/tools/pub/pubspec

# The following section is specific to Flutter packages.
flutter:

  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true

  assets:
    - assets/images/flutter_logo.png

  fonts:
    - family: Poppins
      fonts:
        - asset: assets/images/fonts/Poppins-Regular.ttf
        - asset: assets/images/fonts/Poppins-Bold.ttf
          weight: 700

  # To add assets to your application, add an assets section, like this:
  # assets:
  #   - images/a_dot_burr.jpeg
  #   - images/a_dot_ham.jpeg

  # An image asset can refer to one or more resolution-specific "variants", see
  # https://flutter.dev/to/resolution-aware-images

  # For details regarding adding assets from package dependencies, see
  # https://flutter.dev/to/asset-from-package

  # To add custom fonts to your application, add a fonts section here,
  # in this "flutter" section. Each entry in this list should have a
  # "family" key with the font family name, and a "fonts" key with a
  # list giving the asset and other descriptors for the font. For
  # example:
  # fonts:
  #   - family: Schyler
  #     fonts:
  #       - asset: fonts/Schyler-Regular.ttf
  #       - asset: fonts/Schyler-Italic.ttf
  #         style: italic
  #   - family: Trajan Pro
  #     fonts:
  #       - asset: fonts/TrajanPro.ttf
  #       - asset: fonts/TrajanPro_Bold.ttf
  #         weight: 700
  #
  # For details regarding fonts from package dependencies,
  # see https://flutter.dev/to/font-from-package

---
