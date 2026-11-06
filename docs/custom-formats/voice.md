# Группа Voice — русский дубляж и студии озвучки

Количество: **41 Custom Format**. Имена, Release Title regex и веса одинаковы в Radarr и Sonarr.

Группа разделяет общий признак полного дубляжа и именованные студии/сервисы/телевизионные дорожки. Если заголовок совпадает с несколькими выражениями, баллы суммируются.

## Полная таблица

| Custom Format | Баллы | Release Title regex |
|---|---:|---|
| Voice - Russian Dubbing | +100 000 | `\bдубляж\b` |
| Voice - Amedia | +2 000 | `\bAmedia\b` |
| Voice - Amediateka | +2 900 | `(?i)\bAmedia[\s._-]*teka\b` |
| Voice - AlexFilm | +1 500 | `\bAlexFilm\b` |
| Voice - BaibaKo | +2 500 | `\bBaibaKo\b` |
| Voice - ColdFilm | +100 | `(?i)\bCold[\s._-]*Film\b` |
| Voice - FOX / Fox Life | +400 | `(?i)\bFOX(?:[\s._-]*Life)?\b` |
| Voice - FocusStudio | +100 | `(?i)\bFocus[\s._-]*Studio\b` |
| Voice - Gears Media | +100 | `(?i)\bGears[\s._-]*Media\b` |
| Voice - GoldTeam | +100 | `(?i)\bGold[\s._-]*Team\b` |
| Voice - HamsterStudio | +100 | `(?i)\bHamster[\s._-]*Studio\b` |
| Voice - HDRezka | +8 000 | `\bHDRezka\b` |
| Voice - IdeaFilm | +100 | `(?i)\bIdea[\s._-]*Film\b` |
| Voice - iTunes | +9 290 | `(?i)\biTunes\b` |
| Voice - Jaskier | +2 800 | `(?i)\bJaskier\b` |
| Voice - Kravec | +3 000 | `(?i)\b(?:Kravec|Кравец)\b` |
| Voice - Кубик в Кубе | +7 000 | `\bКубик\s+в\s+Кубе\b` |
| Voice - Кураж-Бамбей | +100 | `(?i)\b(?:Кураж[\s._-]*Бамбей|Kurazh[\s._-]*Bambey)\b` |
| Voice - LE-Production | +2 900 | `(?i)\bLE[\s._-]*Production\b` |
| Voice - LineFilm | +100 | `(?i)\bLine[\s._-]*Film\b` |
| Voice - LostFilm | +5 000 | `\bLostFilm\b` |
| Voice - Мосфильм-Мастер | +9 500 | `(?i)\b(?:Мосфильм[\s._-]*Мастер|Mosfilm[\s._-]*Master)\b` |
| Voice - MovieDalen | +9 200 | `(?i)\bMovie[\s._-]*Dalen\b` |
| Voice - Невафильм | +9 300 | `(?i)\b(?:Невафильм|Neva[\s._-]*Film)\b` |
| Voice - NewStudio | +4 000 | `\bNewStudio\b` |
| Voice - NovaFilm | +1 000 | `\bNovaFilm\b` |
| Voice - NovaMedia | +600 | `(?i)\bNova[\s._-]*Media\b` |
| Voice - OMSKBIRD records | +500 | `(?i)\bOMSK[\s._-]*BIRD(?:[\s._-]*Records)?\b` |
| Voice - Пифагор | +9 400 | `(?i)\b(?:Пифагор|Pifagor)\b` |
| Voice - Red Head Sound | +9 000 | `(?i)\bRed[ ._-]*Head(?:[ ._-]*Sound)?\b` |
| Voice - SDI Media | +500 | `(?i)\bSDI[\s._-]*Media\b` |
| Voice - Sunshine Studio | +50 | `(?i)\bSunshine[\s._-]*Studio\b` |
| Voice - Тайкун | +100 | `(?i)\b(?:Тайкун|Taikun)\b` |
| Voice - TV - НТВ | +400 | `(?i)\b(?:НТВ|NTV)\b` |
| Voice - TV - ОРТ | +400 | `(?i)\b(?:ОРТ|ORT)\b` |
| Voice - TV - РенТВ | +400 | `(?i)\b(?:Рен[\s._-]*ТВ|Ren[\s._-]*TV)\b` |
| Voice - TV - РТР | +400 | `(?i)\b(?:РТР|RTR)\b` |
| Voice - TV - ТВ3 | +400 | `(?i)\b(?:ТВ[\s._-]*3|TV[\s._-]*3)\b` |
| Voice - TVShows | +6 000 | `\bTVShows\b` |
| Voice - WinMedia | +9 100 | `(?i)\bWin[\s._-]*Media\b` |
| Voice - заКадры | +500 | `(?i)\bза[\s._-]*кадры\b` |

## Логика шкалы

- Voice - Russian Dubbing (+100 000) описывает общий признак дубляжа.
- Индивидуальные студии и дорожки имеют +50…+9 500. Это относительное ранжирование поставщиков, а не утверждение об объективном качестве каждого релиза.
- Один отдельный студийный балл меньше шага источников в 20 000; несколько совпавших признаков суммируются.
- Полный дубляж и конкретная студия могут начислиться одновременно, если совпали оба regex.

## Ограничения

Распознавание происходит по Release Title. Оно не анализирует аудиопоток, число голосов или фактический тип перевода. Слово «дубляж» — текстовый маркер. Название студии — также только маркер в заголовке, а не гарантия наличия её дорожки.

При изменении политики следует синхронно обновить универсальную схему, JSON Radarr и Sonarr и их Recyclarr YAML.
