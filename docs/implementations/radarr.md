# Реализация универсальной схемы в Radarr

Каталог Radarr содержит **56 Custom Formats**:

| Группа | Количество |
|---|---:|
| Voice | 41 |
| Src | 8 |
| Format | 5 |
| Extra | 2 |
| **Всего** | **56** |

Текущая привязка каталога предназначена для профиля **Radarr 1080p RU**. Сами JSON-определения не ограничены разрешением.

## Как Radarr различает источники

Radarr имеет отдельные Source и Quality Modifier, поэтому Blu-ray BDRip, Remux и BR-DISK можно классифицировать нативно.

| Логический тип | Условие Radarr | Формат | Баллы |
|---|---|---|---:|
| WEB-DL | Source = WEB-DL | Src-WEB-DL | +140 000 |
| Blu-ray BDRip | Source = Blu-ray; Modifier = None | Src-Bluray-BDRip | +120 000 |
| WEBRip | Source = WEBRip | Src-WEBRip | +100 000 |
| HDTV/SDTV | Source = TV; Modifier = None | Src-HDTV/SDTV | +80 000 |
| Blu-ray Remux | Source = Blu-ray; Modifier = Remux | Src-Bluray-Remux | +60 000 |
| Blu-ray Disk | Source = Blu-ray; Modifier = BR-DISK | Src-Bluray-Disk | 0 |
| Явный Disk/ISO по названию | Release Title regex | Src-Bluray-Disk-Title / Src-DVD-Disk | -1 000 000 |

BR-DISK и DVD-R не включены в текущий профиль качества; обычный DVD/DVDRip не блокируется правилом полного DVD Disk.

## Каталог и файлы

- [JSON catalog Radarr — 56 отдельных JSON](../../recyclarr/catalogs/radarr-custom-formats-json.tar.gz)
- [Recyclarr YAML Radarr](../../recyclarr/config/radarr.yml)
- [Общий settings.yml с providers](../../recyclarr/config/settings.yml)

JSON архив содержит каталог `custom-formats/`, в котором хранится отдельный файл на каждый Custom Format. Provider Radarr должен указывать именно на этот каталог.

## Оценки и область применения

YAML назначает баллы всем 56 форматам в профиле `Radarr 1080p RU`. API-ключ задаётся через `!secret radarr_1080p_api_key`; реальное значение в Git не хранится. У Recyclarr установлен `delete_old_custom_formats: false`, поэтому неуправляемые старые форматы автоматически не удаляются.

Extra-Theatrical использует Edition = Theatrical и существует только в Radarr. Extra-HEVC / H.265 общий и нейтральный.

Каталог отражает подготовленную конфигурацию Radarr 1080p. В рамках операции переноса в Sonarr 2026-11-06 отдельный Radarr Sync не выполнялся.
