
# Convenzioni sui nomi

In questa sezione, we will not deal with the best CSS naming conventions for maintainability and scale; not only is that up to you, it’s also out of the scope of a Sass styleguide. I suggest those recommended by [CSS Guidelines](http://cssguidelin.es/#naming-conventions).

Ci sono alcuni elementi a cui è possibile attribuire un nome in Sass, ed è importante scegliere bene in modo che l'intera code base sia consistente e facile da leggere:

* variabili;
* funzioni;
* mixin.

I segnaposti di Sass sono deliberatamente omessi in questa lista dato che possono essere considerati dei regolari selettori CSS, quindi seguendo la steassa tipologia di nomi delle classi.

Riguardo alle variabili, funzioni e mixin, ci atteniamo a qualcosa di simile al CSS: **minuscolo separato da trattini**, e soprattutto significativo.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$vertical-rhythm-baseline: 1.5rem;

@mixin size($width, $height: $width) {
  // ...
}

@function opposite-direction($direction) {
  // ...
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$vertical-rhythm-baseline: 1.5rem

=size($width, $height: $width)
  // ...

@function opposite-direction($direction)
  // ...
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [CSS Guidelines’ Naming Conventions](http://cssguidelin.es/#naming-conventions)






## Costanti

Se sei lo sviluppatore di un framework o di una libreria, potresti imbatterti in variabili che non devono essere modificate in nessuna circostanza: le costanti. Sfortunatamente (o fotunatamente?), Sass non dispone di alcun modo per definire tali entità, quindi dobbiamo aderire a delle precise convenzioni di nomenclatura per chiarificare il ruolo di ogni variabile.

Come per molti altri linguaggi, suggerisco il maiuscoletto con underscore di separazione per le variabili quando hanno il ruolo di costanti. Non solo si tratta di una convenzione molto comune, contrasta inoltre molto bene rispetto alle comuni variabili scritte in minuscolo separate da trattini.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Giusto
$CSS_POSITIONS: (top, right, bottom, left, center);

// Sbagliato
$css-positions: (top, right, bottom, left, center);
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Giusto
$CSS_POSITIONS: (top, right, bottom, left, center)

// Sbagliato
$css-positions: (top, right, bottom, left, center)
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [Dealing With Constants in Sass](http://www.sitepoint.com/dealing-constants-sass/)






## Namespace

Se vuoi distribuire il tuo codice Sass, come nel caso di una libreria o un framework, un layout a griglia o altro, può essere opportuno attribuire un namespace a tutte le variabili, funzioni, mixin e segnaposto così da non andare in conflitto con codice altrui.

Per esempio, se stai lavorando ad un progetto *Sassy Unicorn* che debba essere usato dagli sviluppatori di tutto il mondo (chi non lo vorrebbe?), potresti usare `su-` come namespace. È abbastanza specifico da evitare collisioni sui nomi e corto abbastanza da non essere fastidioso da scrivere.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
$su-configuration: ( ... );

@function su-rainbow($unicorn) {
  // ...
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
$su-configuration: ( ... )

@function su-rainbow($unicorn)
  // ...
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>Da notare che il namespacing automatico è uno degli obbiettivi di design della futura rivisitazione di <code>@import</code> in Sass 4.0. Dato che si avvicina la sua disponibilità, verrà meno la necessità di aggiungere i namespace manualmente; in futuro, le librerie con namespace manuali potrebbero diventare più difficili da usare.</p>
</div>

### Letture Aggiuntive

* [Please Respect the Global CSS Namespace](http://blog.kaelig.fr/post/44554267597/please-respect-the-global-css-namespace)
