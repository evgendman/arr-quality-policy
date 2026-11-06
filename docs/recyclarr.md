# Recyclarr: JSON-каталоги и применение

Здесь разделены три сущности:

1. **JSON Custom Formats** — определение одного формата: имя и условия распознавания.
2. **Recyclarr YAML** — список форматов и оценки, назначаемые конкретному Quality Profile.
3. **settings.yml** — локальные resource providers и пути к JSON-каталогам.

Реальные API-ключи находятся только в локальном `secrets.yml` на машине Recyclarr и не коммитятся.

## Текущие каталоги

- [Radarr JSON catalog — 56 файлов](catalogs/radarr-custom-formats-json.tar.gz)
- [Sonarr JSON catalog — 55 файлов](catalogs/sonarr-custom-formats-json.tar.gz)

Каждый архив содержит папку `custom-formats/` и отдельный JSON для каждого формата. Идентификаторы ресурсов имеют разные пространства имён `arrqp-radarr-*` и `arrqp-sonarr-*`; каталоги не следует смешивать в одном provider.

## Установка каталогов на хост

Если репозиторий клонирован в `/opt/arr-quality-policy`, распакуйте архивы:

```bash
mkdir -p /opt/arr-quality-policy/recyclarr/radarr /opt/arr-quality-policy/recyclarr/sonarr
tar -xzf radarr-custom-formats-json.tar.gz -C /opt/arr-quality-policy/recyclarr/radarr
tar -xzf sonarr-custom-formats-json.tar.gz -C /opt/arr-quality-policy/recyclarr/sonarr
```

В результате появятся:

- `/opt/arr-quality-policy/recyclarr/radarr/custom-formats/`
- `/opt/arr-quality-policy/recyclarr/sonarr/custom-formats/`

Фрагмент providers находится в [settings.yml](../recyclarr/config/settings.yml). Он предполагает эти пути. При другом расположении репозитория скорректируйте пути.

## Конфигурации экземпляров

- [Radarr YAML](../recyclarr/config/radarr.yml): `mini_radarr_1080p`, URL `http://127.0.0.1:7878`, профиль `Radarr 1080p RU`.
- [Sonarr YAML](../recyclarr/config/sonarr.yml): `mini_sonarr_1080p`, URL `http://127.0.0.1:8989`, профиль `1080p RU`.

Loopback URL корректен, если Recyclarr запускается на том же хосте, что и Arr. При удалённом запуске нужен адрес, доступный с узла Recyclarr.

В обоих YAML включено `delete_old_custom_formats: false`: неуправляемые форматы не удаляются автоматически. Примеры используют `!secret`, не реальные ключи.

## API-ключи

Используйте [secrets.yml.example](../recyclarr/config/secrets.yml.example) только как образец имён переменных. Создайте настоящий `secrets.yml` в каталоге конфигурации Recyclarr на соответствующем хосте, вставьте значения из Arr и установите права владельца, например `chmod 600 secrets.yml`.

Переменные:

- `radarr_1080p_api_key`
- `sonarr_1080p_api_key`

Не помещайте реальные API-ключи в Git, README, YAML-конфигурации, отчёты или shell history.

## Preview, Sync и проверка

Безопасная последовательность для каждого экземпляра отдельно:

1. Сделать штатную резервную копию Arr.
2. Проверить версию JSON-каталога и YAML.
3. Запустить Preview только нужного сервиса и экземпляра; проверить Create, Update, Unchanged, Delete и изменения профиля.
4. После проверки Preview выполнить Sync для этого сервиса.
5. Сверить API/базу: число форматов, условия, оценки, отсутствие нежелательных удалений и неизменность структуры Quality Profile.

Команды:

```bash
recyclarr sync sonarr --preview
recyclarr sync sonarr

recyclarr sync radarr --preview
recyclarr sync radarr
```

При нескольких экземплярах одного сервиса укажите точное имя через `--instance`. Не запускайте Sync без сервисного аргумента, если общий конфиг содержит и Radarr, и Sonarr.

У v8 каталоги конфигурации и данных можно задавать переменными окружения `RECYCLARR_CONFIG_DIR` и `RECYCLARR_DATA_DIR`. Не следует использовать устаревшее имя `RECYCLARR_APP_DATA_DIR`.

## Проверенные статусы на 2026-11-06

- Sonarr 1080p: Recyclarr v8.8.1 Sync завершён успешно; создано 32, обновлено 4, неизменено 19, удалено 0. Постпроверка подтвердила все 55 назначений оценок.
- Radarr 1080p: JSON-каталог построен по настроенным определениям Radarr. Отдельный Recyclarr Sync Radarr в рамках операции переноса Sonarr не выполнялся.
