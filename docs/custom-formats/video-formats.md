# Группа Format — HDR и Dolby Vision

Пять форматов группы Format одинаковы по смыслу и Release Title regex в Radarr и Sonarr. Они описывают видеорежим/цветность и не привязаны к 1080p или 2160p.

## Полная таблица

| Custom Format | Баллы | Release Title regex |
|---|---:|---|
| Format-HDR | +125 | `(?i)\bHDR\b|\bHDR\s*10\b|\bHDR\s*10(?=\+)|\bHDR\s*10\s*Plus\b` |
| Format-HDR10 | +1 000 | `(?i)\bHDR\s*10\b|\bHDR\s*10(?=\+)|\bHDR\s*10\s*Plus\b` |
| Format-HDR10+ | +2 000 | `(?i)\bHDR\s*10(?=\+)|\bHDR\s*10\s*Plus\b` |
| Format-DolbyVision | +500 | `(?i)\b(?:DV|DoVi|Dolby[ ._-]*Vision)\b|\b(?:DV|DoVi|Dolby[ ._-]*Vision)[ ._-]*(?:P(?:ROFILE)?[ ._-]*)?8[._ ]1\b` |
| Format-DV8.1 | +3 500 | `(?i)\b(?:DV|DoVi|Dolby[ ._-]*Vision)[ ._-]*(?:P(?:ROFILE)?[ ._-]*)?8[._ ]1\b` |

## Намеренное суммирование

| Маркер | Совпавшие форматы | Сумма |
|---|---|---:|
| HDR | HDR | +125 |
| HDR10 | HDR + HDR10 | +1 125 |
| HDR10+ | HDR + HDR10 + HDR10+ | +3 125 |
| Dolby Vision (общий) | DolbyVision | +500 |
| Dolby Vision Profile 8.1 | DolbyVision + DV8.1 | +4 000 |
| HDR10+ и DV Profile 8.1 | все три HDR + оба DV | +7 125 |

Форматы HDR перекрываются намеренно: более конкретная метка добавляет бонус, не отменяя общий признак. Dolby Vision не штрафуется: текстовое название не доказывает профиль DV и наличие HDR10 fallback.

Эти оценки являются аддитивными предпочтениями. HDR10+ не становится обязательным условием допуска 2160p; обычный 4K остаётся возможным, если Quality Profile не запрещает его отдельно.

## Ограничения распознавания

Проверяется Release Title, не видеопоток. Поддерживаются HDR10+ и HDR10 Plus; слитное написание HDR10Plus без разделителя сейчас не включено. Совпадение DV/DoVi/Dolby Vision не доказывает технический профиль и совместимость с конкретным телевизором или клиентом.
