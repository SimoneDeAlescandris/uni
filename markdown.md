# Indice

- [Introduzione](#introduzione)
- [Formattazione](#formattazione)
  - [*Italic*](#italic)
  - [**Bold**](#bold)
  - [~~Strikethrough~~](#strikethrough)
  - [<u>Underline</u>](#underline)
  - **<a href="#Header" style="font-size: 20px;">Header</a>**
  - [Apice e Pedice](#apice-pedice)
  - <a href="#commenti" style="color: green;">Commenti</a>
  - **<a href="#testo-colorato" style="color: blue;">Testo colorato</a>**
  - [Quote](#quote)
  - [List](#list)
  - [Paragraph](#paragraph)
  - [`Code`](#code)
  - [Link](#link)
  - [Footnotes](#footnotes)
  - [Image](#image)
  - <a href="#highlighter" style="background-color: lightgreen; color: black; padding: 2px; border-radius: 4px;">Highlighter</a>
  - [Allineamento del testo](#allineamento-del-testo)
  - [Abbreviazioni](#abbreviazioni)
  - [Callout](#callout)
  - [Front Matter](#front-matter)
  - [Embed di Video](#embed-di-video)
- [Bibliografia](#bibliografia)<br><br>

# **Introduzione**

Markdown è uno dei linguaggi di markup più utilizzati per aggiungere elementi formattati in documenti di testo, creato nel 2004 da John Gruber.  
A differenza degli editor [WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG), come Microsoft Word, Markdown è più versatile e viene utilizzato per scopi diversi, come la creazione di pagine web (Astro, Jamstack), documenti, note (Obsidian), libri, presentazioni, email e documenti tecnici; persino ChatGPT lo utilizza per formattare le sue risposte. 

L'estensione di questi tipi di file è ".md" o ".markdown".<br>
Markdown fornisce una sintassi più semplice rispetto all'HTML, pur venendo tradotto in HTML durante la visualizzazione. Nulla vieta di usare un mix fra i due linguaggi **SE** il render di Markdown supporta HTML.<br><br>

# **Formattazione**

- *<span id="italic">Italic</span>*: per rendere in corsivo una frase si circonda le sue parole con un underscore (`_`) o un asterisco. Es.: `_this_` o `*that*`.
- **<span id="bold">Bold</span>**: similmente il grassetto lo si ottiene circondando la parola con due asteristichi. Oppure usando due underscore, scelta meno comune. Es.: `**this**` o `__that__`.  
  Per avere sia Bold che Italic possiamo usare un triplo underscore, triplo asterisco oppure un mix fra asterischi e underscore. Es.: `___this___`, `***that***`, `_**these**_` o `**_those_**`.
- ~~<span id="Strikethrough">Strikethrough</span>~~: si usa il simbolo `~` (tilde), richiamabile su Windows tenendo premuto `ALT + 126`. Es.: `~~this~~`
- <span id="Underline"><u>Underline</u></span>: testo sottolineato non supportato nativamente, bisogna ricorrere al tag HTML `<u>`.
- **<span id="Header" style="font-size: 20px;">Header</span>**: nei titoli si antepone alla frase il cancelletto e, come in HTML, mettendone un numero che va da uno (`#`, equivalente a `<h1>`) a sei (`######`, equivalente a `<h6>`) si ottiene una diversa grandezza per il titolo. <br><br>

- **<span id="apice-pedice">Superscript e Subscript</span>** (Apice e Pedice): usati per formule matematiche, unità di misura e note a piè di pagina. Non sono supportati in Markdown puro o GitHub. Es.:
  ```md
  x^2^ <!-- Apice -->
  H~2~O <!-- Pedice -->
  ```
  Versione HTML:  
  ```html
  x<sup>2</sup> <!-- Apice -->
  H<sub>2</sub>O <!-- Pedice -->
  Loro alternativa è usare **MathJax/KaTeX** nei documenti che supportano LaTeX:  
  ```md
  $$ x^2 $$  
  $$ H_2O $$
  ```
- <span id="commenti" style="color: green;">Commenti</span>: non supportati, possibili solo attraverso la sintassi HTML. Es.: `<!-- Commento -->`. <!-- Questo è un segreto! -->
- **<span id="testo-colorato" style="color: blue;">Testo colorato</span>**: solo se si usa HTML e CSS. Es.: `<span style="color: blue;">this</span>`
- **<span id="quote">Quote</span>**: anteponi alla citazione il simbolo "greater than" (`>`). Se essa si estende su più paragrafi possiamo usare lo stesso simbolo in ogni riga per mantenere la formattazione.
    ```
    > There are 10 types of people in this world:
    > Those who understand binary and those who don't.
    ```
    Attraverso poi `> >` possiamo creare una quote all'interno di una quote
    ```
    > Memento Mori.
    > > “La novità è che non c’è più tempo”.
    ```
- **<span id="list">List</span>**, ne esistono di diversi tipi:
  1. *unordered*, con i "bullet point";
  2. *ordered*, con i numeri";
  3. *To-do list*.
      ```md
      - [x] ~~Finire Blabbo;~~
      - [x] Chiamare assicurazione;
      - [ ] Fare da mangiare;
      - [ ] Studiare Markdown.
      Lista della spesa:
      - Pane;
      * Latte;
      1. Frutta:
        1. Mele;
        2. Pere;
        3. Banane.
      2. Formaggio;
      - Verdure:
        - Spinaci;
        * Broccoli.
      ```
  4. **Definition List** (Liste di definizione): permettono di creare liste con termini e relative definizioni; utili in glossari, FAQ e documentazione tecnica. Non supportate in Markdown puro. Es.:  
      ```md
      Termine 1  
      : Definizione 1  

      Termine 2  
      : Definizione 2  
      ```
      Versione HTML:  
      ```html
      <dl>
        <dt>Termine 1</dt>
        <dd>Definizione 1</dd>
        <dt>Termine 2</dt>
        <dd>Definizione 2</dd>
      </dl>
      ```
    5.  **Toggle List (Collapsible Sections):** non supportate nativamente. Tuttavia, alcuni sistemi permettono di farlo con HTML:  
        ```html
        <details>
          <summary>Testo visibile (cliccabile)</summary>
          Qui il testo che appare quando si clicca.
        </details>
        ```  
- **<span id="paragraph">Paragraph</span>**: normalmente, i paragrafi sono di tipo "sigle straight line". Ovvero, scrivendo quanto segue
  > Do I contradict myself?
  > Very well then I contradict myself,
  > (I am large, I contain multitudes.)
  
  ci aspetteremmo che venga mantenuta la separazione fra i paragrafi; purtroppo non accadrà e avremo
  > Do I contradict myself? Very well then I contradict myself, (I am large, I contain multitudes.)  
  
  Dunque se volessimo forzare una nuova linea dovremo per forza rompere l'unione fra i paragrafi
  > Do I contradict myself?
  >
  > Very well then I contradict myself,
  >
  > (I am large, I contain multitudes.)  
  
  Questo è ciò che viene detto *hard line break*; per avere un *soft line break* dobbiamo aggiungere due spazi alla fine di ogni riga, oppure usare il tag HTML `<br>` alla fine della linea.
  > Do I contradict myself?  
  Very well then I contradict myself,  
  (I am large, I contain multitudes.)
- **<span id="code">Code</span>**: utilizzando il carattere `` ` `` (backtick, accento grave inclinato), richiamabile su Windows tenendo premuto `ALT + 96`, si possono scrivere blocchi di codice in due modi possibili:
  - inline code, `` `**this**` ``;
  - block of code. Scrivendo poi nei tre backtrick iniziali il linguaggio utilizzato, questo verrà riconosciuto da Markdown:
    ````markdown
    ```python
    def somma(a, b):
        return a + b

    numero1 = 5
    numero2 = 10
    print(f"La somma di {numero1} e {numero2} è: {somma(numero1, numero2)}")
    ```
    ````  
    Inoltre, nel caso di blocchi di codice che iniziano con tre backtrick (`` ``` ``), GitHub aggiunge in automatico il tasto "copia"; per fare lo stesso in un sito web possiamo usare HTML e JavaScript, mentre in un progetto Next.js o Astro possiamo usare librerie come Shiki.
- **[Link](about:blank "Esempio")**<span id="link">,</span> ve ne sono tre tipi:
  1. _inline link_. 
    Es.: ``[Title](URL "title")`` o raramente `<URL>` (usato principalmente per le email <nomeutente@provider.dominio>);
  2. _reference link_, è modo per riferirsi allo stesso link più volte senza doverlo ripetere ogni volta. Es.:  
      ```markdown
      Questo è un link di esempio: [Testo][id-ref].

      [id-ref]: about:blank "Titolo opzionale"
      ```
  3. *Heading ID*: identificatori unici che servono per creare **ancoraggi (anchor links)**, ovvero collegamenti per saltare direttamente a un determinato punto in una pagina. 
    Vengono solitamente usati documenti tecnici o wiki come **Indice dei contenuti (Table of Contents - TOC)**, per facilitare la navigazione interna.
    Sintassi: `{#id-personalizzato-univoco}`. Es.:
      ```md
      ## Indice
      [Vai alla sezione importante](#sezione-importante)
      ---
      ## Sezione Importante {#sezione-importante}
      ```
      In HTML avremmo scritto: `<h2 id="sezione-importante">Sezione Importante</h2>`.  
      È anche possibile **omettere l'ID** in alcuni casi perché GitHub, vscode e molti altri tool assegnano ID automaticamente basandosi sul titolo, linkabile usando come ID il nome del titolo. Alcune regole da tenere a mente infine sono che: 
      - in presenza di spazi, questi verranno convertiti in `-`;  
      - i caratteri speciali (es.: `è, à, !`) vengono rimossi o sostituiti.  
      - Sono *case-insensitive*, quindi `#Titolo` e `#titolo` sono uguali.  
- **<span id="footnotes">Footnotes</span>** ("note a piè di pagina"): utili per aggiungere riferimenti o spiegazioni senza interrompere il flusso del testo. Attenzione: non sono supportate da tutti gli editor Markdown, infatti GitHub non le gestisce nativamente. Un esempio ne chiarirà la sintassi:  
    ```markdown
    Questo è un esempio di footnote[^1].
    
    [^1]: Qui il testo della nota a piè di pagina.
    ```
    Possiamo usare anche `[^md]` per inserire più note senza doverci preoccupare di numerarle manualmente.
- **<span id="image">Image</span>**, la sintassi è quasi la stessa dei link.  
  Es.: ``![Testo alternativo](URL "title")``.  
  Equiv. in HTML: `<img src="URL" alt="Testo alternativo" title="title">`.  
  Il titolo di un'immagine o link, non obbligatorio, è ciò che compare se lasciamo il mouse sull'immagine per qualche secondo. Per <abbr title="dimensione, posizione, effetti hover, filtri visivi, bordi o margini">modificare un'immagine</abbr> dobbiamo usare HTML o CSS e un editor che supporti quindi anche questi due linguaggi.  
  <img src="./img/5_AOT.JPG" alt="meme in stile AOT con Fidaleo vs Brenti" width=35% style="position:relative;" title="Fidaleo vs Brenti">
- **DIVISORI**: si fanno con tre trattini o underscore. Es. `---` o `___`.
- **TABELLE**: supportate, ma tediose da scrivere. Di defualt il testo è allineato a sinistra.  Es.:
  ```markdown
  | Colonna 1 | Colonna 2 | Colonna 3 |
  |:----------|:---:|-:|
  | Valore 1  | Valore 2  | Valore 3  |
  | Valore 4  | Valore 5  | Valore 6  |
  ```
- **<span** id="highlighter" style="background-color: lightgreen; color: black; padding: 2px; border-radius: 4px;">Highlighter</span**
  Markdown standard non supporta evidenziazione del testo e ancora una volta dobbiamo usare HTML con sintassi `<mark>this</mark>`; alcuni editor estesi (come Obsidian o Notion) permettono l’uso di `==testo evidenziato==`.
  Per cambiare il colore si usa invece CSS, con il tag `background-color`. Consiglio è quello di usare il seguente script se è consentito il CSS:
  ```markdown
  <style>
    .evidenziato {
      background-color: lightgreen;
      color: black;
      padding: 2px;
      border-radius: 4px;
    }
  </style>

  <span class="evidenziato">Testo con colore personalizzato</span>
  ```
- **<span id="allineamento-del-testo">Allineamento del testo (destra, sinistra, giustificato)</span>**: Markdown puro non lo supporta. Tuttavia, puoi farlo con HTML:
     ```html
     <p style="text-align: left;">Testo allineato a sinistra (default)</p>
     <p style="text-align: center;">Testo allineato al centro</p>
     <p style="text-align: right;">Testo allineato a destra</p>
     <p style="text-align: justify;">Testo giustificato su tutta la riga</p>
     ```  
- **<span id="abbreviazioni">Abbreviazioni</span>**: non supportate nativamente, ma si può usare HTML: `<abbr title="Uniform Resource Locator">URL</abbr>`.  
  Alcuni editor avanzati permettono di definirle con  
  ```markdown
  *[HTML]: HyperText Markup Language
  ```  
  Poi, ovunque si scriverà HTML, verrà mostrato il tooltip "HyperText Markup Language" al passaggio del mouse. <br><br>

- **<span id="callout">Callout</span>**: blocchi evidenziati usati per attirare l’attenzione su una nota importante. Non sono parte di Markdown standard, ma possiamo impelmentarli attraverso HTML e CSS oppure in editor avanzati come Obsiadian attraverso la sintassi:
  ```
  > [!NOTE] Questo è un callout
  > Puoi usarlo per evidenziare informazioni importanti.
  ```
- **<span id="front-matter">Front Matter</span>**: è un blocco di **metadati** scritto in *YAML* che viene usato nei blog statici come Jekyll, Hugo, Docusaurus e Astro per definire informazioni come titolo, autore, data, tag, layout, categorie. Non è visibile nel Markdown normale. Es:  
     ```yaml
     ---
     title: "markdown"
     author: "Simone"
     date: "2025-04-04"
     tags: ["Markdown", "Guida", "Tutorial"]
     layout: "post"
     categories: ["Tutorial"]
     ---
     ```
- **<span id="embed-video">Embed di Video</span>**: Markdown puro non lo integra. Tuttavia, si dovrebbe poter usare HTML con `<iframe>` o in alcuni editor, come Obsidian, `![](https://www.youtube.com/watch?v=dQw4w9WgXcQ)`. Tuttavia non sono riuscito a farlo funzionare.

<details>
<summary>Quasi ogni tipo di testo formattato può essere integrato con gli altri tipi.</summary>

> | [***`Esempio`***](about:blank "Lautaro Martinez") | Colonna 2 |
> |:--------------------------------------------------|----------:|
> |  Valore 1                                         | Valore 2  |
</details><br><br>

# Bibliografia:

- [Edoardo Midali](https://youtu.be/jz0WfxLXth8?si=ACuzopn3DP8t9ilb);
- [Markdown Guide](https://www.markdownguide.org/getting-started/);
- [Markdown Tutorial](https://www.markdowntutorial.com/).