# ProgressBar Component

`ProgressBar` — настраиваемый компонент прогресс-бара, построенный на **SVG** без использования сторонних библиотек. Поддерживает разные состояния и может отображаться в режиме дашборда.

## Demo

Демо сайт: [Progress Dashboard Demo](https://dashboard-widget.kolhovv.workers.dev)

## Props

| Prop         | Type                                                | Default        | Description |
|------------- |-----------------------------------------------------|----------------|-------------|
| `percentage` | `number`                                            | `0`            | Процент заполнения прогресс-бара (0–100). |
| `state`      | `'inProgress' \| 'success' \| 'warning' \| 'error'` | `'inProgress'` | Состояние прогресс-бара, влияет на цвет и стиль. |
| `dashboard`  | `boolean`                                           | `false`        | При включении изменяет стиль на вид дашборда. |

## States

- `inProgress` — бар в процессе заполнения.  
- `success` — успешно завершен.  
- `warning` — требует внимания.  
- `error` — произошла ошибка.  


