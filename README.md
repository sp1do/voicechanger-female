# VoiceChanger — женский голос (w-okada VCClient)

Готовая сборка [w-okada/voice-changer](https://github.com/w-okada/voice-changer) **2.0.78-beta (CUDA)** с женскими RVC-моделями и безопасным скриптом запуска. Работает локально, без интернета и подписок.

## Требования
- Windows 10/11 x64
- Видеокарта **NVIDIA** (RTX 20xx и новее, от 6 ГБ видеопамяти). На AMD и встроенной графике эта сборка не заработает.
- Около 20 ГБ свободного места
- [7-Zip](https://www.7-zip.org/) для распаковки

## Установка
1. Скачай **все** части `VoiceChanger-female.7z.001`, `.002` и т. д. со страницы [Releases](../../releases) в одну папку.
2. Открой `.001` в 7-Zip и распакуй. Путь должен быть **без кириллицы и пробелов**, например `C:\VoiceChanger`.
3. Установи [VB-Audio Virtual Cable](https://vb-audio.com/Cable/): распакуй архив, запусти `VBCABLE_Setup_x64.exe` **от имени администратора**, нажми *Install Driver* и **перезагрузи ПК**.
4. Запусти `dist\main\start_safe.bat`. Если появится SmartScreen: «Подробнее» → «Выполнить в любом случае».

## Настройка
В окне программы:

| Параметр | Значение |
|---|---|
| ГПУ | твоя NVIDIA |
| Голос (слот) | начни с **RU Female** |
| Тон | +12 (если голос «бурундучий», ставь +8…+10) |
| Фрагмент | 8192–12000 |
| Дополнительно | 16384 или больше |
| Усиление выход | 1 |
| Шумовой гейт | −50…−60 |
| Шумоподавление | подавление1 + подавление2 |
| вход | твой микрофон |
| выход | `CABLE Input (VB-Audio Virtual Cable)` |
| монитор | наушники (чтобы слышать себя) |

Нажми **Старт**.

**Telegram / Discord / игры:** выбери микрофоном `CABLE Output (VB-Audio Virtual Cable)`.

## Голоса в сборке
| Слот | Имя | Источник |
|---|---|---|
| 5–7 | Female p249 / p262 / p340 | [Nekochu/RVC-VCTK_Voice-sample](https://huggingface.co/Nekochu/RVC-VCTK_Voice-sample), Apache-2.0 |
| 8 | RU Female | [Razer112/Public_Models](https://huggingface.co/Razer112/Public_Models) (OriginalRU), OpenRAIL |
| 9 | Female EN | [Razer112/Public_Models](https://huggingface.co/Razer112/Public_Models) (Female), OpenRAIL |
| 10 | E-Woman EN | [Razer112/Public_Models](https://huggingface.co/Razer112/Public_Models) (E-Woman), OpenRAIL |

Встроенные японские голоса и Beatrice-модели автора программы убраны. При первом запуске программа может сама докачать демо-голоса.

## Безопасность
- Сборка скачана с официального [Hugging Face wok000/vcclient000](https://huggingface.co/wok000/vcclient000), SHA256 архива сверен: `1ca9151005ab64658cfc4bf40f845008d2543abe7ff67db2da9d6889f07f7ae0`.
- Все `.pth`-модели проверены [picklescan](https://github.com/mmaitre314/picklescan), угроз нет.
- `start_safe.bat` запускает сервер только на `127.0.0.1` (штатные `start_http*.bat` открывают его для всей локальной сети). У программы есть [известная уязвимость](https://github.com/w-okada/voice-changer/issues/1114), поэтому **закрывай её, когда не пользуешься**.
- Добавляешь свои модели? Проверяй `.pth` через picklescan: такой файл может содержать исполняемый код.

## Известные баги сборки 2.0.78-beta
- Если окно не открывается и сервер сразу закрывается, в системе задана переменная `ELECTRON_RUN_AS_NODE`. `start_safe.bat` её сбрасывает.
- Конвертация файлов через API падает (ошибка `Timer ... enable`), в реальном времени всё работает.

## Лицензии
Программа распространяется под лицензией MIT (© Wataru Okada и соавторы), см. [LICENSE](LICENSE). Лицензии моделей указаны в таблице выше. VB-Cable в сборку не входит: это donationware от VB-Audio, скачивай его с официального сайта.
