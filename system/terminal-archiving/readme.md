## Linux terminal archiving

Команды:
- `tar` - tape archive.
- `tar cvf archiveName archivingFileName` - cvf - create verbose file(f - всегда должна быть последней). Создать архив
- `tar tf` - tf - test file - проверить что находится внутри
- `tar xvf archiveName` - xvf - extract verbose file - разархивировать архив выводя процесс в консоль(flag v - verbose)
- `gzip archiveName` - компрессировать архив в формат gz
- `gupzip archiveName` - раскомпрессировать архив формата gz
- `bzip2` - компрессировать архив в формат bz2
- `bunzip2` - раскомпрессировать архив формата bz2
- `xz` - компрессировать архив в формат xz
- `unxz` - раскомпрессировать архив формата xz
- `tar cvzf GZIPFileName.gz target` - архивировать и компрессировать файл в архив формата gz. Флаг z (из cvzf) отвечает за тип архива (gzip)
- `tar cvjf BZIP2FileName.bz2 target` - архивировать и компрессировать файл в архив формата bz2. Флаг j (из cvjf) отвечает за тип архива (bzip2)
- `tar cvJf XZFileName.xz target` - архивировать и компрессировать файл в архив формата xz. Флаг J (из cvJf) отвечает за тип архива (xz)
- `tar xf archiveName` - разархивировать любой формат архивов (xz, bz2, gz)
- `zip -r ZIPName.zip target` - архивировать и компрессировать файл в архив формата zip. Может потребовать установить zip на ОС
- `unzip ZIPName.zip ` - разархивировать архив формата zip