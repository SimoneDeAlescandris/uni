# Indice

- [init](#init)
- [clone](#clone)
- [add](#add)
- [status](#status)
- [diff](#diff)
- [commit](#commit)
- [log](#log)
- [tag](#tag)
- [show](#show)
- [.gitignore](#.gitignore)
- [remote](#remote)
- [restore](#restore)
- [rm](#rm)
- [mv](#mv)
- [help](#help)

- [Per collegarsi ad un server remoto](#collegarsi-ad-un-server-remoto)
- [Bibliografia](#bibliografia)

<!-- Completare Indice -->

<img src="./img/6_git.png" alt="Logo Git" title="Logo Git" width="34px" style="float:left; margin-right:12px;">

# Introduzione

Un Sistema di Controllo Versione (**VCS**, _Version Control System_) registra nel tempo le modifiche apportate a un file o a un insieme di file, permettendo di ripristinare versioni precedenti in qualsiasi momento. Utilizzarne uno è fondamentale per mantenere la cronologia completa delle modifiche e garantire un recupero rapido in caso di errori.  
Tra questi, **Git**, creato da Linus Torvalds nel 2005, è ad oggi lo standard de facto. È un sistema di controllo versione <u>distribuito</u>, il che significa che ogni sviluppatore possiede una copia completa del progetto, comprensiva della sua cronologia. Questa caratteristica offre:  
- <u>Flessibilità</u>, perché ogni sviluppatore può lavorare indipendentemente;  
- <u>Sicurezza</u>, perché la perdita di un server centrale non compromette il progetto;  
- <u>Efficienza</u>, grazie alla gestione rapida di versioni e modifiche.  
  Git considera i propri dati più come una sequenza di istantanee (**snapshot**) in un mini filesystem. Ogni volta che si registra (commit) lo stato del progetto, Git fondamentalmente fa un’immagine di tutti i file in quel momento e per essere efficiente, se alcuni file non sono cambiati, non li risalva, ma crea semplicemente un collegamento al file già precedente salvato.  
La maggior parte delle operazioni in Git sono _in locale_, con pochissima latenza dovuta al fatto che l'intera storia del progetto (e tutto ciò che serve a farlo funzionare) è sul disco locale. Inoltre, l'_integrità_ dei progetti è garantita dal fatto che Git aggiunge solo dati e ogni azione è controllata da un checksum, con meccanismo di hash SHA-1, impedendo ogni possibilità di perdita o corruzione di file senza che Git non se ne accorga.  

## I Tre Stati  

In Git, i file possono trovarsi in tre stati principali:  
- ***modified*** (*modificati*): il file è stato modificato, ma non ancora committato nel database.  
- ***staged*** (_in stage_): il file, modificato nella versione corrente, è stato selezionato per essere incluso nel prossimo snapshot (commit).    
- ***committed*** (*committati*): il file è stato salvato in modo sicuro nel database locale di Git.

Questi stati si collegano a tre concetti fondamentali:  
- **Working Tree** (*albero di lavoro*): una copia di una versione specifica del progetto. I file vengono estratti dal database compresso di Git e resi disponibili sul disco locale per essere consultati o modificati.  
- **Staging Area** (*area di stage*): un file, situato generalmente nella directory di Git, che registra le informazioni sui cambiamenti destinati al prossimo commit. È anche chiamato **indice** (*index*). 
- **Git Directory** (*directory di Git*): luogo dove Git archivia i metadati e il database degli oggetti del progetto. È la parte più importante di Git ed è ciò che viene effettivamente copiato quando si clona un repository.  

> Il flusso di lavoro (***workflow***) è più o meno il seguente:  
> 1. Modifica i file nel tuo albero di lavoro.  
> 2. Aggiungi all'area di stage solo le modifiche che desideri includere nel prossimo commit.  
> 3. Committa, i file presenti nell'area di stage, creando un’istantanea (**_snapshot_**) permanente nella directory di Git.  

Se una particolare versione di un file è presente nella directory Git, è considerata **committata** (*committed*). Se il file è stato modificato e aggiunto all’area di stage, è **in stage** (*staged*). Se il file è stato modificato, da quando è stato estratto, ma non ancora aggiunto all’area di stage, è semplicemente **modificato** (*modified*).  

<img src="./img/7_areas.png" alt="Rappresentazione dei tre stati possibili in Git" title="Rappresentazione dei tre stati possibili in Git" width="50%" style="display:block; margin-left:auto; margin-right:auto;">

## Distinzione tra Git e GitHub

Prima di proseguire con la configurazione pratica di Git, è utile chiarire la differenza tra **Git** e **GitHub**.  
**Git** è uno strumento locale per il controllo di versione, che ti permette di gestire lo sviluppo di un progetto in modo distribuito.  
**GitHub** è una piattaforma web che offre servizi di hosting per repository Git, oltre a funzionalità aggiuntive come la collaborazione tra sviluppatori, la gestione delle modifiche tramite pull request e l’integrazione continua (CI/CD).

Git è indipendente da GitHub: puoi usare Git in locale senza mai utilizzare GitHub, ma non puoi utilizzare GitHub senza Git.

<!-- Parlare qui dei repository remoti? -->

## Configurazione Iniziale di Git

Passando alla pratica, l'unico posto che ci consente di poter sfruttare tutte il potenziale di Git è la riga di comando (“**<span style="color: skyblue;">Git</span> <span style="color: #FDDC5C;">Ba</span><span style="color: green;">sh</span>**”). Molte interfaccie grafiche implementano solo una parte delle funzionalità per semplificarne l’uso.  

Prima di iniziare ad usarlo, dobbiamo installarlo sul nostro device. Per farlo riferirsi al [sito ufficiale](https://git-scm.com/downloads). Su Android è possibile farlo utilizzando un emulatore del terminale Linux, come [Termux](https://play.google.com/store/apps/details?id=com.termux&hl=it).  

Successivamente dobbiamo inserire le nostre **credenziali** ed è conveniente utilizzare le stesse sia su Git (locale) che su GitHub (remoto) in modo che ogni interazione, come *push* o *pull*, avvengano senza problemi e ogni *commit* in locale sia correttamente associato al nostro repository remoto predefinito.  
```powershell  
git config --global user.name "IlTuoNomeUtente"
git config --global user.email "la.tua.email@example.com"
```  
Con l’opzione `--global`, la configurazione viene salvata per **tutti i repository Git** nel sistema. Se invece vuoi specificare un nome o un’email diversa solo per un repository specifico, puoi **omettere `--global`**.  

Puoi controllare tutte le configurazioni correnti (globali e locali) con:  
```powershell  
git config --list     # Elenco completo
git config user.name  # Singola voce specifica
```  

Puoi anche personalizzare altri aspetti, come l’**editor di testo predefinito** (usato ad esempio per scrivere messaggi di commit):  
```powershell  
git config --global core.editor "nano"
git config --global core.editor "code --wait"   # Per usare Visual Studio Code
``` 

Per abilitare la **colorazione automatica dell’output**, utile per distinguere meglio le informazioni nei comandi:  
```powershell  
git config --global color.ui auto
```  

Quando lavori con repository remoti su GitHub via HTTPS, potresti voler evitare di inserire le credenziali ad ogni operazione. In tal caso, puoi configurare un *credential helper* per salvare (o memorizzare temporaneamente) le tue credenziali.  
```powershell  
git config --global credential.helper cache        # Memorizza temporaneamente
git config --global credential.helper wincred      # Salva in modo permanente su Windows
git config --global credential.helper osxkeychain  # Salva in modo permanente su MacOS
```

# Elenco comandi utili:

> **PREMESSA**: Posizionarsi nella cartella dove lavorerai con Git, usando `cd`.

- **<span id="init" style="font-size: 16px;">`$ git init`</span>**: comando iniziale per avviare il monitoraggio di un progetto con Git. Deve essere eseguito nella directory del progetto e crea una nuova subdirectory denominata `.git`, contenente tutti i file necessari per il repository. Con questo solo comando preliminare non viene ancora tracciato alcun file.
  ```powershell
  git init
  ```

- **<span id="clone" style="font-size: 16px;">`$ git clone [url]`</span>**: ottieni una copia di un repository Git esistente, incluso lo storico dei commit, i rami, i tag, e la configurazione interna del progetto.
	```powershell
	git clone https://github.com/libgit2/libgit2
  git clone https://github.com/libgit2/libgit2 mylibgit   # Rinomina la cartella `libgit2` in `mylibgit`, con contenuto invariato
	```

- **<span id="add" style="font-size: 16px;">`$ git add`</span>**: è un comando multiuso, lo si usa per: iniziare a tracciare nuovi file; mettere in staging i file e per contrassegnare i file in conflitto di merge come risolti.
  ```powershell
  git add README.py   # Aggiunge un singolo file specificato all'area di stage
  git add .           # Aggiunge tutti i file nella directory corrente e nelle subdirectory
  git add *.txt       # Aggiunge tutti i file con estensione .txt (o qualche essa sia) nella directory corrente
  ```

- **<span id="status" style="font-size: 16px;">`$ git status`</span>**: mostra informazioni dettagliate sullo stato dei file nel repository e determina quali file sono modificati (_modified_), tracciati (_tracked_) o non tracciati (_untracked_).
  ```powershell
  git status
  git status -s       # Visualizzazione più sintetica
  git status --short  # Visualizzazione più sintetica (alternativa)
  ```
  Esempio di output:
	```powershell
	 M README						# M	 : file modificato, ma non ancora aggiunto all'area di stage
	M  lib/simplegit.rb		# file modificato ed è già in area di stage.
	MM Rakefile						# MM : file modificato, messo in stage e poi ulteriormente modificato.
	A  lib/git.rb					# A	 : file, nuovo, aggiunto all'area di stage
	?? LICENSE.txt				# ?? : file nuovo, non tracciato
	```

  <img src="./img/8_lifecycle.png" alt="Tutti i possibili stati di un file: Untracked; Unmodified; Modified; Staged." title="Tutti i possibili stati di un file" width="90%" style="display:block; margin-left:auto; margin-right:auto;">

- **<span id="diff" style="font-size: 16px;">`$ git diff`</span>**: se `$ git status` fosse un po’ troppo vago per i tuoi standard e tu volessi sapere esattamente cosa è cambiato, questo comando mostra le differenze, riga per riga, tra i file modificati e l’ultima versione tracciata (HEAD o staging area). Serve per vedere *cosa* cambierà prima di committare.  
  ```powershell  
  git diff            # mostra le modifiche non ancora aggiunte
  git diff --staged   # mostra le modifiche che hai già aggiunto con `git add` e che finiranno nel prossimo commit
  ```  
  
- **<span id="commit" style="font-size: 16px;">`git commit`</span>**: salva uno snapshot permanente dei file che si trovano *nell'area di stage* nel repository locale. Non registra automaticamente *tutti* i cambiamenti, ma solo quelli che sono stati aggiunti all'area di stage attraverso `git add`. Eventuali modifiche apportate dopo tale comando non saranno incluse nel commit finché non verranno registrate con `git add`.
  ```powershell
	git commit -m "Titolo: Ciao" -m "Descrizione: Messaggio descrittivo"
	git commit -a -m "Messaggio" 	# Aggiunge automaticamente tutti i file tracciati modificati e poi committa (equivalente a `git add` + `git commit`)
    - git commit --amend 			# Modifica l'ultimo commit, utile per correggere il messaggio o aggiungere altri file dimenticati.
	``` 
	L'opzione `-m`, non necessaria, permette di scrivere direttamente un messaggio di fianco ad ogni commit per avere un nostro report sulle informazioni che avevamo quando lo avevamo creato.

- **<span id="log" style="font-size: 16px;">`git log`</span>**: mostra la cronologia di tutti i commit effettuati, in ordine dal più recente al più vecchio, in modo da poter visionare quali modifiche sono state fatte, da chi, e con quale messaggio (oppure per recuperare l'ID di un commit). Essendo solo un comando di lettura, non modifica nulla ed è quindi sicuro eseguirlo tutte le volte che vogliamo.
	```powershell
  git log
	git log -n										# Mostra gli ultimi n commit.
	git log --oneline  								# Mostra ogni commit su una singola riga, molto più compatto.
  git log --graph --oneline 						# Aggiunge anche un piccolo grafico ad albero, utile per visualizzare i rami.
  git log -p 										# Mostra anche le modifiche effettive (diff) apportate da ogni commit.
  ```
  L'output è simile a:
		```powershell
		commit 3f9c1bfae3f2d7b123456789abcdef123456789			# È l'hash identificativo del commit, unico per ogni cambiamento.
		Author: Simone <simone@example.com>									# Chi ha fatto il commit.
		Date:   Sat Apr 6 10:00 2025 +0200									# Quando è stato fatto.

				Fix: corretto bug nel calcolo del fattoriale		# Descrizione data al commit.
		```

- **<span id="tag" style="font-size: 16px;">`git tag`</span>**: è un'etichetta che viene assegnata a un commit specifico per indicare un <u>commit è importante</u> ed è usato spesso per segnare versioni stabili (esempio: `v1.0`, `v2.1.5`, ecc.).  
  1. Usando semplicemente `git tag` andremo ad <u>elencare</u> tutti i tag, ordinati alfabeticamente. Non indica a quale commit puntano a meno che non si usi `git show`.
  2. Per <u>filtrare</u> i tag si usa `-l`. Ad esempio, `git tag -l 'v1.8.5*'` elencherà solo i tag che iniziano con `v1.8.5`.
  3. **Lightweight Tag** (tag leggero): un semplice riferimento, un puntatore, ad un commit. Non contiene informazioni extra come data, autore, messaggio. È praticamente come un **segnalibro**.
		```powershell
		git tag nome-tag
		```  
  4. **Annotated Tag** (tag annotato): questo tipo di tag viene salvato nel database Git come oggetto completo. È la <u>forma raccomandata</u> quando si rilasciano versioni ufficiali di un progetto perché conserva più informazioni.  
		```powershell
		git tag -a v1.4 -m 'my version 1.4'
		```
		Include:  
		- Nome del tagger;  
		- Email del tagger;  
		- Data e ora;  
		- Messaggio di tag;  
		- Possibilità di firma con <abbr title="GNU Privacy Guard">GPG</abbr>.  
	Quando si va a creare localmente un tag, Git lo memorizza solo nella nostra repository locale e per inviarlo ad server remoto dobbiamo eseguire, in ordine, i seguenti comandi:
	```
	git push origin master
	git push [tagname]
	```
	oppure se si ha necessità di inviare più tag assieme si può usare
	```
	git push origin master
	git push --tags
	```

- **<span id="show" style="font-size: 16px;">`git show`</span>**: mostra le informazioni salvate nel tag annotato e il commit a cui punta.  
  ```powershell
  git show v1.4
  ```

- **<span id=".gitignore" style="font-size: 16px;">`.gitignore`</span>**: file di testo usato per dire a Git quali file o cartelle non tracciare. Si crea nella root del repository.  
  ```powershell  
  echo "*.log" >> .gitignore
  echo "build/" >> .gitignore
  echo "*~" >> .gitignore
  git add .gitignore
  git commit -m "Aggiunto file .gitignore"
  ```
	Ogni riga rappresenta un pattern, ad esempio `*.log` ignora tutti i file `.log`, `build/` ignora tutta la cartella `build`. La terza riga dice a Git di ignorare tutti i file che terminano con una tilde (`~`), utilizzata da molti editor di testo, come Emacs, per contrassegnare i file temporanei.  
	Le regole per i patterns che puoi inserire nel file `.gitignore` sono le seguenti:  
  - Le righe vuote o le righe che iniziano con `#` vengono ignorate;
  - È possibile specificare una directory con una barra obliqua ( `/`);  
  - Puoi negare una riga iniziandola con un punto esclamativo ( `!`);  
  - I _modelli glob standard_ funzionano.  
  	Essi sono come espressioni regolari semplificate utilizzate dalle shell. Un asterisco ( `*`) corrisponde a zero o più caratteri; `[abc]`corrisponde a qualsiasi carattere all'interno delle parentesi (in questo caso a, b o c); un punto interrogativo ( `?`) corrisponde a un singolo carattere; e le parentesi che racchiudono caratteri separati da un trattino( `[0-9]`) corrispondono a qualsiasi carattere tra di loro (in questo caso da 0 a 9). Puoi anche utilizzare due asterischi per abbinare le directory nidificate; `a/**/z`corrisponderebbe a `a/z`, `a/b/z`, `a/b/c/z`, e così via.  
  Esempio pratico di un file `.gitignore`:
  ```powershell
  # no .a files
  *.a

  # but do track lib.a, even though you're ignoring .a file above
  !lib.a

  # only ignore the root TODO file, not subdir/TODO
  /TODO

  # ignore all files in the build/ directory
  build/

  # ignore doc/notes.txt, but not doc/server/arch.txt
  doc/*.txt

  # ignore all .txt files in the doc/ directory
  doc/**/*.txt
  ```
  GitHub mantiene un elenco abbastanza completo di buoni esempi di file `.gitignore` per dozzine di progetti e linguaggi su https://github.com/github/gitignore se vuoi un punto di partenza per il tuo progetto.
  
- **<span id="remote" style="font-size: 16px;">`$ git remote`</span>**: 
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->
  <!-- TODO -->

- **<span id="restore" style="font-size: 16px;">`$ git restore`</span>**: **ripristina** file nella working directory (*directory di lavoro*) o nell’area di staging, scartando modifiche indesiderate senza alterare la cronologia del repository (quindi senza creare commit).

  - `git restore <file>`: **annulla le modifiche locali** al file, ripristinandolo dalla versione nell’ultimo commit (HEAD)o dall'area di staging.  
  - `git restore --staged <file>`: rimuove il file dall'**area di staging**, riportandolo nello stato di "modificato ma non in stage". È utile se hai aggiunto un file con `git add` ma ti sei accorto di aver sbagliato.
  - `git restore --source <commit> <file>`: ripristina il file a una versione specifica indicata da un commit passato, senza influenzare altri file.
  - `git restore --worktree <file>`: ripristina il file solo nella working directory, mantenendo invariata la versione in stage.

  Senza opzioni aggiuntive, `git restore` opera sulla **working directory**. Con `--staged`, opera sull'**area di staging**; usando entrambe le opzioni contemporaneamente, puoi ripristinare file in entrambi i luoghi con un solo comando.
  Attenzione: `git restore` elimina le modifiche locali **senza chiedere conferma**, quindi è importante usarlo solo quando sei certo di voler scartare i cambiamenti.

- **<span id="rm" style="font-size: 16px;">`$ git rm`</span>**: rimuove file sia dalla working directory che dall’indice (staging area). Se vuoi solo smettere di tracciarlo ma lasciarlo sul disco, devi usare l’opzione `--cached`.  
  ```powershell
  git rm file.txt
  git commit -m "Rimosso file.txt"
  ```
  oppure per ignorarlo mantenendolo:
  ```powershell
  git rm --cached file.txt
  echo "file.txt" >> .gitignore
  git commit -m "Ignora file.txt"
  ```
	Per forzare la rimozione di un file si usa l'opzione `-f`. Questa è una funzionalità di sicurezza per impedire la rimozione accidentale di dati che non sono stati ancora registrati in uno snapshot e che non possono essere recuperati da Git.
	
- **<span id="mv" style="font-size: 16px;">`$ git mv`</span>**: comando che sposta o rinomina un file o una cartella e automaticamente aggiorna l’indice.  
  ```powershell
  git mv vecchio_nome.txt nuovo_nome.txt
  git commit -m "Rinominato file"
  ```
	È equivalente a fare manualmente `mv` e poi `git add` e `git rm`.  
	```powershell
  mv vecchio_nome.txt nuovo_nome.txt
	git rm vecchio_nome.txt
	git add nuovo_nome.txt
	git commit -m "Rinominato file"
  ```
  
- **<span id="help" style="font-size: 16px;">`help`</span>**: per accedere alla documentazione dettagliata di ogni comando ci sono tre metodi principali:  
  ```powershell  
  git help <comando>
  git <comando> --help
  man git-<comando>
  ```  

<!-- Nel libro ProGit sono arrivato a pagina 29 --> 
<!-- TODO -->

# Suggerimento opzionale (sviluppato)

Per dare fin da subito una **visione d’insieme**, potresti introdurre brevemente il concetto di *repository remoto*, spiegando che Git non lavora solo in locale: può sincronizzare i dati con server esterni, come **GitHub**, **GitLab** o **Bitbucket**.  
Questi remoti permettono di **collaborare** con altri, **eseguire backup** e **condividere codice** pubblicamente o privatamente.  
Puoi aggiungere, ad esempio:

> > **Nota:** in Git lavorerai spesso sia localmente (sul tuo computer) sia con un *repository remoto*, come su GitHub. È per questo che configurare correttamente le credenziali in locale facilita le operazioni di sincronizzazione, come `git push` e `git pull`.

<!-- 
Capire come cambiare l'url di git remote add origin perché ho cambiato nome alla repository su git... 
In generale rivedermi git remote.
-->

## Collegarsi ad un server remoto  

[Per collegarsi ad un server remoto](https://youtu.be/qj_q0idpeMQ?t=641&si=9j7vWgyLVRmaP7Nv) (come GitHub) dobbiamo usare il comando `$ git remote`.  

```powershell
% git remote add origin https://github.com/GiuIiopaesani/sitoweb
```

Per caricare poi tutti i file della nostra directory in una repository dobbiamo poi usare il comando

```powershell
$ git push origin master
$ git push -u
```

L’opzione `-u` ci permetterebbe di salvare quello che stiamo per inserire come default per la prossima volta che useremo il comando `$ git push`.

> L’ordine quindi sarebbe quello di eseguire il comando `add` per ogni nuovo file aggiunto, `status` per verificare la situazione e `commit` per salvare tutto, poi `push` e quindi le cose si troveranno sul nostro server remoto.
>

https://www.instagram.com/p/C_K4qfnI2Ga/?igsh=MW0ya3kyZnMwbGJsdA==

# Bibliografia

- [Learn Git Branching](https://learngitbranching.js.org/?locale=it_IT);
- [tesseslol, guida git](https://gist.github.com/tesseslol/da62aabec74c4fed889ea39c95efc6cc);
- [Pro Git - Scott Chacon, Ben Straub](https://git-scm.com/book/it/v2);
- [Edoardo Midali](https://www.youtube.com/watch?v=wPAE9-DdMtI);
- [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview);
- [Introduction to Git in VS Code](https://code.visualstudio.com/docs/sourcecontrol/intro-to-git);
- [Version control in VS Code](https://code.visualstudio.com/docs/introvideos/versioncontrol);
- [Working with GitHub in VS Code](https://code.visualstudio.com/docs/sourcecontrol/github);
- [git - la guida tascabile](https://rogerdudler.github.io/git-guide/index.it.html).