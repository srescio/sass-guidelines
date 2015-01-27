
# Sintassi e formattazione

A mio parere, la primissima cosa che una styleguide dovrebbe fare è descrivere come vogliamo che appaia il codice.

Quando più sviluppatori sono coinvolti nella scrittura del CSS su uno stesso progetto, è solo una questione di tempo prima che ognuno inizi a fare le cose a modo proprio. Le lnee guida sul codice che promuovono la consistenza non solo prevengono questa situazione, ma aiutano anche nella lettura e nell'aggiornamento del codice.

Grosso modo, è auspicabile (sfacciatamente ispirato a [CSS Guidelines](http://cssguidelin.es/#syntax-and-formatting)):

* due (2) spazi per indentazione, niente tabs;
* idealmente, righe larghe 80 caratteri;
* regole CSS scritte correttamente su più righe;
* uso significativo degli spazi bianchi.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  display: block;
  overflow: hidden;
  padding: 0 1em;
}

// Sbagliato
.foo {
    display: block; overflow: hidden;

    padding: 0 1em;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Dato che la sintassi predefinita di Sass costringe a questi standard di scrittura
// Non c'è un modo sbagliato di procedere
.foo
  display: block
  overflow: hidden
  padding: 0 1em
{% endhighlight %}
  </div>
</div>

Non ci occuperemo della questione relativa all'organizzazione dei file in questa sezione. Sarà l'oggetto di [un'altra sezione](#architecture).






## Stringhe

Il CSS non richiede che le stringhe siano virgolettate, neanche quando contengono degli spazi. Prendiamo i nomi delle font-family oer esempio: non importa se li racchiudi o meno tra virgolette per il parser CSS.

Per questo motivo, Sass *a sua volta* non richiede che le stringhe siano virgolettate. Ancora meglio (e *fortunatamente*, se mi concedi), una stringa virgolettata è strettamente equivalente alla sua controparte senza virgolette (e.g. `'abc'` è strettamente equivalente a `abc`).

Detto questo, i linguaggi che non richiedono che le stringhe siano virgolettate sono certametne una minoranza, per questo **le stringhe dovrebbero sempre essere virgolettate con apici singoli** in Sass (singoli perché più semplici da scrivere dei doppi su tastiere *qwerty*). Oltre alla consistenza con gli altri linguaggi, incluso il cugino del CSS ovvero JavaScript, ci sono vari motivi per questa scelta:

* i nomi dei colori sono trattati come colori se non virgolettati, il che può portare a seri problemi;
* la maggior parte degli evidenziatori di sintassi hanno problemi con le stringhe non virgolettate;
* aiuta in generale la leggibilità;
* non ci sono ragioni valide per non quotare le stringhe.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif;

// Sbagliato
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif;

// Sbagliato
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$font-stack: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif

// Sbagliato
$font-stack: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif

// Sbagliato
$font-stack: Helvetica Neue Light, Helvetica, Arial, sans-serif
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>Nell'esempio precedente, <code>sans-serif</code> non è virgolettato perchè è un valore specifico del CSS che deve rimanere tale.</p>
</div>

anche le URL dovrebbero essere virgolettate, per le stesse ragioni di cui sopra:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  background-image: url('/images/kittens.jpg');
}

// Sbagliato
.foo {
  background-image: url(/images/kittens.jpg);
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
.foo
  background-image: url('/images/kittens.jpg')

// Sbagliato
.foo
  background-image: url(/images/kittens.jpg)
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [All You Ever Need to Know About Sass Interpolation](http://webdesign.tutsplus.com/tutorials/all-you-ever-need-to-know-about-sass-interpolation--cms-21375)
* [SassyStrings](https://github.com/HugoGiraudel/SassyStrings)






## Numeri

In Sass, un numero è un tipo di dato che include tutto, dai numeri senza unità alle lunghezze, durata, frequenze, angoli e così via. Questo consente di effettuare calcoli su tutte queste misure.



### Zero

I numeri dovrebbero mostrare lo zero prima di un valore decimale inferiore a uno. Lo zero finale non è necessario.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  padding: 2em;
  opacity: 0.5;
}

// Sbagliato
.foo {
  padding: 2.0em;
  opacity: .5;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
.foo
  padding: 2em
  opacity: 0.5

// Sbagliato
.foo
  padding: 2.0em
  opacity: .5
{% endhighlight %}
  </div>
</div>



### Unità

Quando si tratta di lunghezze, un valore `0` non dovrebbe mai avere unità.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$length: 0;

// Sbagliato
$length: 0em;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$length: 0

// Sbagliato
$length: 0em
{% endhighlight %}
  </div>
</div>

L'errore più comune che mi viene in mente riguardo ai numeri in Sass, è pensare che le unità siano solo delle stringhe che possono essere tranquillamente affisse ad un numero. Anche se sembra così, non è così che funzionano le unità. Pensa alle unità come dei simboli algebrici. Per esempio, nel mondo reale, moltiplicare 5 pollici per 5 pollici restituisce 25 pollici quadrati. La stessa logica si applica in Sass. 

Per aggiungere una unità ad un numero, devi moliplicare il numero per *1 unità*.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$value: 42;

// Giusto
$length: $value * 1px;

// Sbagliato
$length: $value + px;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$value: 42

// Giusto
$length: $value * 1px

// Sbagliato
$length: $value + px
{% endhighlight %}
  </div>
</div>

Nota che sommare *un valore 0 di una unità* funziona ugualmente, ma consiglierei il metodo di cui sopra dato che sommare *0 unità* può essere un po confusionario. Naturalmente, se si cerca di convertire un numero verso un'altra unità, sommare 0 all'unità preesistente non funzionerà.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$value: 42 + 0px;
// -> 42px

$value: 1in + 0px;
// -> 1in

$value: 0px + 1in;
// -> 96px
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$value: 42 + 0px
// -> 42px

$value: 1in + 0px
// -> 1in

$value: 0px + 1in
// -> 96px
{% endhighlight %}
  </div>
</div>

Alla fine molto dipende da ciò che cerchi di ottenere. Tieni solo a mente che sommare le unità come stringhe non è un buon modo di procedere.

Per rimuoverè l'unità da un valore, devi dividerlo per *una unità del suo stesso tipo*.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$length: 42px;

// Giusto
$value: $length / 1px;

// Sbagliato
$value: str-slice($length + unquote(''), 1, 2);
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$length: 42px

// Giusto
$value: $length / 1px

// Sbagliato
$value: str-slice($length + unquote(''), 1, 2)
{% endhighlight %}
  </div>
</div>

Appendere una unità come stringa ad un numero risulta in una stringa, impedendo ulteriori operazioni sul valore. Dividire la parte numerica di un numero con una unità dà nuovamente come risultato una stringa. Non è in genere quello che si vuole.



### Calcoli

**Calcoli numerici di primo livello dovrebbero sempre essere racchiusi tra parentesi**. Non solo questo requisito migliora drasticamente la leggibilità, previene anche alcuni casi limite costringendo Sass ad elaborare i contenuti delle parentesi.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  width: (100% / 3);
}

// Sbagliato
.foo {
  width: 100% / 3;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
.foo
  width: (100% / 3)

// Sbagliato
.foo
  width: 100% / 3
{% endhighlight %}
  </div>
</div>



### Numeri Magici

"Numero magico" è un [termine informatico](http://en.wikipedia.org/wiki/Magic_number_(programming)#Unnamed_numerical_constants) che stà per *costante numerica senza nome*. Basilarmente, è un numero randomico che *semplicemente funziona*™ senza essere legato ad alcuna spiegazione logica.

Inutile dire che **i numeri magici sono una piaga e dovrebbero essere evitati a tutti i costi**. Quando non riesci a trovare una spiegazione ragionevole sul perchè un determinato numero funziona, aggiungi un commento esplicativo che argomenti in che comodo sei arrivato ad ottenerlo e perchè pensi che funzioni. Ammettere di non sapere perché qualcosa funziona è comunque più utile per il prossimo sviluppatore piuttosto che costringerlo a cercare di capire la situazione da zero.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/**
 * 1. Numero magico. questo valore è il più basso che ho trovato per allineare il margine superiore di 
 * `.foo` con il suo genitore. Idealmente, dovremmo aggiustarlo correttamente.
 */
.foo {
  top: 0.327em; /* 1 */
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/**
 * 1. Numero magico. questo valore è il più basso che ho trovato per allineare il margine superiore di
 * `.foo` con il suo genitore. Idealmente, dovremmo aggiustarlo correttamente.
 */
.foo
  top: 0.327em /* 1 */
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [Use Lengths, Not Strings](http://hugogiraudel.com/2013/09/03/use-lengths-not-strings/)
* [Correctly Adding Unit to Number](http://css-tricks.com/snippets/sass/correctly-adding-unit-number/)
* [Magic Numbers in CSS](http://css-tricks.com/magic-numbers-in-css/)
* [Sassy-Math](https://github.com/at-import/sassy-math)






## Colori

I colori sono una parte importante del linguaggio CSS. Naturalmente, Sass è un alleato prezioso quando si tratta di manipolare i colori, soprattutto mettendo a disposizione delle [funzioni potenti](http://sass-lang.com/documentation/Sass/Script/Functions.html).



### Formati dei colori

In modo da rendere i colori semplici da gestire, il mio consiglio è di rispettare il seguente ordine di preferenza per il formato dei colori:

1. [Parole chiave colori CSS](http://www.w3.org/TR/css3-color/#svg-color);
1. [Notazione HSL](http://en.wikipedia.org/wiki/HSL_and_HSV);
1. [Notazione RGB](http://en.wikipedia.org/wiki/RGB_color_model);
1. Notazione esadecimale. Preferibilmente in minuscolo ed abbreviata quando possibile.

Per i principianti, le parole chiave spesso sono auto esplicative. La rappresentazione HSL non è solo la più semplice da comprendere per il cervello umano<sup>[citazione necessaria]</sup>, rende anche più semplice agli autori dei fogli di stile modificare il colore aggiustando tonalità, saturazione e luminosità individualmente. RGB ha il beneficio di evidenziare subito se un colore è più tendente al blu, verde o rosso ma non facilita la creazione di un colore composto di queste tre parti. Infine, gli esadecimali sono quasi indecifrabili per la mente umana.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  color: red;
}

// Sbagliato
.foo {
  color: #FF0000;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
.foo
  color: red

// Sbagliato
.foo
  color: #FF0000
{% endhighlight %}
  </div>
</div>

Quando si usa la notazione HSL o RGB, è bene aggiungere uno spazio singolo dopo una virgola (`,`) e nessuno spazio tra le parentesi (`(`, `)`) ed il contenuto.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo {
  color: rgba(0, 0, 0, 0.1);
  background: hsl(300, 100%, 100%);
}

// Sbagliato
.foo {
  color: rgba(0,0,0,0.1);
  background: hsl( 300, 100%, 100% );
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
.foo
  color: rgba(0, 0, 0, 0.1)
  background: hsl(300, 100%, 100%)

// Sbagliato
.foo
  color: rgba(0,0,0,0.1)
  background: hsl( 300, 100%, 100% )
{% endhighlight %}
  </div>
</div>



### Colori e variabili

Quando si usa un colore più di una volta, memorizzalo in una variabile con un nome significativo che rappresenti il colore.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$sass-pink: #c69;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$sass-pink: #c69
{% endhighlight %}
  </div>
</div>

Ora sei libero di usare questa variabile ovunque tu voglia. Tuttavia, se il suo utilizzo è strettamente legato ad un tema, sconsiglierei di usare la variabile così com'è. Salvalo invece in un'altra variabile con un nome che spiega come dovrebbe essere usato.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$main-theme-color: $sass-pink;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$main-theme-color: $sass-pink
{% endhighlight %}
  </div>
</div>

Così facendo si evita che un cambio di tema possa portare a qualcosa come `$sass-pink: blue`.



### Schiarire e scurire i colori



Le funzioni [`lighten`](http://sass-lang.com/documentation/Sass/Script/Functions.html#lighten-instance_method) e [`darken`](http://sass-lang.com/documentation/Sass/Script/Functions.html#darken-instance_method) manipolano la luminosità di un colore nello spazio HSL aggiungendo o sottraendo luminosità. Basilarmente non sono altro che degli alias per il parametro `$lightness` della funzione [`adjust-color`](http://sass-lang.com/documentation/Sass/Script/Functions.html#adjust_color-instance_method).

Il fatto è che queste funzioni spesso non danno il risultato che ci si aspetta. La funzione [`mix`](http://sass-lang.com/documentation/Sass/Script/Functions.html#mix-instance_method) invece è un buon modo di schiarire o scurire un colore mischiandolo con bianco `white` o il nero `black`.

Il benefico di usare `mix` invece di una delle due funzioni menzionate sopra è che il colore tenderà gradualmente al bianco o al nero in base a quanto diminuisce la proporzione con il colore, mentre `darken` e `lighten` vanno rapidamente a sovrascrivere un colore con il bianco o il nero.

<figure role="group">
  <img src="/assets/images/lighten-darken-mix.png" alt="Illustrazione della differenza tra le funzioni Sass lighten/darken e mix" />
  <figcaption>Illustrazione della differenza tra <code>lighten</code>/<code>darken</code> e <code>mix</code> di <a href="http://codepen.io/KatieK2/pen/tejhz/" target="_blank">KatieK</a></figcaption>
</figure>

Se non vuoi scrivere la funzione `mix` ogni volta, puoi creare due funzioni `tint` e `shade` semplici da usare (che fanno anche parte di [Compass](http://compass-style.org/reference/compass/helpers/colors/#shade)) per fare la stessa cosa:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Schiarisce leggermente un colore
/// @access public
/// @param {Color} $color - color to tint
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function tint($color, $percentage) {
  @return mix($color, white, $percentage);
}

/// Scurisce leggermente un colore
/// @access public
/// @param {Color} $color - color to shade
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function shade($color, $percentage) {
  @return mix($color, black, $percentage);
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Schiarisce leggermente un colore
/// @access public
/// @param {Color} $color - color to tint
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function tint($color, $percentage)
  @return mix($color, white, $percentage)

/// Scurisce leggermente un colore
/// @access public
/// @param {Color} $color - color to shade
/// @param {Number} $percentage - percentage of `$color` in returned color
/// @return {Color}
@function shade($color, $percentage)
  @return mix($color, black, $percentage)
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>La funzione <a href="http://sass-lang.com/documentation/Sass/Script/Functions.html#scale_color-instance_method"><code>scale-color</code></a> è pensata per scalare le proprietà in maniera più fluida prendendo in considerazione quanto sono già alte o basse. Dovrebbe dare dei risultati simili a <code>mix</code> ma con una convenzione più chiara. Tuttavia il fattore di scala non è esattamente uguale.</p>
</div>



### Letture Aggiuntive

* [A Visual Guide to Sass & Compass Color Functions](http://jackiebalzer.com/color)
* [How to Programmatically Go From One Color to Another](http://thesassway.com/advanced/how-to-programtically-go-from-one-color-to-another-in-sass)
* [Sass Color Variables That Don't Suck](http://davidwalsh.name/sass-color-variables-dont-suck)
* [Using Sass to Build Color Palettes](http://www.sitepoint.com/using-sass-build-color-palettes/)
* [Dealing with Color Schemes in Sass](http://www.sitepoint.com/dealing-color-schemes-sass/)






## Liste

Le liste sono l'equivalente di Sass degli array. Una lista è una struttura di dati piatta (diversamente dalle [mappe](#maps)) intesa per memorizzare valori di ogni tipo (incluse liste, permettendo annidamenti di liste).

Le liste dovrebbero rispettare le seguenti linee guida:

* a meno che non siano troppo lunghe per rientrare in una riga di 80 caratteri, mostrarle sempre su una riga singola;
* a meno che non sia utilizzata così com'è per usarla nel CSS, separe sempre gli elementi con una virgola;
* a meno che non sia vuota o annidata in un altra lista, non usare mai le parentesi;
* non aggiungere mai una virgola finale.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$font-stack: 'Helvetica', 'Arial', sans-serif;

// Sbagliato
$font-stack:
  'Helvetica',
  'Arial',
  sans-serif;

// Sbagliato
$font-stack: 'Helvetica' 'Arial' sans-serif;

// Sbagliato
$font-stack: ('Helvetica', 'Arial', sans-serif);

// Sbagliato
$font-stack: ('Helvetica', 'Arial', sans-serif,);
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$font-stack: 'Helvetica', 'Arial', sans-serif

// Sbagliato (dato che non è supportato)
$font-stack:
  'Helvetica',
  'Arial',
  sans-serif

// Sbagliato
$font-stack: 'Helvetica' 'Arial' sans-serif

// Sbagliato
$font-stack: ('Helvetica', 'Arial', sans-serif)

// Sbagliato
$font-stack: ('Helvetica', 'Arial', sans-serif,)
{% endhighlight %}
  </div>
</div>

Quando si aggiungono nuovi elementi ad una lista, usare sempre le API. Non cercare di aggiungere nuovi elementi manualmente.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$shadows: 0 42px 13.37px hotpink;

// Giusto
$shadows: append($shadows, $shadow, comma);

// Sbagliato
$shadows: $shadows, $shadow;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$shadows: 0 42px 13.37px hotpink

// Giusto
$shadows: append($shadows, $shadow, comma)

// Sbagliato
$shadows: $shadows, $shadow
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [SassyLists](http://sassylists.com)






## Maps

Since Sass 3.3, stylesheet authors can define maps &mdash; the Sass term for associative arrays, hashes or even JavaScript objects. A map is a data structure mapping keys (that can be any data type, including maps although I wouldn't recommend it) to values of any type.

Maps should be written as follows:

* space after the colon (`:`);
* opening brace (`(`) on the same line as the colon (`:`);
* **quoted keys** if they are strings (which represents 99% of the cases);
* each key/value pair on its own new line;
* comma (`,`) at the end of each key/value;
* **trailing comma** (`,`) on last item to make it easier to add, remove or reorder items;
* closing brace (`)`) on its own new line;
* no space or new line between closing brace (`)`) and semi-colon (`;`).

Illustration:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Yep
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);

// Nope
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Yep
$breakpoints: ('small': 767px, 'medium': 992px, 'large': 1200px,)

// Nope
$breakpoints: ( 'small': 767px, 'medium': 992px, 'large': 1200px )

// Nope
$breakpoints: (small: 767px, medium: 992px, large: 1200px,)

// Nope (since it is not supported)
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
)
{% endhighlight %}
  </div>
</div>



### Debugging a Sass map

If you ever find yourself lost, wondering what kind of crazy magic is happening in a Sass map, worry not because there is still a way to be saved.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
@mixin debug-map($map) {
  @at-root {
    @debug-map {
      __toString__: inspect($map);
      __length__: length($map);
      __depth__: if(function-exists('map-depth'), map-depth($map), null);
      __keys__: map-keys($map);
      __properties__ {
        @each $key, $value in $map {
          #{'(' + type-of($value) + ') ' + $key}: inspect($value);
        }
      }
    }
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
=debug-map($map)
  @at-root
    @debug-map
      __toString__: inspect($map)
      __length__: length($map)
      __depth__: if(function-exists('map-depth'), map-depth($map), null)
      __keys__: map-keys($map)
      __properties__
        @each $key, $value in $map
          #{'(' + type-of($value) + ') ' + $key}: inspect($value)
{% endhighlight %}
  </div>
</div>

If you are interested in knowing the depth of the map, add the following function. The mixin will display it automatically.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Compute the maximum depth of a map
/// @param {Map} $map
/// @return {Number} max depth of `$map`
@function map-depth($map) {
  $level: 1;

  @each $key, $value in $map {
    @if type-of($value) == 'map' {
      $level: max(map-depth($value) + 1, $level);
    }
  }

  @return $level;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Compute the maximum depth of a map
/// @param {Map} $map
/// @return {Number} max depth of `$map`
@function map-depth($map)
  $level: 1

  @each $key, $value in $map
    @if type-of($value) == 'map'
      $level: max(map-depth($value) + 1, $level)

  @return $level;
{% endhighlight %}
  </div>
</div>



### Further reading

* [Using Sass Maps](http://www.sitepoint.com/using-sass-maps/)
* [Debugging Sass Maps](http://www.sitepoint.com/debugging-sass-maps/)
* [Real Sass, Real Maps](http://blog.grayghostvisuals.com/sass/real-sass-real-maps/)
* [Sass Maps are Awesome](http://viget.com/extend/sass-maps-are-awesome)
* [Sass list-maps](https://github.com/lunelson/sass-list-maps)
* [Sass Maps Plus](https://github.com/lunelson/sass-maps-plus)
* [Sassy-Maps](https://github.com/at-import/sassy-maps)
* [Introduction to Sass Maps Usage and Examples](http://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)






## CSS Ruleset

At this point, this is mostly revising what everybody knows, but here is how a CSS ruleset should be written (at least, according to most guidelines, including [CSS Guidelines](http://cssguidelin.es/#anatomy-of-a-ruleset)):

* related selectors on the same line; unrelated selectors on new lines;
* the opening brace (`{`) spaced from the last selector by a single space;
* each declaration on its own new line;
* a space after the colon (`:`);
* a trailing semi-colon (`;`) at the end of all declarations;
* the closing brace (`}`) on its own new line;
* a new line after the closing brace `}`.

Illustration:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Yep
.foo, .foo-bar,
.baz {
  display: block;
  overflow: hidden;
  margin: 0 auto;
}

// Nope
.foo,
.foo-bar, .baz {
    display: block;
    overflow: hidden;
    margin: 0 auto }
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Yep
.foo, .foo-bar,
.baz
  display: block
  overflow: hidden
  margin: 0 auto

// Nope
.foo,
.foo-bar, .baz
    display: block
    overflow: hidden
    margin: 0 auto
{% endhighlight %}
  </div>
</div>

Adding to those CSS-related guidelines, we want to pay attention to:

* local variables being declared before any declarations, then spaced from declarations by a new line;
* mixin calls with no `@content` coming before any declaration;
* nested selectors always coming after a new line;
* mixin calls with `@content` coming after any nested selector;
* no new line before a closing brace (`}`).

Illustration:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo, .foo-bar,
.baz {
  $length: 42em;

  @include ellipsis;
  @include size($length);
  display: block;
  overflow: hidden;
  margin: 0 auto;

  &:hover {
    color: red;
  }

  @include respond-to('small') {
    overflow: visible;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo, .foo-bar,
.baz
  $length: 42em

  +ellipsis
  +size($length)
  display: block
  overflow: hidden
  margin: 0 auto

  &:hover
    color: red

  +respond-to('small')
    overflow: visible
{% endhighlight %}
  </div>
</div>



### Further reading

* [Anatomy of a Ruleset](http://cssguidelin.es/#anatomy-of-a-ruleset)






## Declaration Sorting

I cannot think of many topics where opinions are as divided as they are regarding declaration sorting in CSS. Concretely, there are two factions here:

* sticking to the alphabetical order;
* ordering declarations by type (position, display, colors, font, miscellaneous...).

There are pros and cons for both ways. On one hand, alphabetical order is universal (at least for languages using the latin alphabet) so there is no argument about sorting one property before another. However, it seems extremely weird to me to see properties such as `bottom` and `top` not right next to each other. Why would animations should appear before the display type? There are a lot of oddities with alphabetical ordering.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  background: black;
  bottom: 0;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
  height: 100px;
  overflow: hidden;
  position: absolute;
  right: 0;
  width: 100px;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  background: black
  bottom: 0
  color: white
  font-weight: bold
  font-size: 1.5em
  height: 100px
  overflow: hidden
  position: absolute
  right: 0
  width: 100px
{% endhighlight %}
  </div>
</div>

On the other hand, ordering properties by type makes perfect sense. Every font-related declarations are gathered, `top` and `bottom` are reunited and reading a ruleset kind of feels like reading a short story. But unless you stick to some conventions like [Idiomatic CSS](https://github.com/necolas/idiomatic-css), there is a lot of room for interpretation in this way of doing things. Where would `white-space` go: font or display? Where does belong `overflow` exactly? What is the property order within a group (it could be alphabetically, oh the irony)?

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  height: 100px;
  width: 100px;
  overflow: hidden;
  position: absolute;
  bottom: 0;
  right: 0;
  background: black;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  height: 100px
  width: 100px
  overflow: hidden
  position: absolute
  bottom: 0
  right: 0
  background: black
  color: white
  font-weight: bold
  font-size: 1.5em
{% endhighlight %}
  </div>
</div>

There is also another interesting subtree of type ordering called [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS), that seems to be quite popular as well. Basically, Concentric CSS relies on the box-model to define an order: starts outside, moves inward.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  width: 100px;
  height: 100px;
  position: absolute;
  right: 0;
  bottom: 0;
  background: black;
  overflow: hidden;
  color: white;
  font-weight: bold;
  font-size: 1.5em;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  width: 100px
  height: 100px
  position: absolute
  right: 0
  bottom: 0
  background: black
  overflow: hidden
  color: white
  font-weight: bold
  font-size: 1.5em
{% endhighlight %}
  </div>
</div>

I must say I cannot decide myself. A [recent poll on CSS-Tricks](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/) determined that over 45% developers order their declarations by type against 14% alphabetically. Also, there are 39% that go full random, including myself.

<figure role="group">
  <img src="/assets/images/css_order_chart.png" alt="Chart showing how developers order their CSS declarations" />
  <figcaption>Chart showing how developers order their CSS declarations</figcaption>
</figure>

Because of this, I will not impose a choice in this styleguide. Pick the one you prefer, as long as you are consistent throughout your stylesheets.

<div class="note">
  <p>A <a href="http://peteschuster.com/2014/12/reduce-file-size-css-sorting/">recent study</a> shows that using <a href="https://github.com/csscomb/csscomb.js">CSS Comb</a> (which uses <a href="https://github.com/csscomb/csscomb.js/blob/master/config/csscomb.json">type ordering</a>) for sorting CSS declarations ends up shortening the average file size under Gzip compression by 2.7%, compared to 1.3% when sorting alphabetically.</p>
</div>



### Further reading

* [CSS Comb](https://github.com/csscomb/csscomb.js)
* [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [On Declaration Sorting](http://meiert.com/en/blog/20140924/on-declaration-sorting/)
* [Reduce File Size With CSS Sorting](http://peteschuster.com/2014/12/reduce-file-size-css-sorting/)
* [Poll Results: How Do You Order Your CSS Properties?](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)






## Selector Nesting

One particular feature Sass provides that is being overly misused by many developers is *selector nesting*. Selector nesting offers a way for stylesheet authors to compute long selectors by nesting shorter selectors within each others.

### General rule

For instance, the following Sass nesting:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  .bar {
    &:hover {
      color: red;
    }
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  .bar
    &:hover
      color: red
{% endhighlight %}
  </div>
</div>

... will generate this CSS:

{% highlight css %}
.foo .bar:hover {
  color: red;
}
{% endhighlight %}

Along the same lines, since Sass 3.3 it is possible to use the current selector reference (`&`) to generate advanced selectors. For instance:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  &-bar {
    color: red;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  &-bar
    color: red
{% endhighlight %}
  </div>
</div>

... will generate this CSS:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo-bar {
  color: red;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo-bar
  color: red
{% endhighlight %}
  </div>
</div>

This method is often used along with [BEM naming conventions](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) to generate `.block__element` and `.block--modifier` selectors based on the original selector (i.e. `.block` in this case).

<div class="note">
  <p>While it might be anecdotal, generating new selectors from the current selector reference (<code>&</code>) makes those selectors unsearchable in the codebase since they do not exist per se.</p>
</div>

The problem with selector nesting is that it ultimately makes code more difficult to read. One has to mentally compute the resulting selector out of the indentation levels; it is not always quite obvious what the CSS will end up being.

This statement becomes truer as selectors get longer and references to the current selector (`&`) more frequent. At some point, the risk of losing track and not being able to understand what's going on anymore is so high that it is not worth it.

To prevent such a situation, we **avoid selector nesting as much as possible**. However, there are obviously a few exceptions to this rule.

### Exceptions

For starters, it is allowed and even recommended to nest pseudo-classes and pseudo-elements within the initial selector.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  color: red;

  &:hover {
    color: green;
  }

  &::before {
    content: 'pseudo-element';
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  color: red

  &:hover
    color: green

  &::before
    content: 'pseudo-element'
{% endhighlight %}
  </div>
</div>

Using selector nesting for pseudo-classes and pseudo-elements not only makes sense (because it deals with closely related selectors), it also helps keep everything about a component at the same place.

Also, when using component-agnostic state classes such as `.is-active`, it is perfectly fine to nest it under the component's selector to keep things tidy.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  // ...

  &.is-active {
    font-weight: bold;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  // ...

  &.is-active
    font-weight: bold
{% endhighlight %}
  </div>
</div>

Last but not least, when styling an element because it happens to be contained within another specific element, it is also fine to use nesting to keep everything about the component at the same place.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  // ...

  .no-opacity & {
    display: none;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  // ...

  .no-opacity &
    display: none
{% endhighlight %}
  </div>
</div>

When working with unexperienced developers, a selector such as `.no-opacity &` might look a little weird. To prevent any confusion, you can build a very short mixin that transform this odd syntax into an explicit API.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Helper mixin to provide simple API to selector nesting
/// @param {String} $selector - Selector
@mixin when-inside($selector) {
  #{$selector} & {
    @content;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Helper mixin to provide simple API to selector nesting
/// @param {String} $selector - Selector
=when-inside($selector) {
  #{$selector} &
    @content
}
{% endhighlight %}
  </div>
</div>

Rewriting our previous example, it would look like this:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  // ...

  @include when-inside('.no-opacity') {
    display: none;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  // ...

  +when-inside('.no-opacity')
    display: none
{% endhighlight %}
  </div>
</div>

As with everything, the specifics are somewhat irrelevant, consistency is key. If you feel fully confident with selector nesting, then use selector nesting. Just make sure your whole team is okay with that.






### Further reading

* [Beware of Selector Nesting](http://www.sitepoint.com/beware-selector-nesting-sass/)
* [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
* [Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)



