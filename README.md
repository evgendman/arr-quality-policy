# arr-quality-policy

Универсальная политика отбора релизов для Radarr и Sonarr. Основной принцип: **разделять выбор целевого качества/разрешения и оценку дополнительных свойств релиза**.

## Путь от концепции к конфигурации

1. **[Универсальная модель качества и Custom Formats](docs/policy-model.md)** — разделение Quality Profile и Custom Formats, независимость каталога от 1080p/2160p, смысл префиксов, диапазоны баллов и их обоснование.
2. **Группы Custom Formats** — полные таблицы имён, весов и условий распознавания:
   - [Voice](docs/custom-formats/voice.md) — 41 формат озвучек, дубляжа, студий и дорожек; regex и оценки.
   - [Src](docs/custom-formats/sources.md) — источники, Blu-ray/DVD Disk и различия условий Radarr/Sonarr.
   - [Format](docs/custom-formats/video-formats.md) — HDR, HDR10, HDR10+, Dolby Vision и DV8.1.
   - [Extra](docs/custom-formats/extras.md) — HEVC/H.265 и Theatrical.
3. **[Реализация в Radarr](docs/implementations/radarr.md)** и **[реализация в Sonarr](docs/implementations/sonarr.md)** — сервисные особенности и состав JSON-каталогов.
4. **[Recyclarr](docs/recyclarr.md)** — JSON-архивы, YAML, settings providers, secrets и безопасный порядок Preview/Sync.

## Актуальные каталоги Recyclarr

- [Radarr JSON catalog — 56 Custom Formats](recyclarr/catalogs/radarr-custom-formats-json.tar.gz)
- [Sonarr JSON catalog — 55 Custom Formats](recyclarr/catalogs/sonarr-custom-formats-json.tar.gz)
- [Radarr instance YAML](recyclarr/config/radarr.yml)
- [Sonarr instance YAML](recyclarr/config/sonarr.yml)
- [Radarr 1080p RU Quality Profile](recyclarr/profiles/radarr-1080p-ru.yml)
- [Sonarr 1080p RU Quality Profile](recyclarr/profiles/sonarr-1080p-ru.yml)
- [Правила повторного использования шаблонов](recyclarr/profiles/README.md)
- [Settings providers](recyclarr/config/settings.yml)
- [Secrets example — только имена переменных и placeholders](recyclarr/config/secrets.yml.example)

В Git нет реальных API-ключей. Реальные значения хранятся только в локальном Recyclarr `secrets.yml`.

## Текущее состояние на 2026-11-06

- Radarr: подготовлен сервисный каталог из 56 форматов, отражающий настроенный профиль Radarr 1080p RU. В рамках переноса Sonarr отдельный Recyclarr Sync Radarr не выполнялся.
- Sonarr: Sync Recyclarr v8.8.1 успешно применён к профилю, который позднее переименован в Sonarr 1080p RU (в отчёте Sync сохранено прежнее имя 1080p RU). Создано 32, обновлено 4, оставлено без изменения 19, удалено 0.
- После Sonarr Sync все 55 управляемых форматов присутствуют, все их оценки соответствуют YAML. В базе осталось 62 Custom Formats, включая 7 прежних Sonarr-local форматов, которые не удалялись.
- Определения Custom Formats не привязаны к разрешению. Оценки назначаются отдельно каждому Quality Profile; наличие каталога в репозитории не включает его автоматически в любой профиль.

## Исторические материалы

- [Сводка текущих оценок](docs/current-custom-format-scores.md) — краткий указатель на полные таблицы групп.
- [Историческая страница HDR](docs/hdr-custom-formats.md) — ссылка на актуальный документ Format.
- [Дорожная карта](docs/roadmap.md) — задачи проекта; перед использованием статусов учитывать предупреждение в начале документа.
