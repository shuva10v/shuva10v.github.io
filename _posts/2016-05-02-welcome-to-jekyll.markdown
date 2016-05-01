---
layout: post
title:  "Jekyll, github pages и grunt"
date:   2016-05-02 00:44:06 +0300
categories: jekyll github grunt npm ruby
---

Сделать блог всегда было легко - wordpress и тысячи подобных 
blog-платформ к вашим услугам.
Я решил попробовать [GitHub Pages](https://pages.github.com/). 
Ниже расскажу про опыт использования.

# Почему GitHub Pages
 
1. Это git. Никаких FTP и уж тем более настройки серверов. 
2. Поддержка markdown. [WYSIWYG][wysiwyg-wiki] - это хорошо, но настоящий IT-шник 
предпочитает консольку. Но писать html слишком больно.
3. Поддержка [jekyll](https://jekyllrb.com/). Jekyll - это простой
генератор сайтов-блогов с возможность кастомизации. О нем подробнее ниже.

# Настройка DNS

Настроить домен для работы с GitHub Pages оказалось достаточно просто.
Для этого достаточно закоммитить файл [CNAME][cname-link], в котором написать 
имя домена и вписать [магические ip-адреса][github-a-record]
в A запись:

```
shuvalov.io.		21599	IN	A	192.30.252.153
shuvalov.io.		21599	IN	A	192.30.252.154
```

# Jekyll и grunt/gulp/npm

Jekyll написан на ruby. Это круто, но для задач фронтенда мне очень нравится
в последнее время экосистема js фреймворков - grunt, gulp, bower, jade и т.д.
Я не смог выбрать удобный фреймворк, аналогичный Jekyll, поэтому решил 
попробовать [Интеграцию jekyll с Yeoman][generator-jekyllrb].
Yeoman это крутой инструмент для скаффолдинга, он позволяет сгенерировать шаблон
веб-приложения под широкий круг задач, например, с его помощью
можно быстро начать делать [расширения для google chrome][generator-chrome-extension].



К сожалению, [оригинальная
версия инструмента][generator-jekyllrb] оказалась нерабочей - на выходе я получил
нечто очень красивое и сложное, но собрать из него рабочий сайт не получилось.
Ошибки были довольно тривиальные и в репозитории уже висели pull requests
с решением проблемы - но автор явно не поддерживал более этот инструмент.
Ок, изучив форки быстро нашел [generator-jekyll-github][generator-jekyll-github].
В нем улучшена интеграция с GitHub Pages, поддержка Jekyll 3 и исправлены ошибки. 
Часть ошибок действительно исправлена, но далее начались проблемы с зависимостями
в Gemfile. Этот dependency hell я уже встречал не раз, работая с ruby приложениями,
и ожидал, что быстрого решения найти не удастся. Повозившись какое-то время,
бросил и собрал блог на Jekyll и написал этот текст.

[github-a-record]: https://help.github.com/articles/setting-up-an-apex-domain/#configuring-a-records-with-your-dns-provider
[generator-jekyllrb]: https://github.com/robwierzbowski/generator-jekyllrb
[generator-jekyll-github]: https://github.com/mdrmike/generator-jekyll-github
[cname-link]: https://github.com/shuva10v/shuva10v.github.io/blob/master/CNAME
[wysiwyg-wiki]: https://ru.wikipedia.org/wiki/WYSIWYG
[generator-chrome-extension]: https://github.com/yeoman/generator-chrome-extension
