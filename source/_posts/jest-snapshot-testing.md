---
title: "Snapshot testing - co to takiego? [Frontend testing #2]"
tags:
  - JavaScript
  - Frontend
  - Frontend testing
categories:
  - Techniczne
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: camera.jpg
coverImage: camera.jpg
date: 2018-02-15 21:56:00
---

Po całkiem długim okresie przerwy (pierwszy wpis z cyklu powstał w lipcu ubiegłego roku), zapraszam znów do przyjrzenia się bliżej frontendowym testom. Dziś porozmawiamy o Jest oraz snapshot testingu - jednej z jego funkcjonalności.

<!-- excerpt -->

Po całkiem długim okresie przerwy (pierwszy wpis z cyklu powstał w lipcu ubiegłego roku), zapraszam znów do przyjrzenia się bliżej frontendowym testom. Obiecałam wtedy kilka fajnych wpisów dotyczących narzędzi, jakie mamy do dyspozycji pisząc testy w JSie. Mam nadzieję, że nie zapomnieliście o temacie!

A w dzisiejszym odcinku zobaczymy czym jest **Jest**. Dokładniej przyjrzymy się jednej z jego funkcjonalności, jaką jest snapshot testing. Czytajcie do końca, żeby dowiedzieć się, co tam jeszcze knuję w temacie wpisów o testowaniu. Enjoy!

## Jest - co to jest ?

Zacznijmy od tego co to jest ten Jest i co może nam zaoferować. Żeby móc wygodnie pisać frontowe testy jednostkowe potrzebujemy narzędzi, które pomagają w uruchomieniu tych testów oraz usprawniają walidowanie wyników poszczególnych operacji. Gdy chcemy do tego podejść bardziej szczegółowo, jest to kilka poziomów, o które musimy się zatroszczyć. Jest środowisko uruchomieniowe (test runner), mamy również test framework, który definuje jak od strony kodu będą wyglądać nasze testy oraz potrzebujemy narzędzia, które ułatwia pisanie asercji, czyli walidowanie efektów np. wywołania funkcji (assertion library).

