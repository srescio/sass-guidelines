
# Commenti

Il CSS è un linguaggio complicato, pieno di hacks e stranezze. Per questo motivo dovrebbe essere pesantemente commentato, specialmente se tu o qualcun altro ha intenzione di leggere e aggiornare il codice a distanza di 6 mesi o un anno. Non permettere che tu o qualcun altro si ritrovi nella posizione di *Non-l'ho-scritto-io-oh-mio-dio-perché*.

Per quanto il CSS possa apparire semplice, c'è sempre spazio per dei commenti. Potrebbero spiegare:

* la struttura e/o il ruolo di un file;
* l'ovviettivo di un set di regole;
* l'idea che si cela dietro un numero magico;
* il motivo di una dichiarazione CSS;
* l'ordine delle dichiarazioni CSS;
* il ragionamento che ha portato a determinate scelte.

E probabilmente ho dimenticato molte altre ragioni. Commentare il codice richiede relativamente poco tempo quando è fatto immediatamente a valle della stesura del codice stesso, quindi fallo al momento giusto. Tornare su un pezzo di codice per commentarlo non solo è completamente irrealistico ma anche estremamente fastidioso.






## Scrivere i commenti

Idealmente, *ogni* gruppo di regole CSS dovrebbe essere preceduto da un commento in C-style spiegando il ruolo del blocco CSS. Tale commento dovrebbe ospitare delle spiegazioni numerate riguardo specifiche parti del gruppo di regole. Per esempio:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/**
 * Helper class to truncate and add ellipsis to a string too long for it to fit
 * on a single line.
 * 1. Prevent content from wrapping, forcing it on a single line.
 * 2. Add ellipsis at the end of the line.
 */
.ellipsis {
  white-space: nowrap; /* 1 */
  text-overflow: ellipsis; /* 2 */
  overflow: hidden;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/**
 * Helper class to truncate and add ellipsis to a string too long for it to fit
 * on a single line.
 * 1. Prevent content from wrapping, forcing it on a single line.
 * 2. Add ellipsis at the end of the line.
 */
.ellipsis
  white-space: nowrap /* 1 */
  text-overflow: ellipsis /* 2 */
  overflow: hidden
{% endhighlight %}
  </div>
</div>

Basilarmente tutto ciò che non sia chiaro a colpo d'occhio dovrebbe essere commentato. La documentazione non è mai troppa. Ricordati che non puoi *commentare troppo*, quindi sbizzarrisciti e scrivi commenti per tutto ciò che lo richiede.

Nel commentare sezioni specifiche di Sass, usa i commenti inline di Sass invece dei blocchi in C-style. Questo rende i commenti invisibili nell'output, anche nella modalità espansa in fase di sviluppo.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
// Add current module to the list of imported modules.
// `!global` flag is required so it actually updates the global variable.
$imported-modules: append($imported-modules, $module) !global;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
// Add current module to the list of imported modules.
// `!global` flag is required so it actually updates the global variable.
$imported-modules: append($imported-modules, $module) !global
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [CSS Guidelines’ Commenting section](http://cssguidelin.es/#commenting)






## Documentazione

Ogni variabile, funzione, mixin e segnaposto che sia inteso per essere riusato in tutta la codebase dovrebbe essere documentato come parte delle API globali usando [SassDoc](http://sassdoc.com).

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Vertical rhythm baseline used all over the code base.
/// @type Length
$vertical-rhythm-baseline: 1.5rem;
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Vertical rhythm baseline used all over the code base.
/// @type Length
$vertical-rhythm-baseline: 1.5rem
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>Three slashes (<code>/</code>) required.</p>
</div>

SassDoc ha due ruoli principali:

* forzare commenti standardizzati usando un sistema basato su annotazioni per tutto ciò che è parte di una API privata o pubblica;
* genera una versione HTML della documentazione delle API usando uno qualunque degli endpoint di SassDoc (CLI tool, Grunt, Gulp, Broccoli, Node...).

<figure role="group">
<img alt="Documentazione generata da SassDoc"
     sizes="100vw"
     srcset="/assets/images/sassdoc-preview_small.png  540w,
             /assets/images/sassdoc-preview_medium.png 900w,
             /assets/images/sassdoc-preview_large.png 1200w,
             /assets/images/sassdoc-preview_huge.png  1590w" />
<figcaption>Documentazione generata da SassDoc</figcaption>
</figure>

Ecco un esempio di mixin documentato estensivamente con SassDoc:

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/// Mixin helping defining both `width` and `height` simultaneously.
///
/// @author Hugo Giraudel
///
/// @access public
///
/// @param {Length} $width - Element’s `width`
/// @param {Length} $height ($width) - Element’s `height`
///
/// @example scss - Usage
///   .foo {
///     @include size(10em);
///   }
///
///   .bar {
///     @include size(100%, 10em);
///   }
///
/// @example css - CSS output
///   .foo {
///     width: 10em;
///     height: 10em;
///   }
///
///   .bar {
///     width: 100%;
///     height: 10em;
///   }
@mixin size($width, $height: $width) {
  width: $width;
  height: $height;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/// Mixin helping defining both `width` and `height` simultaneously.
///
/// @author Hugo Giraudel
///
/// @access public
///
/// @param {Length} $width - Element’s `width`
/// @param {Length} $height ($width) - Element’s `height`
///
/// @example scss - Usage
///   .foo
///     +size(10em)
///
///   .bar
///     +size(100%, 10em)
///
/// @example css - CSS output
///   .foo {
///     width: 10em;
///     height: 10em;
///   }
///
///   .bar {
///     width: 100%;
///     height: 10em;
///   }
=size($width, $height: $width)
  width: $width
  height: $height
{% endhighlight %}
  </div>
</div>



### Letture Aggiuntive

* [SassDoc](http://sassdoc.com)
* [SassDoc: a Documentation Tool for Sass](http://www.sitepoint.com/sassdoc-documentation-tool-sass/)
