---
title: Hexo - nowy rok, nowy blog!
thumbnailImagePosition: top
coverMeta: out
coverSize: partial
date: 2017-01-26 19:46:42
thumbnailImage: hexo_thumb.png
coverImage: hexo.png
tags:
  - Programowanie
  - Blogowanie
  - Hexo
  - Github
---

Dawno się nie słyszeliśmy, prawda? W międzyczasie przez bloga przeszła burza, a jej rezultatem jest to, co właśnie widzicie. I nie jest to tylko nowy szablon. Przez ostatnie kilka miesięcy budowałam tego bloga od zera na nowej platformie. Dlatego też, **na dobry nowy początek**, nie może zabraknąć wpisu na temat narzędzi, które na to pozwalają.

<!-- more -->

Utrzymywanie bloga na bloggerze przysprawiało mi problemów od samego początku. Edytowanie postów, przeróbki w html'u czy też edytowanie szablonu było strasznie męczące. Z tego powodu właśnie wyruszyłam w poszukiwaniu czegoś, co będzie bliższe mojemu sercu technologicznie (JavaScript &#10084;	), a z drugiej strony proste w obsłudze. Myślałam o narzędziu, które jest przyjazne developerom, a niekoniecznie nietechnicznym użytkownikom.

# Hexo
W tychże poszukiwaniach natrafiłam na platformę Hexo. Jest to narzędzie do blogowania, które jest po prostu node'owym skryptem. Instalujemy je za pomocą npm'a i w kilka sekund mamy bloga:
```bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
Proste, prawda?

Jeśli chodzi o posty, to do ich tworzenia używamy Markdowna (kolejny miód na moje serce). Pracuje mi się z nim dużo wygodniej niż z bloggerowym wydaniem XHTMLa (sic!).
Hexo oferuje również duuuuużo różnorodnych pluginów. Nie miałam jeszcze okazji się nimi bawić, ale już widzę kilka, które może się przydadzą. Dodatkowo, dla mnie zdecydowanym plusem jest to, że cały czas poruszam się w obrębie narzędzi, które są mi znane. Jak pewnego dnia okaże się, że nikt jeszcze nie stworzył potrzebnego mi pluginu, zawsze mogę go napisać sama.

Publikowanie posta z Hexo sprowadza się do użycia kilku komend, no i oczywiście dostarczenia treści ;)

# Tranquilpeak
Jednak, przyznajmy szczerze, fajna platforma to nie wszystko. Zależało mi na przyjemnym, estetycznym szablonie, który będzie stworzony przy użyciu narzędzi, które znam i lubię. W ten sposób zdecydowałam się na tranquilpeak. Jest to (przynajmniej dla mnie) naprawdę zgrabny i minimalistyczny szablon. Można go dowolnie dostosowywać, ma bardzo bogaty interfejs ustawień i obfitą dokumentację.

Ja zdecydowałam się dodatkowo wprowadzić do niego kilka poprawek, by odpowiadał moim potrzebom i lepiej wyglądał na ekranach o dużej rozdzielczości. Z racji, że jest to normalny frontendowy projekt zmiany te poszły szybko i byłam bardzo zadowolona z wyboru, który dokonałam.

Żródła możecie oczywiście znaleźć na [githubie](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak).

# Github pages
Ok, wszystko pięknie, ale na pewno pojawia się Wam w głowach pytanie: gdzie hostuję swojego bloga? No i okazuje się, że tu też zwróciłam się w stronę rozwiązań, które już znałam. Jako, że są to same statyczne strony, hostuję je na [Github Pages](https://pages.github.com/).

Czyni to dodatkowo łatwym jeden z pluginów do hexo. Hexo dysponuje różnymi rodzajami deployerów. Z racji, że hostuje bloga na Githubie używam [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git), ale możesz również deployować na heroku, ftp, czy używając własnej shellowej komendy, specyficznej dla wybranego przez Ciebie rodzaju hostingu.

Jestem bardzo ciekawa jak w dalszej perspektywie będzie się sprawował stack, który wybrałam. Na razie jestem całkiem z niego zadowolona.

A Wy? Jak Wam podoba się nowa odsłona bloga? Napiszcie koniecznie w komentarzach.

Ania
