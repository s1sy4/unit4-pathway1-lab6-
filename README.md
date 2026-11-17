# Practice: Add a ViewModel to Dessert Clicker

Codelab: https://developer.android.com/codelabs/basic-android-kotlin-compose-practice-viewmodel

Практика по переносу состояния и логики из `MainActivity` в ViewModel.

## Что сделано

- Создан `DessertUiState` — состояние экрана: индекс текущего десерта, количество
  проданных десертов, выручка, цена и изображение текущего десерта.
- Создан `DessertViewModel`:
  - состояние хранится в `MutableStateFlow` и отдаётся как `StateFlow`;
  - `onDessertClicked()` увеличивает количество продаж и выручку, выбирает следующий
    десерт по `startProductionAmount`;
  - `determineDessertIndex()` определяет, какой десерт показывать дальше.
- В `MainActivity`/`DessertClickerApp` удалены локальные переменные состояния и логика
  продажи; UI получает данные из `dessertUiState` через `collectAsState()`.
- Подключена зависимость `androidx.lifecycle:lifecycle-viewmodel-compose`
  и `viewModel()` для создания ViewModel.

## Структура

```
app/src/main/java/com/example/dessertclicker/
├── MainActivity.kt          # UI, подписка на состояние ViewModel
├── ui/DessertViewModel.kt   # данные и бизнес-логика
├── data/DessertUiState.kt   # UI-состояние
├── data/Datasource.kt       # список десертов
├── model/Dessert.kt
└── ui/theme/
```

## Запуск

Открыть папку `dessert-clicker-viewmodel` в Android Studio и запустить `app`.
При повороте экрана количество проданных десертов и выручка сохраняются.

> Итоговый код соответствует официальной ветке `viewmodel`
> репозитория basic-android-kotlin-compose-training-dessert-clicker.
> Проект использует Groovy-сборку; при необходимости Android Studio предложит
> обновить Gradle/AGP.
