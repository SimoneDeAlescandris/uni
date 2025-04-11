# Indice

- [init](#init)
- [add](#add)
- [status](#status)
- [commit](#commit)
- [log](#log)
- [clone](#clone)
- [tag](#tag)
- [show](#show)
- [.gitignore](#gitignore)
- [rm](#rm)
- [mv](#mv)

- [Per collegarsi ad un server remoto](#collegarsi-ad-un-server-remoto)
- [Bibliografia](#bibliografia)

---
---
---

# Introduzione

Un Sistema di Controllo Versione (**VCS**, _Version Control System_) registra nel tempo le modifiche apportate a un file o a un insieme di file, permettendo di ripristinare versioni precedenti in qualsiasi momento. Utilizzarne uno è fondamentale per mantenere la cronologia completa delle modifiche e garantire un recupero rapido in caso di errori.  
Tra questi, **Git**, creato da Linus Torvalds nel 2005, è ad oggi lo standard de facto. È un sistema di controllo versione <u>distribuito</u>, il che significa che ogni sviluppatore possiede una copia completa del progetto, comprensiva della sua cronologia. Questa caratteristica offre:
- <u>Flessibilità</u>, perché ogni sviluppatore può lavorare indipendentemente;
- <u>Sicurezza</u>, perché la perdita di un server centrale non compromette il progetto;
- <u>Efficienza</u>, grazie alla gestione rapida di versioni e modifiche. 
  Git considera i propri dati più come una sequenza di istantanee (**snapshot**) in un mini filesystem. Ogni
  volta che si registra (commit) lo stato del progetto, Git fondamentalmente fa un’immagine di tutti i file in quel momento e per essere efficiente, se alcuni file non sono cambiati, non li risalva, ma crea semplicemente un collegamento al file già precedente salvato.

# Setup

- I file in Git possono essere in tre stati principali:
  - ***modified*** (modificati): il file è stato modificato, ma non è ancora stato committato nel database.  
  - ***staged*** (in stage): hai contrassegnato un file, modificato nella versione corrente, perché venga inserito nello snapshot alla prossima commit.
  - ***committed*** (committati): il file è registrato al sicuro nel database locale.
	
	<img src="https://git-scm.com/book/en/v2/images/areas.png" alt="Rappresentazione dei tre stati possibili in Git" width="40%">
	

L’**albero di lavoro** è un checkout di una versione specifica del progetto. Questi file vengono estratti dal database compresso nella directory di Git, e salvati sul disco per essere usati o modificati.

L’***area di stage*** è un file, contenuto generalmente nella directory di Git, con tutte le informazioni riguardanti la tua prossima commit. Il suo nome tecnico nel gergo di Git è ***indice***.

La directory di Git è dove Git salva i metadati e il database degli oggetti del tuo progetto. Questa è la parte più importante di Git, ed è ciò che viene copiato quando si clona un repository da un altro computer.

- Il flusso di lavoro (***workflow***) di base in Git funziona così:
	1. Modifica i file nel tuo albero di lavoro.
	2. Seleziona per lo stage solo quei cambiamenti che vuoi facciano parte del tuo prossimo commit, che aggiunge solo queste modifiche all’area di stage.
	3. Committa, ovvero salva i file nell’area di stage in un’istantanea (***snapshot***) permanente nella tua directory di Git.

Se una particolare versione di un file è nella directory git, viene considerata già committata (***committed***). Se il file è stato modificato, ma è stato aggiunto all’area di staging, è ***in stage***. E se è stato modificato da quando è stata estratto, ma non è ***in stage***, è ***modificato***.

<img src="./img/6_git.png" alt="Logo Git" title="Logo Git" width="8%" style="float:left; position: relative; padding:2%">

### **`Chiedere aiuto`**

Se dovessi avere bisogno di aiuto durante l’uso di Git, ci sono tre modi per visualizzare la pagina di aiuto (pagina man) di ciascun comando di Git, direttamente dal manuale.

```powershell
$ git help <comando>
$ git <comando> --help
$ man git-<comando>
```

Puoi, per esempio, leggere la pagina man del comando config eseguendo:

```powershell
$ git help config
```
# [*Cos'è, come funziona e come usare GIT*](https://youtu.be/qj_q0idpeMQ?si=wKBShBqM7aJyM2w_)

Per prima cosa, è utile sapere che usando “**<span style="color: skyblue;">Git</span> <span style="color: #FDDC5C;">Ba</span><span style="color: green;">sh</span>**” potrebbero esserci delle funzioni in più rispetto che ad usare git nel terminale di Windows.

Aprendo l’applicazione tra le prime cose che dobbiamo fare è spostarci nella cartella in cui desideriamo lavorare e quindi utilizzare il comando `cd` seguito dal percorso della cartella tra le virgolette.	

<!-- Nel libro ProGit sono arrivato a pagina 8 -->

---
---
---

## Tra i comandi più utili abbiamo:

- **<span id="init" style="font-size: 16px;">`$ git init`</span>**: comando iniziale per avviare il monitoraggio di un progetto con Git. Deve essere eseguito nella directory del progetto e crea una nuova subdirectory denominata `.git`, contenente tutti i file necessari per il repository. Con questo solo comando preliminare non viene ancora tracciato alcun file.
  ```powershell
  git init
  ```

- **<span id="add" style="font-size: 16px;">`$ git add`</span>**: per iniziare a tracciare i file. Può essere utilizzato in diversi modi:
  ```powershell
  git add README.py   # Aggiunge un singolo file specificato all'area di stage
  git add .           # Aggiunge tutti i file nella directory corrente e nelle subdirectory
  git add *.txt       # Aggiunge tutti i file con estensione .txt (o qualche essa sia) nella directory corrente
  ```

- **<span id="status" style="font-size: 16px;">`$ git status`</span>**: mostra informazioni dettagliate sullo stato dei file nel repository e determina quali file sono modificati, tracciati o non tracciati.
  ```powershell
  git status
  # Per una visualizzazione più sintetica si possono usare:
  git status -s
  # oppure
  git status --short
  ```
  Esempio di output:
	```powershell
	M README.py						# M	 : file modificato, ma non ancora aggiunto all'area di stage
	MM Rakefile						# MM : file modificato, messo in stage e poi ulteriormente modificato.
	A  lib/git.rb					# A	 : file, nuovo, aggiunto all'area di stage
	M  lib/simplegit.rb		# file modificato ed è già in area di stage.
	?? LICENSE.txt				# ?? : file non tracciato
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

- **<span id="clone" style="font-size: 16px;">`$ git clone [url]`</span>**: ottieni una copia di un repository Git esistente, incluso lo storico dei commit, i rami, i tag, e la configurazione interna del progetto.
	```powershell
	git clone https://github.com/libgit2/libgit2
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

- **<span id="gitignore" style="font-size: 16px;">`.gitignore`</span>**: file di testo usato per dire a Git quali file o cartelle non tracciare. Si crea nella root del repository.  
  ```powershell  
  echo "*.log" >> .gitignore
  echo "build/" >> .gitignore
  echo "*~" >> .gitignore
  git add .gitignore
  git commit -m "Aggiunto file .gitignore"
  ```
	Ogni riga rappresenta un pattern, ad esempio `*.log` ignora tutti i file `.log`, `build/` ignora tutta la cartella `build`. La terza riga dice a Git di ignorare tutti i file che terminano con una tilde (~), utilizzata da molti editor di testo, come Emacs, per contrassegnare i file temporanei.  
	Le regole per i modelli che puoi inserire nel file `.gitignore` sono le seguenti:  
  - Le righe vuote o le righe che iniziano con `#` vengono ignorate;
  - È possibile terminare i modelli con una barra ( `/`) per specificare una directory;  
  - Puoi negare uno schema iniziandolo con un punto esclamativo ( `!`);  
  - I modelli glob standard funzionano.  
  	Essi sono come espressioni regolari semplificate utilizzate dalle shell. Un asterisco ( `*`) corrisponde a zero o più caratteri; `[abc]`corrisponde a qualsiasi carattere all'interno delle parentesi (in questo caso a, b o c); un punto interrogativo ( `?`) corrisponde a un singolo carattere; e le parentesi che racchiudono caratteri separati da un trattino( `[0-9]`) corrispondono a qualsiasi carattere tra di loro (in questo caso da 0 a 9). Puoi anche utilizzare due asterischi per abbinare le directory nidificate; `a/**/z`corrisponderebbe a `a/z`, `a/b/z`, `a/b/c/z`, e così via.
   
- **<span id="rm" style="font-size: 16px;">`$ git rm`</span>**: rimuove file sia dal working directory che dall’indice (staging area). Se vuoi solo smettere di tracciarlo ma lasciarlo sul disco, devi usare l’opzione `--cached`.  
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
  
- **`$ git diff`**: mostra le differenze, riga per riga, tra i file modificati e l’ultima versione tracciata (HEAD o staging area). Serve per vedere *cosa* cambierà prima di committare.  
  ```powershell
  git diff
  ```
  mostra le modifiche non ancora aggiunte, mentre
  ```powershell
  git diff --staged
  ```
  mostra le modifiche che hai già aggiunto con `git add` e che finiranno nel prossimo commit.  

	Insomma, serve se il comando `$ git status` fosse un po’ troppo vago per i tuoi standard e tu volessi sapere esattamente cosa è cambiato.  
	
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
- [Working with GitHub in VS Code](https://code.visualstudio.com/docs/sourcecontrol/github).