## Linux terminal input-output

Команды:
- `text > fileName` - перезаписывает файл и сохраняет в нём text
- `text >> fileName` - дописывает в файл текст
- `2>` - перенаправления потока чтения файла с ошибками
- `2> /dev/null>` - не сохранит ошибочные результаты
- `grep term file &> file2` - `&>` сохранит и ошибочные и истинные результаты
- `>`, `>>` - Перенаправление хороших результатов с перезаписыванием (>) или дозаписыванием(>>)
- `2>`, `2>>` - Перенаправление плохих результатов с перезаписыванием (2>) или дозаписыванием(2>>)
- `&>` - Сохранить и плохие и хорошие
- `/dev/null` - не сохранять результаты (сохранить на не существующее устройство)