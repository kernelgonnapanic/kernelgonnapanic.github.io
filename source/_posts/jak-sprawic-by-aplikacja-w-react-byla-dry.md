---
title: "Jak sprawić, by Twoja aplikacja w React była DRY?"
tags:
  - React
  - Javascript
  - Dobre praktyki
  - Frontend
keywords:
  - React
  - Higher Order Components
  - dobre praktyki React
  - wzorce React
  - render prop
thumbnailImagePosition: right
coverMeta: out
coverSize: partial
thumbnailImage: pumpkin.jpg
coverImage: pumpkin.jpg
date: 2017-10-29 13:35:00
---

Jestem przekonana, że większość z Was, spotkała się już w swojej karierze z zasadą "don't repeat yourself". Nie ważne w jakim języku programujemy, dążymy do tego, by nasz kod był [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). Z tego powodu korzystamy z różnego rodzaju abstrakcji czy wzorców, które pozwalają nam na uniknięcie kopiowana fragmentów kodu i konieczności późniejszego ich utrzymywania. Dziś chciałabym pokazać Wam 2 wzorce, które możecie zastosować w przypadku aplikacji bazujących na React'cie.
<!-- more -->
Wyobraźmy sobie klasyczną aplikację React'ową. Składa się ona z wielu komponentów, a jej rozszerzanie i rozbudowywanie zazwyczaj łączy się z tworzeniem kolejnych. Załóżmy, że naszym dzisiejszym zadaniem jest dodanie animującego się header'a. Chcielibyśmy, by początkowo był on przeźroczysty (opacity: 0) i w raz ze scrollowaniem strony, był coraz bardziej widoczny (aż do opacity: 1). Końcowym efektem jest to, co widzicie na gifie poniżej.

{% image center fig-100 hoc.gif %}

Pierwszym naszym rozwiązaniem jest umieszczenie kodu odpowiedzialnego za tę funkcjonalność w komponencie, który wyświetla header i listę.

{% codeblock DummyPage.js lang:js https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/pages/DummyPage.js DummyPage.js %}
class DummyPage extends Component {
  constructor() {
    super();
    this.state = {
      scrollPos: 0,
    };
    this.scrollView = null;
    this.handleScroll = this.handleScroll.bind(this);
    this.calculateOpacity = this.calculateOpacity.bind(this);
  }
  calculateOpacity() {
    if(!this.state.scrollPos) return 0;
    if (this.state.scrollPos > 200) return 1;
    return this.state.scrollPos / 200;
  }
  handleScroll() {
    if(!this.scrollView) return;
    const scrollPos = this.scrollView.scrollTop;
    this.setState({ scrollPos });
  }
  render() {
    return (
      <div
        className="container"
        onScroll={this.handleScroll}
        ref={ref => this.scrollView = ref}
      >
        <Header
          opacity={this.calculateOpacity()}
          text="Dummy page"
        />
        <List />
      </div>
    );
  }
}
{% endcodeblock %}

Wszystko pięknie śmiga, więc jesteśmy zadowoleni. Jednak za kilka dni, okazuje się, że to rozwiązanie tak przypadło użytkownikom do gustu, że chcielibyśmy je zastosować w innych miejscach aplikacji. I co teraz? Wiemy dobrze, że kopiowanie kodu odpowiedzialnego za animowanie headera to nie jest dobry pomysł. Jak sprawić, byśmy mogli użyć tego zachowania w wielu miejscach aplikacji?

## Higher Order Component

Zacznijmy od krótkiego wstępu i powiedzenia kilku słów wyjaśnienia czym są **Higher Order Components** . HOC (używając skróconej nazwy komponentu wyższego rzędu) jest funkcją, która bierze jako argument komponent i zwraca nowy komponent. W ten sposób jesteśmy w stanie oddzielić pewną logikę, zamknąć ją w tejże funkcji i przekazując do niej różnego rodzaju komponenty, w pewien sposób powiększać ich możliwości.

Zobaczmy jak wygląda to w przypadku naszej mini-aplikacji. Spróbujmy zaimplementować tę samą funkcjonalność, lecz oddzielić logikę odpowiedzialną za animowanie headera do naszego HOCa.

  {% codeblock PageWithHoc.js lang:js https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/pages/PageWithHoc.js PageWithHoc.js %}
import withAnimatedHeader from '../enhancers/withAnimatedHeader';

const PageWithHoc = ({ opacity }) => (
  <div>
    <Header
      blue
      opacity={opacity}
      text="Page with HOC"
    />
    <List/>
  </div>
);

export default withAnimatedHeader(PageWithHoc);
  {% endcodeblock %}

Widzimy, że komponent zawierający header i listę znacząco się odchudził. Ale możemy też zauważyć, że nie jest on już eksportowany. Eksportujemy rezultat wywyołania funkcji `withAnimatedHeader`, do której przekazaliśmy nasz komponent. Czym jest ta funkcja? Dobrze myślicie, to jest właśnie Higher Order Component.

Teraz sprawdźmy jak wygląda funkcja `withAnimatedHeader` czyli komponent wyższego rzędu.
  {% codeblock withAnimatedHeader.js lang:js https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/enhancers/withAnimatedHeader.js withAnimatedHeader.js %}
