# Сводка текущих оценок Custom Formats

Последнее обновление: 2026-11-06.

Эта страница служит кратким указателем. Полные таблицы имён, баллов и регулярных выражений находятся в документах групп.

| Группа | Текущие веса | Полная спецификация |
|---|---:|---|
| Src: источники | WEB-DL +140 000; BDRip +120 000; WEBRip +100 000; HDTV/SDTV +80 000; Blu-ray Remux +60 000 | [Src — источники и дисковые маркеры](custom-formats/sources.md) |
| Voice: русский дубляж | +100 000 | [Voice — 41 формат, полная таблица и regex](custom-formats/voice.md) |
| Voice: отдельные студии/дорожки | +50…+9 500 | [Voice — 41 формат, полная таблица и regex](custom-formats/voice.md) |
| Format: HDR / HDR10 / HDR10+ | +125 / +1 000 / +2 000, накопительно | [Format — HDR и Dolby Vision](custom-formats/video-formats.md) |
| Format: Dolby Vision / DV8.1 | +500 / +3 500, Profile 8.1 итого +4 000 | [Format — HDR и Dolby Vision](custom-formats/video-formats.md) |
| Extra: HEVC/H.265 | 0 | [Extra — дополнительные признаки](custom-formats/extras.md) |
| Extra: Theatrical | +50, только Radarr | [Extra — дополнительные признаки](custom-formats/extras.md) |
| DVD/Blu-ray Disk title markers | -1 000 000 | [Src — источники и дисковые маркеры](custom-formats/sources.md) |

Баллы назначаются отдельно в каждом Quality Profile. Они не задают целевое разрешение или порядок групп качества. См. [универсальную модель](policy-model.md).

Актуальные привязки: [Radarr YAML](../recyclarr/config/radarr.yml), [Sonarr YAML](../recyclarr/config/sonarr.yml). JSON-каталоги и порядок применения описаны в [руководстве Recyclarr](recyclarr.md).
