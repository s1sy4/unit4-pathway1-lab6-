# Stages of the Activity lifecycle (Dessert Clicker)

Codelab: https://developer.android.com/codelabs/basic-android-kotlin-compose-activity-lifecycle

Стартовое приложение **Dessert Clicker**: нажатие на десерт «продаёт» его и увеличивает
количество проданных десертов и выручку. В задании добавлено логирование жизненного
цикла и исправлена потеря состояния при повороте экрана.

## Что сделано

- Добавлена константа `private const val TAG = "MainActivity"`.
- Переопределены все основные callbacks Activity и добавлены сообщения в Logcat:
  `onCreate`, `onStart`, `onResume`, `onRestart`, `onPause`, `onStop`, `onDestroy`.
- Проверены сценарии: запуск, выход по Back, уход на домашний экран и возврат,
  частичное перекрытие экраном Share, поворот устройства.
- Пять переменных состояния переведены с `remember` на `rememberSaveable`:
  `revenue`, `dessertsSold`, `currentDessertIndex`, `currentDessertPrice`,
  `currentDessertImageId` — данные больше не сбрасываются при configuration change.
- Добавлен импорт `android.util.Log`.

## Как смотреть логи

1. Запустить приложение.
2. Открыть вкладку **Logcat** в Android Studio.
3. Ввести фильтр `tag:MainActivity`.
4. Поворачивать эмулятор и сворачивать приложение — в логе будет видна
   последовательность `onPause → onStop → onDestroy → onCreate → onStart → onResume`.

## Структура

```
app/src/main/java/com/example/dessertclicker/
├── MainActivity.kt        # UI, lifecycle callbacks, rememberSaveable
├── data/Datasource.kt     # список десертов
├── model/Dessert.kt       # модель
└── ui/theme/              # тема приложения
```

## Запуск

Открыть папку `activity-lifecycle` в Android Studio и запустить `app`.
Минимальная версия Android — 24.

> Итоговый код соответствует официальной ветке `main`
> репозитория basic-android-kotlin-compose-training-dessert-clicker.
