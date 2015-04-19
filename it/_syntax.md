
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

Incredibile ma vero, le stringhe ricoprono un ruolo centrale sia nell'ecosistema del CSS che in Sass. La maggior parte dei valori sono o grandezze o stringhe (solitamente non virgolettate), quindi è abbastanza cruciale aderire a delle linee guida quando si usano le stringhe in Saas.

### Encoding

Per evitare potenziali problemi con la codifica dei caratteri, è fotemente consigliabile forzare la codifica [UTF-8](http://en.wikipedia.org/wiki/UTF-8) nel [foglio di stile principale](#main-file) usando la direttiva `@charset`. Assicurati che sia la prima regola del foglio di stile e che non ci sia alcun carattere prima di essa.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
@charset 'utf-8';
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
@charset 'utf-8'
{% endhighlight %}
  </div>
</div>

### Virgolette

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
$direction: 'left';

// Sbagliato
$direction: left;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$direction: 'left'

// Sbagliato
$direction: left
{% endhighlight %}
  </div>
</div>

### Stringhe come valori CSS

Specifici valori CSS come `initial` o `sans-serif` non necessitano di essere virgolettati. Invece la dichiarazione `font-family: 'sans-serif'` fallirà silentemente perchè il CSS si aspetta un identificatore, non una stringa virgolettata. Per questo motivo, non si virgolettano questi valori.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$font-type: sans-serif;

// Sbagliato
$font-type: 'sans-serif';

// Penso okay
$font-type: unquote('sans-serif');
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$font-type: sans-serif

// Sbagliato
$font-type: 'sans-serif'

// Penso okay
$font-type: unquote('sans-serif')
{% endhighlight %}
  </div>
</div>

Quindi possiamo fare una distinzione tra le stringhe intese per essere usate come valori CSS (identificatori CSS) come l'esempio precedente, e le stringhe come tipo di dato in Saas, ad esempio le chiavi delle mappe.

Non virgolettiamo le prime, ma racchiudiamo le seconde in virgolette singole.

### Stringhe contenenti virgolette

Se una stringa contiene una o più virgolette singole, si può considerare di racchiudere la stringa tra virgolette doppie (`"`), in modo da evitare di eseguire l'escape di troppi caratteri dentro la stringa.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Okay
@warn 'You can\'t do that.';

// Okay
@warn "You can't do that.";
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Okay
@warn 'You can\'t do that.'

// Okay
@warn "You can't do that."
{% endhighlight %}
  </div>
</div>

### Le URL

Le URL dovrebbero essere virgolettate, per le stesse ragioni di cui sopra:

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

L'errore più comune che mi viene in mente riguardo ai numeri in Sass, è pensare che le unità siano solo delle stringhe che possono essere tranquillamente affisse ad un numero. Anche se sembra vero, non è così che funzionano le unità. Pensa alle unità come dei simboli algebrici. Per esempio, nel mondo reale, moltiplicare 5 pollici per 5 pollici restituisce 25 pollici quadrati. La stessa logica si applica in Sass. 

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

Appendere una unità come stringa ad un numero risulta in una stringa, impedendo ulteriori operazioni sul valore. Separando la parte numerica di un numero con una unità dà nuovamente come risultato una stringa. Non è in genere quello che si vuole.



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
  <img alt="Illustrazione della differenza tra le funzioni Sass lighten/darken e mix"
     sizes="100vw"
     srcset="/assets/images/lighten-darken-mix_small.png  540w,
             /assets/images/lighten-darken-mix_medium.png 900w,
             /assets/images/lighten-darken-mix_large.png 1200w,
             /assets/images/lighten-darken-mix_huge.png  1590w" />
  <figcaption>Illustrazione della differenza tra <code>lighten</code>/<code>darken</code> e <code>mix</code> di <a href="http://codepen.io/KatieK2/pen/tejhz/" target="_blank">KatieK</a></figcaption>
</figure>

Se non vuoi scrivere la funzione `mix` ogni volta, puoi creare due funzioni `tint` e `shade` semplici da usare (che fanno anche parte di [Compass](http://compass-style.org/reference/compass/helpers/colors/#shade)) per fare la stessa cosa:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Schiarisce leggermente un colore
/// @access public
/// @param {Color} $color - colore da schiarire
/// @param {Number} $percentage - percentuale di `$color` nel colore finale
/// @return {Color}
@function tint($color, $percentage) {
  @return mix($color, white, $percentage);
}

/// Scurisce leggermente un colore
/// @access public
/// @param {Color} $color - colore da scurire
/// @param {Number} $percentage - percentuale di `$color` nel colore finale
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
/// @param {Color} $color - colore da schiarire
/// @param {Number} $percentage - percentuale di `$color` nel colore finale
/// @return {Color}
@function tint($color, $percentage)
  @return mix($color, white, $percentage)

/// Scurisce leggermente un colore
/// @access public
/// @param {Color} $color - colore da scurire
/// @param {Number} $percentage - percentuale di `$color` nel colore finale
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

* su singola riga o righe multiple;
* necessariamente su righe multiple se troppo lunghe per rientrare in una riga di 80 caratteri;
* sempre racchiuse tra parentesi;
* virgola finale se su righe multiple, oppure no se su riga singola.

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

// Sbagliato (non è supportato)
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

* [Understanding Sass lists](http://hugogiraudel.com/2013/07/15/understanding-sass-lists/)
* [SassyLists](http://sassylists.com)






## Mappe

A partire da Sass 3.3, gli autori dei fogli di stile possono definire delle mappe &mdash; il termine Sass che definisce gli array associativi, hash simili a oggetti JavaScript. Una mappa è una struttura dati che associa delle chiavi (che possono essere costituite da qualunque tipo di dato, incluse altre mappe ma lo sconsiglierei) a dei valori di qualunque tipo.

Le mappe dovrebbero essere scritte come segue:

* uno spazio dopo i due punti (`:`);
* parentesi tonda aoerta (`(`) sulla stessa riga dei due punti (`:`);
* **chiavi virgolettate** se sono stringhe (che rappresenta il 99% dei casi);
* ogni coppia chiave/valore deve stare su una propria riga;
* una virgola alla fine di ogni coppia chiave/valore;
* **virgola finale** (`,`) sull'ultimo elemento per facilitare l'aggiunta, rimozione o riordinamento degli elementi;
* parentesi tonda chiusa (`)`) su una nuova riga;
* nessuno spazio o nuova riga tra la parentesi tonda chiusa (`)`) e il punto e virgola (`;`).

Illustrazione:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
);

// Sbagliato
$breakpoints: ( small: 767px, medium: 992px, large: 1200px );
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$breakpoints: ('small': 767px, 'medium': 992px, 'large': 1200px,)

// Sbagliato
$breakpoints: ( 'small': 767px, 'medium': 992px, 'large': 1200px )

// Sbagliato
$breakpoints: (small: 767px, medium: 992px, large: 1200px,)

// Sbagliato (dato che non è supportato)
$breakpoints: (
  'small': 767px,
  'medium': 992px,
  'large': 1200px,
)
{% endhighlight %}
  </div>
</div>



### Debuggare una Sass map

Se dovessi sentirti disorientato, domandandoti che tipo di magia sia in opera all'interno di una Sass map, non preoccuparti perchè c'è un modo per uscirne.

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

Se vuoi sapere la profondità di una mappa, aggiungi la seguente funzione. Il mixin la visualizzerà automaticamente.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Calcola la profondità massima di una mappa
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
/// Calcola la profondità massima di una mappa
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



### Letture Aggiuntive

* [Using Sass Maps](http://www.sitepoint.com/using-sass-maps/)
* [Debugging Sass Maps](http://www.sitepoint.com/debugging-sass-maps/)
* [Extra Map functions in Sass](http://www.sitepoint.com/extra-map-functions-sass/)
* [Real Sass, Real Maps](http://blog.grayghostvisuals.com/sass/real-sass-real-maps/)
* [Sass Maps are Awesome](http://viget.com/extend/sass-maps-are-awesome)
* [Sass list-maps](https://github.com/lunelson/sass-list-maps)
* [Sass Maps Plus](https://github.com/lunelson/sass-maps-plus)
* [Sassy-Maps](https://github.com/at-import/sassy-maps)
* [Introduction to Sass Maps Usage and Examples](http://webdesign.tutsplus.com/tutorials/an-introduction-to-sass-maps-usage-and-examples--cms-22184)






## Regole CSS

A questo punto andiamo a rivisitare nozioni note un po a tutti, comunque questo è il modo in cui si dovrebbe scrivere un insieme di regole CSS (almeno in base alla maggior parte delle guidelines, incluso [CSS Guidelines](http://cssguidelin.es/#anatomy-of-a-ruleset)):

* selettori relazionati su una stessa riga; selettori non relazionati a capo;
* la parentesi graffa aperta (`{`) separata dall'ultimo selettore da un singolo spazio;
* ogni dichiarazione su una nuova riga;
* uno spazio dopo i due punti (`:`);
* punto e virgola di chiusura (`;`) alla fine di tutte le dichiarazioni;
* la parentesi graffa di chiusura (`}`) su una nuova riga;
* una nuova riga dopo la parentesi chiusa `}`.

Illustrazione:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
.foo, .foo-bar,
.baz {
  display: block;
  overflow: hidden;
  margin: 0 auto;
}

// Sbagliato
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

// Sbagliato
.foo,
.foo-bar, .baz
    display: block
    overflow: hidden
    margin: 0 auto
{% endhighlight %}
  </div>
</div>

In aggiunta alle guidelines sul CSS di cui sopra, bisogna fare attenzione a:

* variabili locali dichiarate prima di ogni dichiarazione, poi separate dalle dichiarazioni da una nuova riga;
* chiamate a mixin senza `@content` prima di qualunque dichiarazione;
* selettori annidati che seguono sempre dopo una nuova riga;
* chiamate a mixin con `@content` che seguono dopo selettori annidati;
* nessuna nuova riga prima di una parentesi graffa chiusa (`}`).

Illustrazione:

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



### Letture Aggiuntive

* [Anatomy of a Ruleset](http://cssguidelin.es/#anatomy-of-a-ruleset)






## Ordinamento delle Dichiarazioni

Non mi vengono in mente degli argomenti dove le opinioni sono tanto divergenti quanto per l'ordinamento delle dichiarazioni nel CSS. Concretamente, ci sono due fazioni:

* mantenere l'ordine alfabetico;
* ordinare le dichiarazioni per tipologia (position, display, colors, font, altro...).

Ci sono pro e contro in entrambi i modi. Da una parte, l'ordine alafabetico è universale (almeno per le lingue che usano l'alfabeto latino) quindi non ci sono dubbi sul mettere un proprietà prima di un'altra. Tuttavia, a me sembra molto strano vedere proprietà come `bottom` e `top` separate anzichè in sequenza. Perchè le animazioni dovrebbero apparire prima della tipologia di display? Ci sono molte stranezze con l'ordinamento alfabetico.

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

D'altra parte, ordinare le proprietà per tipologia ha molto più senso. Ogni dichiarazione relativa al font è raggruppata, `bottom` e `top` sono riuniti e leggendo un insieme di regole sembra di leggere una breve storia. Ma a meno di adottare qualche tipo di convenzione come [Idiomatic CSS](https://github.com/necolas/idiomatic-css), c'è molto spazio per l'interpretazione di quale sia il modo migliore di raggrupare le regole. Dove si collocherebbe `white-space` : font o display? A che gruppo appartiene esattamente `overflow` ? Qual'è l'ordine delle proprietà all'interno di un gruppo (potrebbe essere alfabetico, che ironia)?

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

C'è un altro interessante sottoinsieme di tipologie di ordinamento chiamato [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS), che sembra abbastanza popolare. Basilarmente, Concentric CSS si basa sul box-model per definire l'ordine: inizia dall'interno, muovendosi verso l'esterno.

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

Devo dire che non riesco a prendere una decisione. Un [sondaggio recente su CSS-Tricks](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/) ha determinato che oltre il 45% degli sviluppatori ordina le sue dichiarazioni per tipologia contro il 14% in ordine alfabetico. Inoltre, c'è un cospiquo 39% che va a braccio randomicamente, incluso il sottoscritto.

<figure role="group">
  <img src="/assets/images/css_order_chart.png" alt="Grafico che illustra come gli sviluppatori ordinano le dichiarazioni CSS" />
  <figcaption>Grafico che illustra come gli sviluppatori ordinano le dichiarazioni CSS</figcaption>
</figure>

Per questo motivo, non impongo una scelta in questa styleguide. Scegli quella che preferisci, l'importante è mantenere la consistenza in tutti i fogli di stile.

<div class="note">
  <p>Uno <a href="http://peteschuster.com/2014/12/reduce-file-size-css-sorting/">studio recente</a> mostra che l'utilizzo di <a href="https://github.com/csscomb/csscomb.js">CSS Comb</a> (che usa <a href="https://github.com/csscomb/csscomb.js/blob/master/config/csscomb.json">l'ordinamento tipologico</a>) per ordinare le dichiarazioni CSS riduce il peso medio dei file con compressione Gzip del 2.7%, rispetto all' 1.3% quando l'ordinamento è alfabetico.</p>
</div>



### Letture Aggiuntive

* [CSS Comb](https://github.com/csscomb/csscomb.js)
* [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS)
* [Idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [On Declaration Sorting](http://meiert.com/en/blog/20140924/on-declaration-sorting/)
* [Reduce File Size With CSS Sorting](http://peteschuster.com/2014/12/reduce-file-size-css-sorting/)
* [Poll Results: How Do You Order Your CSS Properties?](http://css-tricks.com/poll-results-how-do-you-order-your-css-properties/)






## Annidamento Selettori

Una particolare caratteristica che Sass mette a disposizione che viene frequentemente abusata da molti sviluppatori è *l'annidamento dei selettori*. L'annidamento dei selettori offre agli autori dei fogli di stile un modo per computare selettori lunghi annidando selettori più brevi gli uni dentro gli altri.

### Regola generale

Ad esempio, il seguente annidamento Sass:

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

... genererà questo CSS:

{% highlight css %}
.foo .bar:hover {
  color: red;
}
{% endhighlight %}

Allo stesso modo, a partire da Sass 3.3 è possibile usare il riferimento del selettore corrente (`&`) per generare selettori avanzati. Ad esempio:

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

... genererà questo CSS:

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

Questo metodo è spesso usato insieme alla [convenzione di nomenclatura BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) per generare selettori `.block__element` e `.block--modifier` basati sul selettore originale  (i.e. `.block` in questo caso).

<div class="note">
  <p>Può sembrare un aneddoto, ma generare nuovi selettori tramite il riferimento del selettore corrente (<code>&</code>) rende quei selettori non ricercabili all'interno della codebase dato che non esistono di per se.</p>
</div>

Il problema dei selettori annidati è che alla fine rendono il codice più difficile da leggere. Lo sviluppatore deve calcolare mentalmente il selettore risultante sulla base del livello di indentazione; non è sempre evidente come sarà il CSS finale.

Questa affermazione è ancora più veritiera nel momento in cui i selettori diventano più lunghi e il ricorso al riferimento del selettore corrente (`&`) più frequente. Ad un certo punto, il rischio di perder traccia e non capire più cosa sta succedendo è così elevato da non valerne la pena.

Per prevenire situazioni simili, è bene **evitare l'annidamento dei selettori il più possibile**. Tuttavia, ci sono ovviamente alcune eccezioni a questa regola.

### Eccezioni

Per cominciare, è permesso e anzi consigliabile annidare pseudo-classi e pseudo-elementi all'interno dei selettori iniziali.

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

Usare l'annidamento dei selettori per le pseudo-classi e gli pseudo-elementi non solo ha senso (perchè gestisce selettori fortemente relazionati), aiuta a mantenere le regole di un componente tutte nello stesso posto.

Inoltre, utilizzando classi agnostiche ai componenti come `.is-active`, è assolutamente giusto annidarle sotto il selettore del componente per mantenere il tutto ordinato.

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

Ultimo ma non per importanza, quando si stilizza un elemento sulla base del fatto che sia contenuto all'interno di un altro specifico elemento, è molto comodo usare l'annidamento per mantenere tutti gli stili relativi al singolo componente tutti nello stesso punto.

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

Lavorando con sviluppatori poco esperti, un selettore come `.no-opacity &` può sembrare un po strano. Per evitare confusione, puoi costruire un piccolo mixin che trasforma questa strana sintassi in una API esplicita.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Mixin per ottenere una semplice API per i selettori annidati
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
/// Mixin per ottenere una semplice API per i selettori annidati
/// @param {String} $selector - Selector
=when-inside($selector) {
  #{$selector} &
    @content
}
{% endhighlight %}
  </div>
</div>

Riscrivendo l'esempio precedente, il risultato sarebbe questo:

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

Come per ogni cosa, le specifiche sono al quanto irrilevanti, la consistenza è l'aspetto importante. Se ti senti pienamente confidente con l'annidamento dei selettori, allora utilizzalo. Assicurati solo che tutto il team sia concorde.






### Letture Aggiuntive

* [Beware of Selector Nesting](http://www.sitepoint.com/beware-selector-nesting-sass/)
* [The Inception Rule](http://thesassway.com/beginner/the-inception-rule)
* [Avoid nested selectors for more modular CSS](http://thesassway.com/intermediate/avoid-nested-selectors-for-more-modular-css)