const withAnimatedHeader = (WrappedComponent) => {
  return class extends Component {
    constructor() {
      super();
      this.state = {
        scrollPos: 0,
      };
      this.scrollView = null;
      this.handleScroll = this.handleScroll.bind(this);
      this.calculateOpacity = this.calculateOpacity.bind(this);
    }
    calculateOpacity() {
      if(!this.state.scrollPos) return 0;
      if (this.state.scrollPos > 200) return 1;
      return this.state.scrollPos / 200;
    }
    handleScroll() {
      if(!this.scrollView) return;
      const scrollPos = this.scrollView.scrollTop;
      this.setState({ scrollPos });
    }
    render() {
      return (
        <div
          className="container"
          onScroll={this.handleScroll}
          ref={ref => this.scrollView = ref}
        >
          <WrappedComponent {...this.props} opacity={this.calculateOpacity()} />
        </div>
      );
    }
  };
}

export default withAnimatedHeader;
  {% endcodeblock %}

Widzimy, że to właśnie tutaj jest zamknięta logika animacji. `WithAnimatedHeader` zwraca nowy komponent, który zdefiniowane ma metody `calculateOpacity` i `handleScroll`. Komponent ten, renderując się, tworzy kontener, który będzie obsługiwał scroll'a a następnie renderuje komponent, który przekazaliśmy jako argument do funkcji.

Więcej na temat Higher Order Components możesz znaleźć w dokumentacji [React'a](https://reactjs.org/docs/higher-order-components.html).


## Function as children


Kolejnym wzorcem, który pozwala na oddzielenie i reużywanie części logiki jest wykorzystanie **function as children**. Z pewnością spotkaliście się z użyciem `this.props.children` jako sposobu na zwiększenie komponowalności waszego React'owego kodu. (Jeśli nie, [tutaj](http://krasimirtsonev.com/blog/article/children-in-jsx) jest kilka informacji na ten temat). Ale czy wiedzieliście, że jako children możemy przekazać funkcję?

Spójrzmy na przykład :)

  {% codeblock PageWithRenderCallback.js lang:js https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/pages/PageWithRenderCallback.js PageWithRenderCallback.js %}
import ScrollViewWithAnimatedHeader from '../enhancers/ScrollViewWithAnimatedHeader';

const PageWithRenderCallback = ({ opacity }) => (
  <ScrollViewWithAnimatedHeader>
    {
      (opacity) => (
        <div>
          <Header
            green
            opacity={opacity}
            text="Page with render callback"
          />
          <List/>
        </div>
      )
    }
  </ScrollViewWithAnimatedHeader>
);

export default PageWithRenderCallback;
  {% endcodeblock %}

Znów widzimy, że nasz komponent zawierający Header i Listę jest malutki, ale renderuje w środku komponent `ScrollViewWithAnimatedHeader`. Ten z kolei przyjmuje jako children funkcję. Ta funkcja zostanie w trakcie renderowania wywołana z argumentem opacity, który możemy przekazać headerowi.

Z czego składa się `ScrollViewWithAnimatedHeader`?

  {% codeblock ScrollViewWithAnimatedHeader.js lang:js https://github.com/kernelgonnapanic/hoc-render-callback-example/blob/master/src/enhancers/ScrollViewWithAnimatedHeader.js ScrollViewWithAnimatedHeader.js %}

class ScrollViewWithAnimatedHeader extends Component {
  constructor() {
    super();
    this.state = {
      scrollPos: 0,
    };
    /* ... */
  }
  calculateOpacity() {
    /* ... */
    return opacity;
  }
  handleScroll() {
    /* ... */
  }
  render() {
    return (
      <div
        className="container"
        onScroll={this.handleScroll}
        ref={ref => this.scrollView = ref}
      >
        {this.props.children(this.calculateOpacity())}
      </div>
    );
  }
};

export default ScrollViewWithAnimatedHeader;
  {% endcodeblock %}

Jest to zwykły komponent, który dodatkowo w metodzie render wywołuje funkcję przekazaną jako `this.props.children` i przekazuje jej jako argument wyliczoną wartość opacity. To nie jest wcale takie trudne, prawda?

## Różnice
Pokazałam Wam 2 wzorce, które możecie zastosować, by wydzielić logikę pewnej funkcjonalności i sprawić, by wasz kod w React był bardziej DRY. Teraz całkiem prawdopodobne, że pojawi się pytanie: który z nich wybrać?
Jeśli wziąć pod uwagę popularność rozwiązania to zdecydowanie wygrywają Higher Order Components. Są bardzo często używane w środowisku React'owym, a jako przykład można podać `connect` z `react-redux`, które pewnie wielu z was kojarzy. Function as children nie jest tak popularne, ale niektóre biblioteki też korzystają z tego wzorca (np. `react-motion`).
Jeśli jednak przyjrzymy się konkretom to lepiej wypada function as children. Nie jest to widoczne na pierwszy rzut oka, w momencie gdy mamy do czynienia z jedną funkcjonalnością. Lecz gdybyśmy chcieli komponować kilka takich funkcjonalności ze sobą, to rozwiązanie prezentuje swoją siłę. (Jeśli chcecie dowiedzieć się więcej na ten temat zapraszam do obejrzenia [tego talka](https://www.youtube.com/watch?v=BcVAq3YFiuc&t=6s), który był też inspiracją do moich dzisiejszych poczynań).

Mam nadzieję, że dzisiejszy artykuł pomoże Wam lepiej organizować logikę w waszych aplikacjach.
Repozytorium z kodem, który stworzyłam w ramach tego przykładu jest [tutaj](https://github.com/kernelgonnapanic/hoc-render-callback-example).

Do następnego!
Ania
