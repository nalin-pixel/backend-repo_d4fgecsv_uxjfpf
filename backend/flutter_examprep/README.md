# ExamPrep (Flutter)

An offline-first exam preparation mobile app for Android and iOS.

Features
- Learning mode: one question at a time, instant feedback, explanation, bookmark-ready structure
- Exam Simulation: timed, randomized questions, score and breakdown
- Question bank: JSON format, unlimited categories
- Progress tracking: tests taken, accuracy per category, improvement over time
- Localization: Serbian (default) and English
- Admin: simple export of current questions to JSON (import path described below)

Project structure (key parts)
- assets/i18n: en.json, sr.json
- assets/questions: questions_sr.json (default), questions_en.json
- lib/src/models: Question, AnswerOption, TestResult
- lib/src/screens: Home, Learning, Simulation, Results, Progress, Settings, Admin
- lib/src/services: LocalizationService, QuestionRepository, StorageService

Run locally
1. Install Flutter SDK (3.19+ recommended).
2. From the `flutter_examprep` folder run:
   - flutter pub get
   - flutter run

Build APK
- flutter build apk --release
- The APK will be in build/app/outputs/flutter-apk/app-release.apk

Build iOS (requires Xcode/macOS)
- flutter build ios --release
- Open ios/Runner.xcworkspace in Xcode to archive and sign

Replace questions with your own
1. Open assets/questions/questions_sr.json (default language). The format is:
```
[
  {
    "id": "q-unique-id",
    "category": "Matematika",
    "text": "Tekst pitanja",
    "options": [
      {"id": "a", "text": "Odgovor A"},
      {"id": "b", "text": "Odgovor B"},
      {"id": "c", "text": "Odgovor C"}
    ],
    "correctId": "b",
    "explanation": "Kratko objašnjenje"
  }
]
```
2. Add as many questions and categories as you wish. Keep 3–5 options per question.
3. For English, mirror the data in assets/questions/questions_en.json.
4. After editing, run `flutter pub get` (hot reload will pick changes in debug; for release rebuild the app).

CSV Import/Export (manual path)
- Export: Use Admin screen Export to create `examprep_export.json` in your device documents folder.
- Import: For now, place your JSON into `assets/questions/questions_sr.json` and rebuild. Optional CSV import can be added later.

Localization
- Default language is Serbian. Change text in assets/i18n/sr.json.
- Add languages by creating `assets/i18n/<code>.json` and wiring it in `MaterialApp.supportedLocales`.

Notes
- All content is bundled and works offline.
- Progress is stored locally with Hive.
