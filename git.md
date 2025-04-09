# Indice
- [init](#init)
- [add](#add)
- [status](#status)
- [commit](#commit)
- [log](#log)
- [clone](#clone)
- [tag](#tag)
- [show](#show)
<!-- TODO -->
  - [Notion](#notion)
- [Bibliografia](#bibliografia)<br><br>

# Bibliografia:

- [Learn Git Branching](https://learngitbranching.js.org/?locale=it_IT);
- [tesseslol, guida git](https://gist.github.com/tesseslol/da62aabec74c4fed889ea39c95efc6cc);
- [Pro Git - Scott Chacon, Ben Straub](https://git-scm.com/book/it/v2);
- [Edoardo Midali](https://www.youtube.com/watch?v=wPAE9-DdMtI);
- [Using Git source control in VS Code](https://code.visualstudio.com/docs/sourcecontrol/overview);
- [Introduction to Git in VS Code](https://code.visualstudio.com/docs/sourcecontrol/intro-to-git);
- [Version control in VS Code](https://code.visualstudio.com/docs/introvideos/versioncontrol);
- [Working with GitHub in VS Code](https://code.visualstudio.com/docs/sourcecontrol/github).

Premessa importante è il concetto di "*Controllo di Versione*".

Git è lo standard de facto per il controllo versione del codice sorgente. Permette di tracciare le modifiche, collaborare con altri sviluppatori e gestire diverse versioni del codice in modo efficiente.  
La sua natura distribuita offre flessibilità e sicurezza, mentre le funzionalità di branching lo rendono perfetto per qualsiasi flusso di lavoro di sviluppo.

# Intro

# Setup

# TODO

# vscode guida

# Notion
<img src="./img/6_git.png" alt="Logo Git" title="Logo Git" width="15%">

## 1 - Per iniziare  
   
**Git** ti permette, lavorando in locale, di ripristinare persino un intero progetto a uno stato precedente, revisionare le modifiche fatte nel tempo, vedere chi ha cambiato qualcosa che può aver causato un problema, chi ha introdotto un problema e quando, e molto altro ancora. Usare un VCS (Sistema per il Controllo di Versione) come Git, in generale, significa anche che se fai un pasticcio o perdi qualche file, puoi facilmente recuperare la situazione.

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
## [*Cos'è, come funziona e come usare GIT*](https://youtu.be/qj_q0idpeMQ?si=wKBShBqM7aJyM2w_)

Per prima cosa, è utile sapere che usando “**<span style="color: skyblue;">Git</span> <span style="color: #FDDC5C;">Ba</span><span style="color: green;">sh</span>**” potrebbero esserci delle funzioni in più rispetto che ad usare git nel terminale di Windows.

Aprendo l’applicazione tra le prime cose che dobbiamo fare è spostarci nella cartella in cui desideriamo lavorare e quindi utilizzare il comando `cd` seguito dal percorso della cartella tra le virgolette.	

### Tra i comandi più utili abbiamo:

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

---
---
---
---
---
---
---
---
---
---

- **`.gitignore`**: file di testo usato per dire a Git quali file o cartelle ignorare (non tracciare). Ogni riga rappresenta un pattern, ad esempio `*.log` ignora tutti i file `.log`, `build/` ignora tutta la cartella `build`. Si crea nella root del repository. Esempio:
  ```bash
  echo "*.log" >> .gitignore
  echo "build/" >> .gitignore
  git add .gitignore
  git commit -m "Aggiunto file .gitignore"
  ```

- `.gitignore`
   
	Spesso avrai una classe di file che non vuoi che Git aggiunga automaticamente o addirittura ti mostri come non tracciati. Si tratta generalmente di file generati automaticamente come file di registro o file prodotti dal sistema di compilazione. In questi casi, è possibile creare un elenco di modelli di file corrispondenti denominati `.gitignore`. Eccone un esempio:
   
	```powershell
	$ cat .gitignore
	*.[oa]
	*~
	```

	La prima riga dice a Git di ignorare qualsiasi file che termina con ".o" o ".a". 
	La seconda riga dice a Git di ignorare tutti i file che terminano con una tilde ( ~), utilizzata da molti editor di testo come Emacs per contrassegnare i file temporanei. Puoi anche includere una directory log, tmp o pid; e così via. 
	Configurare un file .gitignore prima di iniziare è generalmente una buona idea in modo da non commettere accidentalmente file che non desideri davvero nel tuo repository Git.
	
	Le regole per i modelli che puoi inserire nel file `.gitignore` sono le seguenti:
   
  - Le righe vuote o le righe che iniziano con `#` vengono ignorate.
  - I modelli glob standard funzionano.
  - È possibile terminare i modelli con una barra ( `/`) per specificare una directory.
  - Puoi negare uno schema iniziandolo con un punto esclamativo ( `!`).

  I modelli glob sono come espressioni regolari semplificate utilizzate dalle shell. Un asterisco ( `*`) corrisponde a zero o più caratteri; `[abc]`corrisponde a qualsiasi carattere all'interno delle parentesi (in questo caso a, b o c); un punto interrogativo ( `?`) corrisponde a un singolo carattere; e le parentesi che racchiudono caratteri separati da un trattino( `[0-9]`) corrispondono a qualsiasi carattere tra di loro (in questo caso da 0 a 9). Puoi anche utilizzare due asterischi per abbinare le directory nidificate; `a/**/z`corrisponderebbe a `a/z`, `a/b/z`, `a/b/c/z`, e così via.
   
	Di seguito è riportato un altro esempio nell’utilizzo di `.gitignore`:
   
	```powershell
	# no .a files
	*.a

	# but do track lib.a, even though you're ignoring .a files above
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
   
	| **Suggerimento** | GitHub maintains a fairly comprehensive list of good `.gitignore` file examples for dozens of projects and languages at https://github.com/github/gitignore if you want a starting point for your project. |
	| --- | --- |

- **`$ git rm`**: comando che rimuove file sia dal working directory che dall’indice (staging area), preparando la rimozione per il prossimo commit. Se vuoi solo smettere di tracciarlo ma lasciarlo sul disco, devi usare l’opzione `--cached`. Esempio:
  ```bash
  git rm file.txt
  git commit -m "Rimosso file.txt"
  ```
  oppure per ignorarlo mantenendolo:
  ```bash
  git rm --cached file.txt
  echo "file.txt" >> .gitignore
  git commit -m "Ignora file.txt"
  ```

- `$ git rm`
   
	To remove a file from Git, you have to remove it from your tracked files (more accurately, remove it from your staging area) and then commit. The `git rm` command does that, and also removes the file from your working directory so you don’t see it as an untracked file the next time around.
	
	If you simply remove the file from your working directory, it shows up under the “Changed but not updated” (that is, ***unstaged***) area of your `git status` output:
	
	```powershell
	$ rm PROJECTS.md
	$ git status
	On branch master
	Your branch is up-to-date with 'origin/master'.
	Changes not staged for commit:
	(use "git add/rm <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)
	
			deleted:    PROJECTS.md
	
	no changes added to commit (use "git add" and/or "git commit -a")
	```
   
	Then, if you run `git rm`, it stages the file’s removal:
	
	```powershell
	$ git rm PROJECTS.md
	rm 'PROJECTS.md'
	$ git status
	On branch master
	Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)
	
		deleted:    PROJECTS.md
	```
   
	La prossima volta che eseguirai il commit, il file scomparirà e non sarà più tracciato. Se hai modificato il file e lo hai già aggiunto all'indice, you must force the removal with the `-f` option. Questa è una funzionalità di sicurezza per impedire la rimozione accidentale di dati che non sono stati ancora registrati in uno snapshot e che non possono essere recuperati da Git.
	
	Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your `.gitignore` file and accidentally staged it, like a large log file or a bunch of `.a` compiled files. To do this, use the `--cached` option:
	
	```powershell
	$ git rm --cached README
	```
   
	You can pass files, directories, and file-glob patterns to the `git rm` command. That means you can do things such as
	
	```powershell
	$ git rm log/\*.log
	```
	
	Note the backslash (`\`) in front of the `*`. This is necessary because Git does its own filename expansion in addition to your shell’s filename expansion. This command removes all files that have the `.log` extension in the `log/` directory. Or, you can do something like this:
	
	```powershell
	$ git rm \*~
	```

	This command removes all files that end with ~.
   

- **`$ git mv`**: comando che sposta o rinomina un file o una cartella e automaticamente aggiorna l’indice. È equivalente a fare manualmente `mv` e poi `git add` e `git rm`. Esempio:
  ```bash
  git mv vecchio_nome.txt nuovo_nome.txt
  git commit -m "Rinominato file"
  ```

- **`$ git diff`**: mostra le differenze riga per riga tra i file modificati e l’ultima versione tracciata (HEAD o staging area). Serve per vedere *cosa* cambierà prima di committare. Esempio:
  ```bash
  git diff
  ```
  mostra le modifiche non ancora aggiunte, mentre
  ```bash
  git diff --staged
  ```
  mostra le modifiche che hai già aggiunto con `git add` e che finiranno nel prossimo commit.

---

- `$ git mv`
   
	Per rinominare un file in Git possiamo usare il comando:
	
	```powershell
	$ git mv file_from file_to
	```
	
	e funziona bene. Infatti, se esegui qualcosa del genere e guardi lo stato, vedrai che Git lo considera un file rinominato:
	
	```powershell
	$ git mv README.md README
	$ git status
	On branch master
	Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)
	
		renamed:    README.md -> README
	```
   
	Tuttavia, ciò equivale a eseguire qualcosa del genere:
	
	```powershell
	$ mv README.md README
	$ git rm README.md
	$ git add README
	```
   
- `$ git diff`
   
	Se il comando `$ git status` fosse un po’ troppo vago per i tuoi standard e tu volessi sapere esattamente cosa è cambiato puoi usare il comando `$ git diff`. Prima di parlarne nel dettaglio però è giusto rispondere alle due domande che probabilmente ci si fa quando lo si utilizza: What have you changed but not yet staged? And what have you staged that you are about to commit? Although `git status` answers those questions very generally by listing the file names, `git diff` shows you the exact lines added and removed – the patch, as it were.
	
	Let’s say you edit and stage the `README` file again and then edit the `CONTRIBUTING.md` file without staging it. If you run your `git status` command, you once again see something like this:
	
	```powershell
	$ git status
	On branch master
	Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)
	
		new file:   README
	
	Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)
	
		modified:   CONTRIBUTING.md
	```
   
	To see what you’ve changed but not yet staged, type `git diff` with no other arguments:
	
	```powershell
	$ git diff
	diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
	index 8ebb991..643e24f 100644
	--- a/CONTRIBUTING.md
	+++ b/CONTRIBUTING.md
	@@ -65,7 +65,8 @@ branch directly, things can get messy.
	Please include a nice description of your changes when you submit your PR;
	if we have to read the whole diff to figure out why you're contributing
	in the first place, you're less likely to get feedback and have your change
		-merged in.
		+merged in. Also, split your changes into comprehensive chunks if you patch is
		+longer than a dozen lines.
		
	If you are starting to work on a particular area, feel free to submit a PR
	that highlights your work in progress (and note in the PR title that it's
	```

	Questo comando confronta ciò che è nella tua directory di lavoro con ciò che è nella tua area di staging. Il risultato ti dice le modifiche che hai apportato che non hai ancora messo in scena.
   
	If you want to see what you’ve staged that will go into your next commit, you can use `git diff --staged`. This command compares your staged changes to your last commit:
	
	```powershell
	$ git diff --staged
	diff --git a/README b/README
	new file mode 100644
	index 0000000..03902a1
	--- /dev/null
	+++ b/README
	@@ -0,0 +1 @@
	+My Project
	```
   
	It’s important to note that `git diff` by itself doesn’t show all changes made since your last commit – only changes that are still unstaged. This can be confusing, because if you’ve staged all of your changes, `git diff` will give you no output.
   
	For another example, if you stage the `CONTRIBUTING.md` file and then edit it, you can use `git diff` to see the changes in the file that are staged and the changes that are unstaged. If our environment looks like this:
	
	```powershell
	$ git add CONTRIBUTING.md
	$ echo 'test line' >> CONTRIBUTING.md
	$ git status
	On branch master
	Changes to be committed:
	(use "git reset HEAD <file>..." to unstage)
	
		modified:   CONTRIBUTING.md
	
	Changes not staged for commit:
	(use "git add <file>..." to update what will be committed)
	(use "git checkout -- <file>..." to discard changes in working directory)
	
		modified:   CONTRIBUTING.md
	```
   
	Now you can use `git diff` to see what is still unstaged
	
	```powershell
	$ git diff
	diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
	index 643e24f..87f08c8 100644
	--- a/CONTRIBUTING.md
	+++ b/CONTRIBUTING.md
	@@ -119,3 +119,4 @@ at the
	## Starter Projects
	
	See our [projects list](https://github.com/libgit2/libgit2/blob/development/PROJECTS.md).
		+# test line
	```
   
	and `git diff --cached` to see what you’ve staged so far (--staged and --cached are synonyms):
   
	```powershell
	$ git diff --cached
	diff --git a/CONTRIBUTING.md b/CONTRIBUTING.md
	index 8ebb991..643e24f 100644
	--- a/CONTRIBUTING.md
	+++ b/CONTRIBUTING.md
	@@ -65,7 +65,8 @@ branch directly, things can get messy.
	Please include a nice description of your changes when you submit your PR;
	if we have to read the whole diff to figure out why you're contributing
	in the first place, you're less likely to get feedback and have your change
		-merged in.
		+merged in. Also, split your changes into comprehensive chunks if you patch is
		+longer than a dozen lines.
		
	If you are starting to work on a particular area, feel free to submit a PR
	that highlights your work in progress (and note in the PR title that it's
	```
   
	| **Nota** | **Git Diff in an External Tool**
	We will continue to use the `git diff` command in various ways throughout the rest of the book. There is another way to look at these diffs if you prefer a graphical or external diff viewing program instead. If you run `git difftool` instead of `git diff`, you can view any of these diffs in software like Araxis, emerge, vimdiff and more. Run `git difftool --tool-help` to see what is available on your system. |
	| --- | --- |

---
---
---

- [Per collegarsi ad un server remoto](https://youtu.be/qj_q0idpeMQ?t=641&si=9j7vWgyLVRmaP7Nv) (come GitHub) dobbiamo usare il comando `$ git remote`.

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