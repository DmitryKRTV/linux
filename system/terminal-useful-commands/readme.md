## Linux terminal useful commands

Команды:
- `find destiantioName -name fileName` - команда поиска файлов, флаги означают способы поиска
- `wc` - world count. Команда показывает информацию о файле в виде: строчки слова символы(байт)
- `sort` - выводит на экран отсортированный по лексикографическому порядку файл. Не мутирует исходный файл. Флаг `-n` позволяет отсортировать по числу
- `cut -d symbolName -f 3 fileName` - разделяет поля по указанному символу используя флаг делиметр - `-d`
- `|` - pipe, позволяет последовательно запускать команды к результатам выполнения команд к предыдущей.
- `grep searching Destination/fileName` - команда поиска текста в файлах. `-i` позволяет игнорировать caseSensitive. Поисковый запрос может быть регулярным выражением с использованием флага `-E 'RegExp'` команда будет вида `grep -E '[A-Z]*' fileName` 