<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Git</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><ul>
<li><a href="#%D0%BA%D0%BB%D0%BE%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F-%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE">Клонирование репозитория локально</a></li>
<li><a href="#%D0%B2%D0%B5%D1%82%D0%BA%D0%B8">Ветки</a></li>
<li><a href="#%D1%81%D0%B1%D1%80%D0%BE%D1%81%D0%B8%D1%82%D1%8C-%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F">Сбросить локальные изменения</a></li>
<li><a href="#commit-%D0%B8-push">Commit и push</a></li>
</ul>
<h3 id="клонирование-репозитория-локально">Клонирование репозитория локально</h3>
<p><code>git clone url [directory]</code></p>
<h3 id="ветки">Ветки</h3>
<p>Создание новой ветки и переход к ней<br>
<code>git checkout -b branchName</code><br>
Создание новой ветки на основе другой<br>
<code>git checkout -b branchName parentBranch</code><br>
Переход к ветке<br>
<code>git checkout branchName</code><br>
Стянуть изменения с чужой ветки на ту на которой находишься<br>
<code>git merge parentBranch</code></p>
<h3 id="сбросить-локальные-изменения">Сбросить локальные изменения</h3>
<p>Сбросить все локальные изменения<br>
<code>git reset --hard HEAD</code><br>
Сброс изменений конкретного файла<br>
<code>git checkout src/app/app.module.ts</code></p>
<h3 id="commit-и-push">Commit и push</h3>
<p>Добавить необходимые файлы на отправку<br>
<code>git add .</code><br>
Создать новый коммит с текстом локально<br>
<code>git commit -m "some text"</code><br>
Отправить изменения на облачный репозиторий<br>
<code>git push</code></p>
</div>
</body>

</html>
