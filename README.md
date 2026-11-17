# ViewModel and State in Compose + Unit tests (Unscramble)

Codelabs:

- https://developer.android.com/codelabs/basic-android-kotlin-compose-viewmodel-and-state
- https://developer.android.com/codelabs/basic-android-kotlin-compose-test-viewmodel

Игра **Unscramble**: нужно угадать слово, буквы которого перемешаны. В проект добавлены
ViewModel, UI-состояние и модульные тесты.

## Что сделано

- Создан `GameUiState` — неизменяемый класс состояния экрана
  (перемешанное слово, счёт, номер слова, флаги ошибки и окончания игры).
- Создан `GameViewModel`:
  - состояние хранится в `MutableStateFlow`, наружу отдаётся `StateFlow`;
  - `resetGame()` очищает игру и выбирает первое слово;
  - `updateUserGuess()` сохраняет ввод пользователя;
  - `checkUserGuess()` проверяет ответ, начисляет `SCORE_INCREASE` (20) и переходит
    к следующему слову или завершает игру;
  - `skipWord()` пропускает слово без изменения счёта;
  - `pickRandomWordAndShuffle()` не повторяет слова и гарантирует, что перемешанное
    слово отличается от исходного.
- `GameScreen` получает ViewModel через `viewModel()`, подписывается на состояние
  через `collectAsState()` и передаёт события в ViewModel.
- Добавлены тестовые зависимости: `junit:junit:4.13.2`, тестовый source set
  с `WordsData.kt` и функцией `getUnscrambledWord()`.
- Написаны 5 модульных тестов (`GameViewModelTest`):
  1. `gameViewModel_Initialization_FirstWordLoaded` — начальное состояние;
  2. `gameViewModel_IncorrectGuess_ErrorFlagSet` — неверный ответ;
  3. `gameViewModel_CorrectWordGuessed_ScoreUpdatedAndErrorFlagUnset` — верный ответ;
  4. `gameViewModel_WordSkipped_ScoreUnchangedAndWordCountIncreased` — пропуск слова;
  5. `gameViewModel_AllWordsGuessed_UiStateUpdatedCorrectly` — конец игры после 10 слов.

## Запуск

Открыть папку `unscramble` в Android Studio и запустить `app`.

Модульные тесты:

```bash
./gradlew testDebugUnitTest
```

Или в Android Studio: правый клик по `GameViewModelTest.kt` → **Run 'GameViewModelTest'**.
Для отчёта по покрытию — **Run with Coverage**.

## Структура

```
app/src/main/java/com/example/unscramble/
├── MainActivity.kt
├── data/WordsData.kt
├── ui/GameScreen.kt
├── ui/GameUiState.kt
├── ui/GameViewModel.kt
└── ui/theme/
app/src/test/java/com/example/unscramble/
├── data/WordsData.kt
└── ui/test/GameViewModelTest.kt
```

> Итоговый код соответствует официальной ветке `main`
> репозитория basic-android-kotlin-compose-training-unscramble.
