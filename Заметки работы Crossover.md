## Заметки по работе Crossover

\* Пути, указанные в этом файде и начинающиеся с `./` - это пути от корня бутылки

---

### При создании любой бутылки
При создании любой бутылки создается папка с названием бутылки по пути `/Users/$USER/Library/Application Support/CrossOver/Bottles/`

---

### Бутылка это папка с файлом `./cxbottle.conf`
Crossover понимает, что папка является бутылкой для Crossover по наличию в папке файла `./cxbottle.conf`

И если на момент запуска Crossover в папке-бутылке не будет этого файла, то в списке бутылок в Crossover не будет этой бутылки и всего, что с ней связано

---

### Приложения быстрого запуска в интерфейсе бутылки
Наверное, после окончания установки программы Crossover анализирует папки по путям
```
/drive_c/ProgramData/Microsoft/Windows/Start Menu/Programs
/drive_c/users/Public/Desktop
```

И если в них появляются новые объекты, например, папки с ярлыками `.lnk` или файлами `.url`, то создается папка `./desktopdata` а в ней папка `cxmenu` а в ней папки и файл
```
Desktop.C^5E3A_users_Public_Desktop/
StartMenu.C^5E3A_ProgramData_Microsoft_Windows_Start^2BMenu/
Shortcuts/
cxmenu_macosx.plist
```

В папках
```
Desktop.C^5E3A_users_Public_Desktop/
StartMenu.C^5E3A_ProgramData_Microsoft_Windows_Start^2BMenu/
```

находятся, те же файлы, что и в
```
/drive_c/ProgramData/Microsoft/Windows/Start Menu/Programs
/drive_c/users/Public/Desktop
```

и хоть они имеют такие же расширения, внутри каждого из них содержится Shell-скрипт примерно такой:
```shell
#!/bin/sh
exec "/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/wine" --bottle "StalkerCOPBottle2" --check --wait-children --start "C:/users/Public/Desktop/S.T.A.L.K.E.R. Call of Pripyat.lnk" "$@"
```


### Приложения на основе ярлыков `.lnk` и `.url` файлов
Если в бутылке есть папка `/desktopdata` и в ней файл `cxmenu_macosx.plist` то при запуске Crossover на основе содержимого файла `cxmenu_macosx.plist` генерирует данные в папке `/Users/$USER/Applications/CrossOver` и там создает папку с таким же названием, как в файле `cxmenu_macosx.plist` называется пункт `Root > CrossOver-76208766-77AA-4001-B004-E52017BA8A45/ > Children > StartMenu/ > Children > Windows Applications/ > Children > НАЗВАНИЕ`. Все приложения из этой папки также отображаются в Launchpad.

Например папку с названием `S.T.A.L.K.E.R. Call of Pripyat [GOG.com]`

В этой папке находятся приложения с такими же названиями, как файлы в папках
```
/desktopdata/cxmenu/Desktop.C^5E3A_users_Public_Desktop/
/desktopdata/cxmenu/StartMenu.C^5E3A_ProgramData_Microsoft_Windows_Start^2BMenu/
```
Папка с этим названием генерируется при каждом запуске Crossover сразу после нажатия на кнопку "Попробовать", если это триал версия Crossover. При этом если в `cxmenu_macosx.plist` это название изменить и перезапустить Crossover, папка со старым названием будет удалена и появится папка с новым названием из `cxmenu_macosx.plist` и точно также после каждого изменения этого названия в `cxmenu_macosx.plist`

---

### Иконки генерируемых приложений
Также после установки программы в бутылку, создается папка `./windata` и в ней создаются `.png` файлы разных размеров. Эти файлы, служат материалом для генерации иконок для приложений в `/Users/$USER/Applications/CrossOver`

Если удалить или переименовать папку `./windata` и изменить название папки для приложений в файле `cxmenu_macosx.plist` и перезапустить Crossover, чтобы он пересоздал папку с приложениями, то у всех приложений будут стандартные иконки, которые будут взяты по пути `CrossOver.app/Contents/Resources/exeIcon.icns`

---

### Неважные вещи
Файл `./cxmenu.conf` судя по его содержимому как-то связан с генерируемыми Crossover'ом приложениями, которые потом отображаются в папке `/Users/$USER/Applications/CrossOver` и в меню бутылки при запуске Crossover.

Удаление файла `./cxmenu.conf` и перезапуск Crossover, похоже, ни на что не повлиял.

В файле `cxmenu_macosx.plist` следующий от корня ключ называется `Crossover-` + `BottleID` + `/`. Значение `BottleID` находится в `./cxbottle.conf`.

Изменение этого ключа в `cxmenu_macosx.plist`, например сокращение до текста `Crossov` и перезапуск Crossover, похоже, ни на что не влияют.
