
# Introduzione





## Perché una styleguide

Una styleguide non è solo un documento piacevole da leggere, raffigurante uno stato ideale del proprio codice. È un documento cruciale nella vita di un progetto, che descrive come e perchè il codice dovrebbe essere scritto. Può sembrare eccessivo per dei progetti piccoli, ma aiuta molto nel mantenere una codebase pulita, scalabile e facilmente manutenibile.

Inutile dire che più sono gli sviluppatori coinvolti in un progetto, più sono necessarie delle linee guida sul codice. Allo stesso modo, più è grande il progetto, più importante diventano le linee guida.

[Harry Roberts](http://csswizardry.com) lo spiega con chiarezza nel suo progetto [CSS Guidelines](http://cssguidelin.es/#the-importance-of-a-styleguide):

<blockquote>
  <p>Una styleguide del codice (nota, non una styleguide sulla grafica) è uno strumento prezioso per i team che:</p>
  <ul>
    <li>creano e mantengono prodotti per un lasso di tempo ragionevolmente;</li>
    <li>hanno sviluppatori con diverse abilità e specializzazioni;</li>
    <li>hanno sviluppatori diversi che lavorano su uno stesso prodotto in determinati periodi;</li>
    <li>assumono regolarmente nuovo personale;</li>
    <li>hanno diverse codebases in cui gli sviluppatori si alternano a vicenda.</li>
  </ul>
</blockquote>






## Liberatoria

Prima di tutto: **questa non è una styleguide sul CSS**. Questo documento non tratterà di convenzioni per i nomi delle classi CSS, pattern modulari e la questione degli ID nel mondo del CSS. Queste linee guida sono mirate unicamente alla discussione di contenuti specifici di Sass.

Inoltre questa styleguide è di mia creazione e pertanto **molto opinionato**. Immaginalo come una collezione di metodologie e consigli che ho raccolto e raffinato nel corso degli anni. Mi da inoltre l'opportunità di linkare a delle risolrse molto utili, quindi assicurati di controllare le *letture aggiuntive*.

Ovviamente, questo non è certo l'unico modo per fare le cose, e potrebbe non adattarsi a tutti i progetti. Sentiti libero di adattarla alle tue necessità. Ogni progetto è un caso a se stante.






## Principi chiave

Il concetto che mi preme di trasmettere con tutta questa styleguide è che **Sass dovrebbe essere tenuto il più semplice possibile**.

Grazie a miei folli esperimenti come [operatori bitwise](https://github.com/HugoGiraudel/SassyBitwise), [iteratori e generatori](https://github.com/HugoGiraudel/SassyIteratorsGenerators) e [JSON parser](https://github.com/HugoGiraudel/SassyJSON) in Sass, siamo tutti ben consci di cosa si possa fare con questo preprocessore.

Il CSS è un linguaggio semplice. Sass, essendo pensato per scrivere CSS, non dovrebbe diventare più complesso del normale CSS. Il [principio KISS](http://en.wikipedia.org/wiki/KISS_principle) (Keep It Simple Stupid) è fondamentale qui e ha anzi precedenza rispetto al [principio DRY](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (Don't Repeat Yourself) in alcune circostanze.

Alcune volte è meglio avere delle ripetizioni per mantenere il codice manutenibile, piuttosto che costruire un sistema pesante, ingombrante, inutilmente complicato che risulta ingestibile a causa della sua complessità.

Inoltre, citando [Harry Roberts](https://csswizardry.com) ancora una volta, **il pragmatismo trionfa sul perfezionismo**. In certi momenti, ti troverai probabilmente ad andare contro le regole qui descritte. Se ha senso, se senti essere la cosa giusta, fallo. Il codice è solo un mezzo, non il fine.



### Letture Aggiuntive

* [KISS principle](http://en.wikipedia.org/wiki/KISS_principle)
* [DRY principle](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
* [Keep Sass Simple](http://www.sitepoint.com/keep-sass-simple/)