Do tej pory elementy te często istniały jako osobne biblioteki, obecnie często są nam podane w jednym pakiecie. I tak też jest w przypadku Jesta.
Jeśli ktoś chciałby się dowiedzieć trochę więcej o tym, z jakich elementów składa się środowisko testowe i czym się od siebie różnią, [tutaj](http://amzotti.github.io/testing/2015/03/16/what-is-the-difference-between-a-test-runner-testing-framework-assertion-library-and-a-testing-plugin/) znajdziecie fajny artykuł na ten temat.

Ustaliliśmy już, że Jest oferuje nam wszystko co jest potrzebne do wystartowania z pisaniem testów. Co więcej twórcy chwalą się, że jest to narzędzie typu zero-configuration. Z moich doświadczeń wynika jednak, że nie zawsze obędziemy się bez dodatkowej konfiguracji i jeśli twój projekt korzysta z preprocesorów czy np. jakichś specyficznych loaderów do webpacka to zazwyczaj trzeba coś więcej poustawiać.

## Co fajnego Jest nam oferuje?

1. Dla mnie najistotniejszy jest fakt, że Jest jest ewidentnie rezultatem ewolucji narzędzi do testowania. Mamy tu do dyspozycji wbudowany mechanizm do mockowania na poziomie rozwiązywania zależności (importów), ale też możemy ręcznie podmienić implementację danej funkcji na czas testów. Zgrabnie też jesteśmy w stanie testować kod asynchroniczny, używając np. konstrukcji async/await. Dodatkowo mamy również wbudowane mierzenie pokrycia kodu, co czasem przydaje się w celach informacyjnych, jednak z wielu powodów nie powinno być traktowane jako wyznacznik jakości otestowania kodu.

   _Przykład tworzenia mocków._

```js
const mock = jest.fn();

const betterMock = jest.fn(() => ({
  answerToLife: 42
});
```

_Przykład testowania wyniku asynchronicznej operacji_

```js
test("the data is peanut butter", async () => {
  expect.assertions(1);
  const data = await fetchData();
  expect(data).toBe("peanut butter");
});
```

2. Zespoły, które wcześniej korzystały z innego setupu dla testów jednostkowych względnie łatwo mogą się przesiąść na Jest'a, ponieważ wspiera on składnie Jasmine'a. Dla tych, którzy korzystali z mniej popularnych opcji, istnieją rozwiązania takie jak `jest-codemods`, które jednorazowo zmieniają składnię testów i wykonują większość brudnej roboty za nas.
3. Jest'a z podstawowymi ustawieniami, gotowego do działania otrzymujemy "za darmo", gdy tworzymy nową aplikację używając `create-react-app` lub `react-native init`.
4. No i oczywiście oferuje mechanizm do testowania za pomocą snapshotów, którym za raz się zajmiejmy w szczegółach.

## Co to jest snapshot testing?

Testowanie przy użyciu snapshotów jest jednym z rodzajów testów, które możemy tworzyć dla kodu frontendowego. Przydaje się w szczególności do testowania komponentów (np. w React czy Vue), ale możemy bazując na tym podejściu pisać też testy logiki biznesowej.

Głównym jego założeniem jest porównywanie wyniku uruchomienia funkcji z jakimś oczekiwanym efektem, który w postaci pliku przechowujemy w repozytorium. W rezultacie uruchomienia testu otrzymujemy diffa między aktualnym, a oczekiwanym rezultatem. Podejrzewam, że nadal nie jest to wystarczająco jasne, dlatego rzućmy okiem na przykład.

Załóżmy, że chcemy przetestować wynik renderowania komponentu `Article` w React:

```js
import React, { Component } from "react";

class Article extends Component {
  render() {
    return (
      <div className="article">
        <header className="article-header">{this.props.title}</header>
        {this.props.children}
      </div>
    );
  }
}

export default Article;
```

Tworzymy do niego nasz pierwszy snapshot test.

```js
import React from "react";
import Article from "./Article.js";
import renderer from "react-test-renderer";

it("renders correctly", () => {
  const tree = renderer
    .create(<Article title="Title">The contents</Article>)
    .toJSON();
  expect(tree).toMatchSnapshot();
});
```

Zauważmy, że używamy `react-test-renderer`, by stworzyć instancję komponentu, a następnie wywołujemy metodę `toJSON`. Mówi to nam o tym, że efekt renderowania tego komponentu będzie serializowany do stringa. W asercji oczekujemy, że rezultat będzie odpowiadał snapshotowi.

**Ale co to ten snapshot i gdzie on się znajduje?**

Gdy pierwszy raz uruchomimy ten test zauważymy, że obok komponentu pojawił się katalog `__snapshots__` z plikiem o takiej zawartości:

```js
exports[`renders correctly 1`] = `
<div
  className="article"
>
  <header
    className="article-header"
  >
    Title
  </header>
  The contents
</div>
`;
```

To jest właśnie snapshot, stworzony przy pierwszym uruchomieniu testu, do którego będziemy z każdym kolejnym odpaleniem testu porównywać wynik. Widzimy, że jest to zserializowany wynik wywołania funkcji render, zapis w postaci tekstowej drzewa DOM, które zostałoby wygenerowane dla tego komponentu.

## Praca ze snapshotami

Przejdźmy teraz może przez cały proces pracy z snapshotami, żeby sobie go utrwalić.

1. Pierwsze uruchomienie testu, generuje nam bazowy snapshot.
2. Snapshot jest przechowywany w repozytorium jako wzorzec prawidłowego rezultatu testu.
3. Za każdym razem, gdy wprowadzamy jakieś zmiany w aplikacji, uruchamiamy testy i sprawdzamy czy ich wyniki są nadal prawidłowe.
4. Jeśli w wyniku naszych zmian, wzorzec w postaci snapshota musi ulec zmianie jesteśmy w stanie go nadpisać za pomocą komendy `jest -u`.

Ponieważ snapshot jest przechowywany w repozytorium każda jego zmiana jest częścią naszych pull requestów, co za tym idzie przechodzi również code review. Jest to bardzo ważny etap, ponieważ pomaga zwalidować czy zmiany w snapshocie nie są wynikiem błędu lub są niepotrzebne.

## Ale po co?

Snapshot testy komponentów sprawdzają czy będą one wyglądać tak, jak tego oczekujemy. W szczególności pozwalają na zobaczenie, jak wygląd tego komponentu będzie się zmieniał pod wpływem różnego rodzaju propsów do niego przekazywanych. Dodatkowo, jeśli używamy jakiegoś z narzędzi, które bazuje na ustawianiu styli inline, możemy również walidować ich poprawność (skąd już bardzo blisku do visual regression testing). Nie testują one jednak zachowania komponentu, np. wykonania odpowiednej akcji po kliknięciu. Tym tematem zajmiemy się już niedługo.

Na dziś już wystarczy :) Czuję jednak, że temat nie jest wyczerpany, dlatego chciałabym poświęcić mu kolejny artykuł. Jeśli masz jakieś pytanie związane z testowaniem z użyciem snapshotów, zadaj je proszę w komentarzu, a ja postaram się na nie odpowiedzieć w kolejnym wpisie.

Oprócz testowania fukcjonalności komponentów czy kolejnego wpisu odnośnie pracy z snapshotami, w ramach naszej serii planuję również poruszyć temat testów e2e, testów dla React Native (Detox, Appium) czy visual regression testing. Na pewno znajdziecie wśród nich czegoś dla siebie, czegoś, co pozwoli Wam pisać lepsze aplikacje frontendowe 💻

Jeżeli interesuje Cię testowanie frontendu to zachęcam do zapisania się na newsletter Szkoły Testów poświęcony temu tematowi. Znajdziesz tam wiele materiałów o testowaniu, różnych narzędziach i technikach, a także dowiesz się w pierwszej kolejności o współtworzonych przeze mnie produktach związanych z testowaniem (coś fajnego się szykuje 😉). Zapisać można się [tutaj](https://szkolatestow.online/#frontend).
