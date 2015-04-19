
# Cosa è Sass

Questo è il modo in cui [Sass](http://sass-lang.com) viene descritto nella sua [documentazione](http://sass-lang.com/documentation/file.SASS_REFERENCE.html):

> Sass è una estensione del CSS che aggiunge potenza ed eleganza al linguaggio di base.

L'obbiettivo finale di Sass è di correggere i difetti del linguaggio CSS. Il CSS, come tutti sappiamo, non è il linguaggio migliore del mondo <sup>[citazione necessaria]</sup>. Nonostante sia semplice da apprendere, può diventare disordinato molto velocemente, specialmente nei grandi progetti.

Ed è qui che entra in scena Sass, in qualità di meta-linguaggio, per migliorare la sintassi del CSS in modo da mettere a disposizione caratteristiche aggiuntive e strumenti utili. Contemporaneamente, Sass vuole essere conservativo rispetto al linguaggio CSS.

Il punto non è trasformare il CSS in un vero e proprio linguaggio di programmazione; Sass interviene solo dove il CSS fallisce. Per questo motivo, prendere la mano con Sass non è più difficile che apprendere il CSS: aggiunge semplicemente alcune funzionalità in più sopra di esso.

Detto questo, ci sono molti modi per usare queste nuove funzionalità. Alcuni buoni, alcuni sbagliati, alcuni insoliti. Queste linee guida sono pensate per darti un approccio consistente e documentato alla scrittura del codice Sass.

### Letture Aggiuntive

* [Sass](http://sass-lang.com)
* [Sass documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)






## Ruby Sass o LibSass

[Il primo committ su Sass](https://github.com/hcatlin/sass/commit/fa5048ba405619273e474a50400c7243fbff54fe) risale alla fine del 2006, più di 8 anni fa. Inutile dire che ha fatto molta strada da allora. Inizialmente sviluppato in Ruby, numerosi porting sono apparsi un po ovunque. Quello di maggior successo, [LibSass](https://github.com/sass/libsass) (scritto in C) è ora molto vicino ad essere del tutto compatibile con la versione Ruby.

Nel 2014, [i teams di Ruby Sass e LibSass hanno deciso di attendere l'allineamento delle due versioni prima di svuluppare nuove funzionalità](https://github.com/sass/libsass/wiki/The-LibSass-Compatibility-Plan). Da allora, LibSass rilascia attivamente delle versioni funzionalmente paritative a quelle del suo fratello maggiore. Le ultime inconsistenze rimaste sono raccolte e listate da me nel progetto [Sass-Compatibility](http://sass-compatibility.github.io). Se sei a conoscenza di una incompatibilità non elencata nel progetto, puoi aprire un issue per aggiungerla.

Torniamo alla scelta del compilatore. In realtà, tutto dipende dal tuo progetto. Se è un progetto Ruby on Rails, faresti meglio ad usare Ruby Sass, che è perfettamente idoneo per un caso come questo. Inoltre, sappi che Ruby Sass sarà sempre l'implementazione di riferimento che guiderà le funzionalità di LibSass.

Per i progetti non-Ruby che necessitano di una integrazione di workflow, LibSass è probabilmente la scelta migliore dato che è principalmente orientato ad essere incluso. Quindi se vuoi utilizzare per esempio NodeJS, [node-sass](https://github.com/sass/node-sass) è lo strumento giusto.



### Letture Aggiuntive

* [LibSass](https://github.com/sass/libsass)
* [Getting to know LibSass](http://webdesign.tutsplus.com/articles/getting-to-know-libsass--cms-23114)
* [Sass-Compatibility](http://sass-compatibility.github.io)
* [Switching from Ruby Sass to LibSass](http://www.sitepoint.com/switching-ruby-sass-libsass/)






## Sass o SCSS

C'è un sacco di confusione riguardo il significato del nome *Sass*, e ci sono buoni motivi: Sass identifica sia il preprocessore sia la sua sintassi. Non molto intuitivo, vero?

Il motivo è che Sass inizialmente descriveva una sintassi la cui caratteristica peculiare era la sensibilità all'indentazione. In breve tempo, i manutentori di Sass decisero di colmare il divario tra Sass e CSS mettendo a disposizione una sintassi simile al CSS chiamata *SCSS* che sta per *Sassy CSS*. Il motto è: se è CSS valido, è SCSS valido.

Da allora, Sass (il preprocessore) mette a disposizione due sintassi: Sass (non tutto maiuscolo, [per favore](http://sassnotsass.com)), conosciuta anche come *la sintassi predefinita*, e SCSS. La decisione su quale delle due utilizzare è soggettiva dato che entrambe sono strettamente equivalenti in termini di funzionalità. È solo una questione di estetica.

La sintassi sensibile agli spazi di Sass si basa sull'indentazione per fare a meno delle parentesi, dei punti e virgola ed altri simboli di punteggiatura, ottenendo una sintassi più breve e minimale. SCSS invece è più semplice da apprendere dato che aggiunge funzionalità sul normale CSS.

Personalmente preferisco SCSS rispetto a Sass perchè è più vicina al CSS e più semplice per molti sviluppatori. Per questo motivo, userò SCSS invece che Sass nel corso di questa guida.



### Letture Aggiuntive

* [What's the difference between Sass and SCSS](http://www.sitepoint.com/whats-difference-sass-scss/)






## Altri Preprocessori

Sass tra le altre cose è un preprocessore. Il suo concorrente più valido è senz'altro [LESS](http://lesscss.org/), un preprocessore basato su NodeJS che è diventato molto popolare grazie al famoso framework CSS [Bootstrap](http://getbootstrap.com/) che lo utilizza. C'è anche [Stylus](http://learnboost.github.io/stylus/) - che è più o meno la versione nerd senza restrizioni di LESS - dove si può fare quasi di tutto dato che quasi trasforma il CSS in un linguaggio di programmazione.

*Perchè scegliere Sass invece di LESS o un altro preprocessore?* è ancora tutt'oggi una domanda valida. Non molto tempo fa, si usava raccomandare Sass per i progetti basati su Ruby perchè era inizialmente sviluppato in Ruby e si sposava bene con Ruby on Rails. Ora che LibSass ha recuperato (largamente) il divario con la versione originale di Sass, non è più un consiglio rilevante.

Ciò che mi piace di Sass è il suo approccio conservativo al CSS. Il design di Sass si basa su forti princìpi: gran parte dell'approccio di design viene naturalmente dalla convinzione del team che a) aggiungere funzionalità extra ha un costo di complessità che deve essere giustificato dalla sua utilità e, b) dovrebbe essere semplice capire gli effetti di un determinato blocco di stili considerando il blocco da solo. Inoltre, Sass ha un'attenzione per i dettagli maggiore rispetto agli altri preprocessori. Per quanto posso dire, i designer principali hanno molto a cuore il supporto di ogni caso-limite della compatibilità CSS e dell'assicurarsi che ogni comportamento generico sia consistente.

In altre parole, Sass non è un preprocessore orientato a gratificare aspiranti programmatori nerd come me aggiungendo straordinarie funzionalità al di sopra del linguaggio che non prevedono il supporto di nessun caso d'uso logico. È un software mirato a risolvere problemi reali; mette a disposizione funzionalità utili per il CSS laddove il CSS viene meno.

Oltre ai preprocessori, dovremmo menzionare anche i postprocessori, che hanno ricevuto un'attenzione significativa negli ultimi mesi, grazie soprattutto a [PostCSS](https://github.com/postcss/postcss) e [cssnext](https://cssnext.github.io/). I postprocessori sono più o meno equivalenti ai preprocessori eccetto che non mettono a disposizione altro che la futura sintassi del CSS.

Puoi pensare ad un postprocessore come a un polyfill per funzionalità CSS non supportate. Per esempio, scriveresti le variabili come sono descritte nelle [specifiche CSS](http://dev.w3.org/csswg/css-variables/), poi compilando il foglio di stile con un postprocessore ciascuna occorrenza di variabile verrebbe rimpiazzata con il suo valore, come farebbe Sass.

L'idea a monte dei postprocessori è che quando i browser supporteranno le nuove funzionalità (e.g. le variabili CSS), il postprocessore non le compilerà più e lascerà che il browser gestisca il codice nuovo.

Mettere a disposizione oggi la sintassi di domani è un'idea nobile, tuttavia devo dire che preferisco comunque usare Sass per molte attività. Ad ogni modo ci sono delle occasioni in cui credo che i postprocessori siano più idonei rispetto a Sass e simili - CSS prefixing ad esempio - ma torneremo su questo punto più in là.



### Letture Aggiuntive

* [LESS](http://lesscss.org/)
* [Stylus](http://learnboost.github.io/stylus/)
* [cssnext](https://cssnext.github.io/)
* [PostCSS](https://github.com/postcss/postcss)
