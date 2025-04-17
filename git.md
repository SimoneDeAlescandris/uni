# Indice

- [Introduzione](#introduzione)
  - [I Tre Stati](#i-tre-stati)
  - [Distinzione tra Git e GitHub](#distinzione-tra-git-e-github)
  - [Configurazione Iniziale di Git](#configurazione-iniziale-di-git)
- [Elenco comandi utili](#elenco-comandi-utili)
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
  - [checkout](#checkout)
  - [restore](#restore)
  - [rm](#rm)
  - [mv](#mv)
  - [help](#help)
- [Connect to a `remote` server](#connect-to-a-remote-server)
- [Riassunto](#riassunto)
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

# Elenco comandi utili

> **PREMESSA**: Posizionarsi nella cartella dove lavorerai con Git, usando `cd`.

- **<span id="init" style="font-size: 16px;">`$ git init`</span>**: comando iniziale per avviare il monitoraggio di un progetto con Git. Deve essere eseguito nella directory del progetto e crea una nuova subdirectory denominata `.git`, contenente tutti i file necessari per il repository. Con questo solo comando preliminare non viene ancora tracciato alcun file.
  ```powershell
  git init
  ```

- **<span id="clone" style="font-size: 16px;">`$ git clone <url>`</span>**: ottieni una copia di un repository Git esistente, incluso lo storico dei commit, i rami, i tag, e la configurazione interna del progetto.
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
  ```
  ```powershell
  git commit -m "Initial commit"
  git add forgotten_file.txt
  git commit --amend 			# Modifica l'ultimo commit, utile per correggere il messaggio o aggiungere altri file dimenticati.
	``` 
	L'opzione `-m`, non necessaria, permette di scrivere direttamente un messaggio di fianco ad ogni commit per avere un nostro report sulle informazioni che avevamo quando lo avevamo creato.

- **<span id="log" style="font-size: 16px;">`git log`</span>**: mostra la cronologia di tutti i commit effettuati, in ordine dal più recente al più vecchio, con dettagli su autore, data, messaggio ed ID del commit. È un comando di solo lettura. Avendo MOLTE opzioni meglio vedere le altre sulla pagina man.  
	```powershell  
  git log
	git log -n										# Mostra gli ultimi n commit.
	git log --oneline  								# Mostra ogni commit su una singola riga, molto più compatto.
  git log --graph --oneline 						# Aggiunge anche un piccolo grafico ad albero, utile per visualizzare i rami.
  git log -p 										# Mostra le modifiche effettive (diff) apportate da ogni commit.
  git log --stat                                  # Fornisce una serie di informazioni: un elenco dei file modificati; quante linee in quei file sono state aggiunge e rimosse; un riassunto delle informazioni.
  git log --shortstat                                  # Come prima, ma con solo il riassunto delle informazioni.
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
	git push <tagname>
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

- **<span id="checkout" style="font-size: 16px;">`$ git checkout -- <file>`</span>**: **sostituisce** `<file>` con la sua versione del commit precedente. Serve ad annullare le modifiche fatte rispetto all'ultimo commit. **Attenzione**: sostituisce, non modifica. Usalo solo se ne sei davvero convinto perché poi non si può più tornare indietro.
  ```powershell
  git status
  git checkout -- CONTRIBUTING.md
  git status
  ```
  Se hai bisogno di entrambe le versioni del file, puoi aprire una nuova ramificazione (**Branch**).
  <!-- RICORDARMI DI METTERE ANCHE QUI IL LINK DI QUANDO PARLERÒ del BRANCH. -->

- **<span id="restore" style="font-size: 14px;">`$ git restore`</span>**: **ripristina** file nella working directory (*directory di lavoro*) o nell’area di staging, scartando modifiche indesiderate senza alterare la cronologia del repository (quindi senza creare commit).

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

# Connect to a `remote` server  

Come [accennato prima](#distinzione-tra-git-e-github), per collaborare a qualsiasi progetto necessitiamo di piattaforme di hosting dei repository, come GitHub. I **repository remoti** sono quindi versioni del progetto ospitate da queste piattafome.  

Per vedere quali server remoti hai configurato, puoi eseguire il comando **`git remote`**, che elenca i nomi abbreviati (_shortname_) di ogni _handle_ (riferimento) remoto specificato. Se hai clonato il tuo repository, attraverso [`git clone`](#clone), dovresti almeno vedere `origin`, ovvero il nome predefinito che Git assegna al server da cui hai clonato, che punta all’URL da cui è stato clonato il progetto. Questo collegamento può essere visualizzato con `git remote -v`, che mostra per ogni shortname l’URL usato sia per il fetch che per il push: 
```powershell 
git remote -v
origin  https://github.com/utente/vecchio-nome-repo.git (fetch)
origin  https://github.com/utente/vecchio-nome-repo.git (push)
``` 

Se successivamente su GitHub rinomini la repository, Git locale **non sa nulla di questo cambiamento**, quindi continuerà a usare l’URL originario finché non lo aggiornerai manualmente (andando a sovrascrive l’URL associato al remote `origin`):  
```powershell 
git remote set-url origin https://github.com/utente/nuovo-nome-repo.git
```  

Se invece vuoi cambiare il nome dello shortname, per esempio da `origin` a `uni`, puoi usare il seguente comando e da questo momento in poi, i `push` e i `pull` andranno specificati con il nuovo nome:
```powershell
git remote rename origin uni
git remote -v
uni  https://github.com/utente/nuovo-nome-repo.git (fetch)
uni  https://github.com/utente/nuovo-nome-repo.git (push)
git push uni master
``` 

Puoi anche aggiungere più remoti contemporaneamente (ad esempio, `uni` e `backup`) e potrai scegliere a quale pushare o da quale tirare i dati. Git non impedisce di avere più remoti; al contrario, è una pratica comune in ambienti distribuiti o quando si vuole avere una copia di backup da qualche altra parte: 
```powershell 
git remote add backup https://gitlab.com/simone/copia.git
``` 

Nei remoti si possono eseguire comandi come:  
...

---
---

`git push`, `git pull`, `git fetch`, indirizzando automaticamente l’origine o la destinazione dei dati verso/da un determinato server remoto.

`git remote`: gestisce i collegamenti ai repository remoti.
```powershell
git remote -v                         # Elenca gli URL associati ai remoti (fetch e push)
git remote add <nome> <url>           # Aggiunge un nuovo remoto
git remote rename <vecchio> <nuovo>   # Rinomina un remoto
git remote remove <nome>              # Rimuove il collegamento a un remoto
```

`git push`: invia i commit dal repository locale a quello remoto.
```powershell
git push                            # Invia le modifiche al branch remoto tracciato
git push origin <nome-branch>       # Invia uno specifico branch a uno specifico remoto
git push -u origin <nome-branch>    # Imposta il branch remoto come tracciato (upstream)
git push --tags                     # Invia tutti i tag locali al repository remoto
git push origin :nome-branch        # Elimina un branch remoto
```

`git pull`: scarica e unisce in un colpo solo le modifiche dal remoto nel branch corrente.
```powershell
git pull                        # Equivalente a `git fetch` seguito da `git merge`
git pull --rebase               # Esegue `git fetch` seguito da `git rebase` anziché `merge`
git pull origin <nome-branch>   # Preleva e unisce un branch remoto specifico
```

`git fetch`: scarica gli oggetti dal remoto ma **NON** li unisce nel branch attuale.
```powershell
git fetch                       # Scarica tutti i branch remoti e gli aggiornamenti
git fetch origin                # Scarica solo dal remoto `origin`
git fetch origin nome-branch    # Scarica un branch specifico
git fetch --all                 # Scarica da tutti i remoti configurati
```

`git merge`: unisce un branch (o commit) nel branch corrente.
```powershell
git merge <branch>            # Unisce il branch indicato nel branch attuale
git merge --no-ff             # Forza la creazione di un commit di merge anche se è possibile un fast-forward
git merge --abort             # Annulla un merge in corso in caso di conflitti
git merge --squash <branch>   # Combina tutte le modifiche in un unico commit (non automatico)
```

`git clone`: crea una copia completa di un repository remoto, compreso il database Git e la configurazione del remoto.
```powershell
git clone <url>                 # Clona il repository nella directory corrente
git clone <url> nome-cartella   # Clona il repository in una cartella specifica
git clone --depth 1 <url>       # Clona solo l’ultimo commit (clone “superficiale”, utile per risparmiare spazio)
git clone --branch <nome>       # Clona un branch specifico
```

Il comando `git rebase` serve per **spostare la base di un branch** su un altro, riscrivendo la cronologia dei commit. In pratica, applica una serie di commit **sopra** un nuovo punto della storia, invece di fonderli come fa `merge`. Questo è utile per **mantenere una cronologia lineare e più leggibile**, evitando i commit di merge visibili nell'albero.

Quando fai `rebase`, Git prende i commit che hai fatto nel tuo branch e li "rigioca" come se li stessi facendo **dopo** un altro punto della storia. È spesso usato prima di eseguire un `merge`, per "pulire" la cronologia.

Esempio concreto: supponiamo che tu stia lavorando nel branch `feature`, ma nel frattempo qualcuno ha aggiornato `master`. Se fai `merge`, otterrai un commit extra che indica il merge. Se fai `rebase`, i tuoi commit verranno spostati sopra `master` e sembrerà che tu abbia lavorato su una base aggiornata fin dall’inizio.

```powershell
git rebase master                           # Sposta i commit del branch attuale sopra l'ultimo commit di master
git rebase -i HEAD~3                        # Apre un'interfaccia interattiva per modificare, unire, riordinare gli ultimi 3 commit
git rebase origin/main                      # Rigioca i tuoi commit sopra l’ultimo stato remoto di main
git pull --rebase                           # Fa pull ma invece di merge applica rebase, per una cronologia più pulita
git rebase --onto main featureA featureB    # Applica i commit di featureB (che derivano da featureA) su main, escludendo featureA
git rebase --continue                       # Dopo aver risolto un conflitto, continua il rebase
git rebase --abort                          # Annulla completamente il rebase e torna allo stato prima del comando
git rebase --skip                           # Salta un commit che ha causato conflitti durante il rebase
```

Le opzioni più usate sono `-i` per fare pulizia dei commit locali (modificare messaggi, unirli, ecc.), `--continue` per proseguire dopo un conflitto, e `--abort` per tornare indietro in caso di errori. `--onto` è più avanzata ma potente per cambiare completamente la base di uno o più commit.

Il rebase è molto utile **prima di fare push**, ma non va usato su branch già condivisi con altri, perché **riscrive la cronologia** e può creare conflitti nei repository remoti. Vuoi che ti faccia uno schema visivo del rebase rispetto al merge per il tuo documento?

---

***`git remote add origin <URL>` e `git clone <URL>` sono la stessa cosa?* No**

- `git clone <URL>` fa **più cose insieme**:
  - inizializza un repository locale (`git init`)
  - configura il remoto come `origin`
  - scarica tutti i file, la cronologia, i branch, ecc.
  - effettua automaticamente il primo checkout nel branch principale

- `git remote add origin <URL>` invece:
  - **aggiunge solo un riferimento al remoto** nel tuo repository locale esistente
  - non scarica nulla, non inizializza nulla, non fa alcun fetch o checkout

Quindi se parti da **zero**, devi usare `git clone`.  
`git remote add origin` lo usi **dopo** un `git init`, ad esempio se stai iniziando un progetto nuovo da locale e poi vuoi connetterlo a GitHub.

Esempio pratico:
```powershell
mkdir nuovo-progetto
cd nuovo-progetto
git init
git remote add origin https://github.com/simone/nuovo-progetto.git
```
Questa sequenza non scarica niente, ma ti permette poi di fare il primo push.

---

<!-- Nel libro ProGit sono arrivato a pagina 42 -->  

---

Per associare il tuo repository locale a un repository remoto, si usa:

```bash
git remote add origin https://github.com/utente/nome-repo.git
```

In questo caso `origin` è un nome convenzionale usato per indicare l’URL remoto predefinito. Puoi avere più remoti, ciascuno con un nome diverso (es. `origin`, `upstream`, ecc.).

Una volta configurato il collegamento, puoi:
- **inviare le modifiche locali** al server remoto con:
  ```bash
  git push origin master
  ```

- **recuperare modifiche da altri sviluppatori** con:
  ```bash
  git pull origin master
  ```

Oppure semplicemente usare:
```bash
git clone https://github.com/utente/nome-repo.git
```
che scarica tutto il repository remoto (con la cronologia completa) e imposta già `origin` come remoto predefinito.

Perché è utile sapere tutto questo già durante la configurazione iniziale?  
Perché **le credenziali che imposti in locale** (tramite `git config`) verranno usate per firmare i tuoi commit, e per **autenticarti** quando interagirai con i remoti. Se non sono corrette o coerenti con quelle usate su GitHub, potresti incontrare errori durante il `push`.

Ad esempio:
```bash
git config --global user.name "Simone"
git config --global user.email "simone@example.com"
```

Se il tuo account GitHub è registrato con un’altra email, GitHub potrebbe non associare correttamente i tuoi commit al tuo profilo. Per evitare problemi, è buona norma usare le **stesse credenziali in locale e sul remoto**.

> ✅ Suggerimento: dopo aver fatto `git push`, visita il tuo repository su GitHub e controlla che il commit risulti attribuito al tuo utente. In caso contrario, verifica che l’email configurata sia corretta.

---

<!-- 
Capire come cambiare l'url di git remote add origin perché ho cambiato nome alla repository su git... 
In generale rivedermi git remote.
-->

[Collegarsi ad un server remoto](https://youtu.be/qj_q0idpeMQ?t=641&si=9j7vWgyLVRmaP7Nv) (come GitHub) dobbiamo usare il comando `$ git remote`.  

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

# Riassunto

<!-- 
Elencare qui quindi le azioni da fare per instanziare un progetto in Git. 
-->

1. Inizializziamo un progetto non esistente muovendoci nella _working directory_ con `cd` o aprendo vscode in quella cartella e usiamo:
   ```powershell
   git init
   ```
  1. (OPZIONALE)
     Se vogliamo partire da un progetto esistente:
     ```powershell
     git clone <URL>
     ```
     ```powershell
     git remote add <nome> <URL>
     ```
etc.

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