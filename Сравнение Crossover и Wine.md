## Сравнение Crossover и Wine

Я создал бутылку с игрой `S.T.A.L.K.E.R. Call of Pripyat [GOG.com]` в Crossover v22.1.1 и в Wine. В Wine с помощью Wineskin Winery на основе Wineskin-2.9.1.9 и движка WS11WineCX64Bit22.1.1-rc2 в macOS Monterey Intel и потом сравнил папку-бутылку сгенерированную Crossover и папку `MyCoolWrapper.app/Contents/SharedSupport/prefix` внутри бутылки, сгенерированной Wine.

Сравнивал в Beyond Compare и в папках `Program Files`, `Program Files (x86)`, `windows` было очень много не идентичных, по содержимому, файлов. Файлы в бутылке Crossover весили больше таких же файлов в бутылке Wine. Также в бутылке Crossover было много эксклюзивных файлов (которых нет в бутылке Wine).

---

Я переместил папки `Program Files`, `Program Files (x86)`, `windows` из бутылки Crossover в бутылку Wine (предварительно убрав эти папки из бутылки Wine) и запустил игру стандартным запуском бутылки Wine и игра без проблем запустилась и я увидел меню игры.

Я переместил папки `Program Files`, `Program Files (x86)`, `windows` из бутылки Wine в бутылкуCrossover (предварительно убрав эти папки из бутылки Crossover), запустил Crossover и из него запустил игру и она не запустилась. 4 попытки повторного запуска игры никак не изменили ситуацию.

Так что, скорее всего, именно конвертировать бутылку Wine в бутылку Crossover не получится, но можно создать новую бутылку Crossover разместив в ней программу, установленную в бутылке Wine.

---

В `CrossOver.app/Contents/SharedSupport/CrossOver/CrossOver-Hosted Application` есть CLI утилиты по созданию Crossover бутылок и работы с ними.