### GitBranches

Создать новую ветку можно с помощью команды git branch <название ветки>. Важно, чтобы название было понятным для вас и других участников проекта. 
Создадим новую ветку для проекта: git branch input.
Переключимся на новую ветку с помощью команды git checkout input. (Чтобы создать ветку и переключиться на нее за одно действие, можно воспользоваться флагом -b: git checkout -b <название ветки>.)
Закоммитим изменения: git commit -a -m “Add input”.
Проверим git status, убедимся, что рабочее дерево чистое. Проверим историю: git log. Видим весь путь работы: последнее изменение и все изменения, которые были еще до ответвления. Чтобы выйти из истории, нужно нажать q в английской раскладке.
Вернемся в основную ветку с помощью команды git checkout main и зайдем в редактор. Изменения пропали, потому что в основную ветку мы их еще не добавляли. Проверяем историю: git log. В ветке main видим только старые коммиты, до ответвления. 
Как сливать ветки и решать конфликты
Когда мы сделали все нужные изменения в коде, проверили, что они работают так, как мы хотим, можно переносить изменения в основной код. 
Сначала нужно переключиться на основную ветку: git checkout main.
Теперь можем забрать изменения из ветки input: git merge --no-ff <название ветки, изменения из которой забираем> -m “Сообщение о слиянии веток”.
Такая команда создаст новый коммит, в котором объединятся две ветки.
Флаг --no-ff отменяет механизм fast-forward, который стоит в git по умолчанию. Если его не отменить, git не будет создавать новый коммит, в котором объединятся две ветки, а просто сделает дополнительную ветку веткой main. Иногда такой механизм полезен, но сейчас он нас запутает, поэтому отключаем его. Вы можете поэкспериментировать и посмотреть, в какой ситуации какой механизм вам больше подходит. 
В нашем случае git понял, как нужно совместить две ветки. Проверим редактор, чтобы убедиться, что результат тот, который нам нужен.
Иногда Git не понимает, как именно нужно объединить ветки и выводит сообщение о конфликте. В таких ситуациях, мы должны показать ему это. Для этого переходим в редактор, удаляем лишние символы и приводим код к тому виду, который нам нужен.  Сохраняем файл в редакторе, проверяем git status — увидим сообщение о конфликте. Чтобы показать Git, что мы разрешили конфликт, просто закоммитим изменения: git commit -a -m «Add input in main».
Проверим историю: git log. Если видим сообщение о коммите, в котором сливаются две ветки, значит, все получилось.
Историю изменений, создания новых веток и слияния можно визуализировать: git log --oneline --graph.
Отправляем изменения на удаленный репозиторий: git push.
Проверяем GitHub. Изменения появились, но залилась только ветка main. Другие ветки нужно заливать отдельно: git push -u origin <название ветки>.
Зальем ветку input: git push -u origin input. Видим, что на GitHub появились две ветки. Переключиться между ветками можно в меню branch.
Как перемещаться по коммитам  
Еще один важный указатель в git — это head. Он указывает, на какой ветке мы находимся. Если мы перейдем в историю, увидим, что head указывает на ветку main и на удаленную ветку origin_main. Это значит, наш локальный и удаленный репозитории синхронизированы. 
Перейдем на другую ветку командой git checkout input, и в истории head будет указывать уже на input.
Как удалить ветку в Git
Если мы понимаем, что ветка больше не нужна, можно ее удалить.  При этом удаляемая ветка не должна быть той веткой, в которой мы находимся. Удалим ветку calc: git branch -d calc. Git предупреждает, что ветка еще не объединена с основной веткой и что удалять ее опасно. Но мы уверены, что хотим удалить ветку, поэтому вводим еще одну команду, которую нам подсказывает git: git branch -D calc.
Теперь удалим ветку input. Она уже залита на GitHub, поэтому сначала удалим ее с удаленного репозитория: git push --delete origin input
Проверим Git Hub: ветка удалилась. Теперь удаляем ветку локально: git branch -d input.
