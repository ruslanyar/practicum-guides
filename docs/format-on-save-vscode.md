# Форматирование при сохранении в VS Code

Вы уже устанавливали `stylelint` и `prettier` в проект и настраивали `npm` скрипты для автоматического форматирования кода. Теперь давайте настроим редактор `VS Code` для форматирования при ручном сохранении файлов (Сtrl+S / Cmd+S).

## Предварительные требования

1. В проекте должны быть установлены и настроены `stylelint` и `prettier` (см. [Линтеры, форматтеры, автоматизация](https://practicum.yandex.ru/learn/fullstack-developer/courses/c519951c-3426-4496-8b50-89dcbb64b023/sprints/170251/topics/96b3fd16-5d4b-4721-ba0a-aa0c4a94615d/lessons/fc7a29bb-74b3-4963-aac1-6c26e2495e3a/) - курс fullstack, [Линтеры, форматтеры, автоматизация](https://practicum.yandex.ru/learn/frontend-developer/courses/738daf5a-b9fe-4bbe-800c-c43f30ebafd4/sprints/149449/topics/094f22ed-74be-4eb9-a626-5e37aa559901/lessons/31816616-1e88-4f0c-96ce-0424f6cb1463/) - курс frontend).

## Установка необходимых расширений для VS Code

Для реализации задуманного нам потребуются следующие расширения:

- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
- [Stylelint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
- [Format Code Action](https://marketplace.visualstudio.com/items?itemName=rohit-gohri.format-code-action)

Первые два позволят `VS Code` форматировать код посредством [`Code Actions`](https://code.visualstudio.com/docs/editor/refactoring#_code-actions-quick-fixes-and-refactorings), в соответствии с прописанными в кофигурационных файлах правилами и подсветят ошибки в коде. Последнее позволит настроить очерёдность выполнения `Code Actions` в `VS Code`.

## Настройка VS Code

Теперь перейдём к настройке `VS Code`.

1. Откроем конфигурационный файл `VS Code`. (`Ctrl+Shift+P / Cmd+Shift+P => Preferences: Open User Settings (JSON)`).
2. Сделаем Prettier дефолтным форматтером и отключаем форматирование при сохранении:

```json
// settings.json
{
  // ... другие настройки VS Code,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": false
}
```

3. Настроим `Code Actions` в зависимости от расширения файла.:

```json
// settings.json
{
  // ... другие настройки VS Code,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": false,
  // Для html файлов используем Code Action - Format Document
  // дефолтным форматтером, в качестве которого мы установили Prettier
  "[html]": {
    "editor.codeActionsOnSave": [
      "source.formatDocument",
    ]
  },
  // Для css и scss файлов также используем Prettier
  // и затем исправляем ошибки с помощью `Stylelint`
  "[css]": {
    "editor.codeActionsOnSave": [
      "source.formatDocument",
      "source.fixAll.stylelint"
    ]
  },
  "[scss]": {
    "editor.codeActionsOnSave": [
      "source.formatDocument",
      "source.fixAll.stylelint"
    ]
  }
}
```

4. Сохраняем конфигурационный файл и перезапускаем `VS Code`.

Теперь при нажатии `Ctrl+S / Cmd+S` `VS Code` будет форматировать код с помощью `Prettier` и исправлять ошибки с помощью `Stylelint`.
