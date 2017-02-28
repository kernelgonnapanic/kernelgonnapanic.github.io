---
title: frontend-microservices-2
thumbnailImagePosition: top
coverMeta: out
coverSize: partial
tags:
---


- ładowanie różnych skryptów w ramach jednej aplikacji
  (wspólny index, aplikacji bootstrapują się na różnych divach)
  + niezależność releasów
  + niezależność używanej technologii
  + nad każdą aplikacją może pracować inny zespół

  - konieczność posiadania aplikacji "hosta", określającego jak poszczególne divy z aplikacji mają wyglądać i się zachowywać
  - konieczność posiadania mechanizmu publikowania skryptów np. na cdn i uaktualniania indexu dla każdego z komponentów
  - brak zdefiniowanego sposobu komunikacji między nimi

- ładowanie różnych aplikacji w iframe'ach
  + prawdziwa separacja (????)

  - problem z komunikacją między komponentami

- layout service (np. Tailor)

http://www.slideshare.net/lmineiro/the-frontend-taboo-a-story-of-full-stack-microservices
https://speakerdeck.com/d_kubyshkin/frontend-microservices
