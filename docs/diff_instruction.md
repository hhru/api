# Получить diff “как на GitHub” для двух больших файлов документации

## Шаг 1 — Сгенерировать diff через git diff
Убедитесь, что git установлен:

```
git --version
```
Сгенерируйте diff для двух файлов и сохрани в файл:
```
git diff --no-index --minimal --histogram -- file1 file2 > changes.diff
```
где file1 и file2 — пути к сравниваемым файлам, файлы документации можно взять в папке [history](../versions/2026/history)


## Шаг 2 — Установить diff2html и отрисовать diff в HTML
Проверьте, что есть Node.js и npm:
```
node -v
npm -v
```

Сгенерируйте HTML (side-by-side как на GitHub):
```
npx diff2html-cli -i file -o preview -s side -- changes.diff
```

# Результат
После выполнения команды выше файл открывается автоматически, если этого не произошло, то надо открыть файл diff.html самостоятельно.

Также можно воспользоваться онлайн ресурсами, например https://www.oasdiff.com/diff или похожими. 