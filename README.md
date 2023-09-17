## Поиск по CSS селекторам в BeautifulSoup4 (справочное руководство)
источник: //docs-python.ru/packages/paket-beautifulsoup4-python/css-selektory/

В модуле BeautifulSoup4 есть метод BeautifulSoup.select(), который использует SoupSieve, чтобы запустить CSS селектор и вернуть все подходящие элементы. 
В объекте Tag есть похожий метод, который запускает CSS селектор в отношении содержимого одного тега.

Интеграция SoupSieve была добавлена в BeautifulSoup4.7.0. 
В более ранних версиях также есть метод .select(), но он поддерживат только самые часто используемые селекторы CSS. 
Если BeautifulSoup4 устанавливался через pip, то одновременно должен был установиться SoupSieve.

## Поиск по атрибутам HTML-тега.

### [attribute]: 
Ищет HTML-элементы с атрибутом attribute.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[href]')
# [<a href="#internal">Internal link</a>, 
# <a href="http://example.com">Example link</a>, 
# <a href="#InSensitive">Insensitive internal link</a>, 
# <a href="http://example.org">Example org link</a>]
```

### [attribute="value"]: 
Ищет HTML-элементы с атрибутом attribute, который имеет значение value.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[href="#internal"]')
# [<a href="#internal">Internal link</a>]
```

### [attribute~="value"]:
Ищет HTML-элементы с атрибутом attribute, где значение value встречается в строке, представляющей список разделенный пробелом.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<ul>
  <li><a href="#internal" class="class1 class2 class3">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[class~=class2]')
# [<a class="class1 class2 class3" href="#internal">Internal link</a>]
```

### [attribute|="value"]:
Ищет HTML-элементы с атрибутом attribute, значение которого представляет собой список разделенный черточками, и который начинается со значения value.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<div lang="en">Some text</div>
<div lang="en-US">Some more text</div>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('div[lang|="en"]')
# [<div lang="en">Some text</div>,
# <div lang="en-US">Some more text</div>]
```

### [attribute^="value"]:
Ищет HTML-элементы с атрибутом attribute, значение которого начинается с value.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[href^=http]')
# [<a href="http://example.com">Example link</a>,
# <a href="http://example.org">Example org link</a>]
```

### [attribute$="value"]:
Ищет HTML-элементы с атрибутом attribute, значение которого заканчивается на value.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<body>
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[href$=org]')
# [<a href="http://example.org">Example org link</a>]
```

### [attribute*="value"]:
Ищет HTML-элементы с атрибутом attribute, значение которого содержит подстроку value.
```
>>> from bs4 import BeautifulSoup as bs
>>> html = """
<html>
<head></head>
<body>
<ul>
  <li><a href="#internal">Internal link</a></li>
  <li><a href="http://example.com">Example link</a></li>
  <li><a href="#InSensitive">Insensitive internal link</a></li>
  <li><a href="http://example.org">Example org link</a></li>
</ul>
</body>
</html>
"""
>>> soup = bs(html, 'html.parser')
>>> soup.select('[href*="example"]')
# [<a href="http://example.com">Example link</a>,
# <a href="http://example.org">Example org link</a>]
```
