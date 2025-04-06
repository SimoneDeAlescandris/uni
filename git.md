# Indice

- <!-- TODO -->
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

- **`$ git init`**: comando iniziale per avviare il monitoraggio di un progetto con Git. Deve essere eseguito nella directory del progetto e crea una nuova subdirectory denominata `.git`, contenente tutti i file necessari per il repository. Con questo solo comando preliminare non viene ancora tracciato alcun file.

  ```powershell
  $ git init
  ```

- **`$ git add`**: per iniziare a tracciare i file. Può essere utilizzato in diversi modi:

  ```powershell
  $ git add README.py   # Aggiunge un singolo file specificato all'area di stage
  $ git add .           # Aggiunge tutti i file nella directory corrente e nelle subdirectory
  $ git add *.txt       # Aggiunge tutti i file con estensione .txt (o qualche essa sia) nella directory corrente
  ```

- **`$ git status`**: mostra informazioni dettagliate sullo stato dei file nel repository e determina quali file sono modificati, tracciati o non tracciati.

  ```powershell
  $ git status
	
  # Per una visualizzazione più sintetica si possono usare:

  $ git status -s
  # oppure
  $ git status --short
  ```

  Esempio di output:
  ```powershell
  M README.py						# M	 : file modificato, ma non ancora aggiunto all'area di stage
  MM Rakefile						# MM : file modificato, messo in stage e poi ulteriormente modificato.
  A  lib/git.rb					# A	 : file, nuovo, aggiunto all'area di stage
  M  lib/simplegit.rb		# file modificato ed è già in area di stage.
  ?? LICENSE.txt				# ?? : file non tracciato
  ```

---
---
---

- **`git commit`**: salva uno snapshot permanente dei file che si trovano *nell'area di stage* nel repository locale. Non registra automaticamente *tutti* i cambiamenti, ma solo quelli che sono stati aggiunti all'area di stage attraverso `git add`. Eventuali modifiche apportate dopo tale comando non saranno incluse nel commit finché non verranno registrate con `git add`.
  
  ```powershell
	git commit -m "Titolo: Ciao" -m "Descrizione: Messaggio descrittivo"
	```
  
	L'opzione `-m`, non necessaria, permette di scrivere direttamente un messaggio di fianco ad ogni commit per avere un nostro report sulle informazioni che avevamo quando lo avevamo creato.  

	#### TODO
  - **Altre opzioni utili**:
    - `git commit -a -m "Messaggio"`: aggiunge automaticamente *tutti* i file tracciati modificati e poi committa (equivalente a `git add` + `git commit`).
    - `git commit --amend`: modifica l'ultimo commit, utile per correggere il messaggio o aggiungere altri file dimenticati.

---

- **`git log`**: mostra la cronologia di tutti i commit effettuati, in ordine dal più recente al più vecchio, in modo da poter visionare quali modifiche sono state fatte, da chi, e con quale messaggio (oppure per recuperare l'ID di un commit).
	
	```powershell
  git log
  ```

  - **Esempio pratico**:  
    Dopo alcuni commit, eseguendo `git log`, puoi vedere un output simile a:
    ```powershell
    commit 3f9c1bfae3f2d7b123456789abcdef123456789
    Author: Simone <simone@example.com>
    Date:   Sat Apr 6 10:00 2025 +0200

        Fix: corretto bug nel calcolo del fattoriale

    commit 1a2b3c4d5e6f7890123456789abcdef12345678
    Author: Simone <simone@example.com>
    Date:   Sat Apr 6 09:30 2025 +0200

        Add: aggiunta funzione per il calcolo del massimo comune divisore
    ```

  - **Come leggerlo**:
    - **commit**: è l'hash identificativo del commit, unico per ogni cambiamento.
    - **Author**: chi ha fatto il commit.
    - **Date**: quando è stato fatto.
    - **Messaggio**: descrizione data al commit.

  - **Opzioni utili**:
    - `git log --oneline`: mostra ogni commit su una singola riga, molto più compatto.
    - `git log --graph --oneline`: aggiunge anche un piccolo grafico ad albero, utile per visualizzare i rami.
    - `git log -p`: mostra anche le modifiche effettive (diff) apportate da ogni commit.

  - **Attenzione**:  
    Il comando `git log` è solo di lettura. Non modifica nulla. È sicuro da usare tutte le volte che vuoi.

---

**Domande per verificare la tua comprensione**:

1. Se modifichi un file e fai subito `git commit -m "Messaggio"` senza prima `git add`, che cosa accade?

2. Se vuoi correggere il messaggio dell'ultimo commit perché hai scritto male una parola, quale comando devi usare?

3. Se vuoi vedere rapidamente l’elenco dei tuoi ultimi 5 commit in modo compatto, che comando useresti?

---

**Fonte**:  
- Pro Git Book, Capitolo 2.1 — Git Basics  
- Pro Git Book, Capitolo 2.2 — Git Status  
- [Git SCM Documentation](https://git-scm.com/docs/git-commit)  
- [Git SCM Documentation](https://git-scm.com/docs/git-log)

---

Ti consiglio di provare subito alcuni di questi comandi in un repository di test, se vuoi posso anche proporti un esercizio pratico per consolidare!  
Vuoi che te ne prepari uno? 🎯

- `$ git log`
   
	Per visualizzare la cronologia dei commit il comando da eseguire sarà
	
	```powershell
	$ git log
	```
   
	By default, with no arguments, `git log` lists the commits made in that repository in reverse chronological order – that is, the most recent commits show up first. As you can see, this command lists each commit with its SHA-1 checksum, the author’s name and e-mail, the date written, and the commit message.
   
 - Ci sono una marea di opzioni che puoi aggiungere a questo comando, tra le più utili abbiamo:
    - `-p`, which shows the difference introduced in each commit. You can also use `-2`, which limits the output to only the last two entries:
  		   
		```powershell
		$ git log -p -2
		commit ca82a6dff817ec66f44342007202690a93763949
		Author: Scott Chacon <schacon@gee-mail.com>
		Date:   Mon Mar 17 21:52:11 2008 -0700

			changed the version number

		diff --git a/Rakefile b/Rakefile
		index a874b73..8f94139 100644
		--- a/Rakefile
		+++ b/Rakefile
		@@ -5,7 +5,7 @@ require 'rake/gempackagetask'
		spec = Gem::Specification.new do |s|
		s.platform  =   Gem::Platform::RUBY
		s.name      =   "simplegit"
		-    s.version   =   "0.1.0"
		+    s.version   =   "0.1.1"
		s.author    =   "Scott Chacon"
		s.email     =   "schacon@gee-mail.com"
		s.summary   =   "A simple gem for using Git in Ruby code."

		commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
		Author: Scott Chacon <schacon@gee-mail.com>
		Date:   Sat Mar 15 16:40:33 2008 -0700

			removed unnecessary test

		diff --git a/lib/simplegit.rb b/lib/simplegit.rb
		index a0a60ae..47c6340 100644
		--- a/lib/simplegit.rb
		+++ b/lib/simplegit.rb
		@@ -18,8 +18,3 @@ class SimpleGit
		end

		end
		-
		-if $0 == __FILE__
		-  git = SimpleGit.new
		-  puts git.show
		-end
		\ No newline at end of file
		```
		   
    - You can also use a series of summarizing options with `git log`. For example, if you want to see some abbreviated stats for each commit, you can use the `--stat` option:
       
     ```powershell
     $ git log --stat
     commit ca82a6dff817ec66f44342007202690a93763949
     Author: Scott Chacon <schacon@gee-mail.com>
     Date:   Mon Mar 17 21:52:11 2008 -0700

     	changed the version number

     Rakefile | 2 +-
     1 file changed, 1 insertion(+), 1 deletion(-)

     commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
     Author: Scott Chacon <schacon@gee-mail.com>
     Date:   Sat Mar 15 16:40:33 2008 -0700

     	removed unnecessary test

     lib/simplegit.rb | 5 -----
     1 file changed, 5 deletions(-)

     commit a11bef06a3f659402fe7563abf99ad00de2209e6
     Author: Scott Chacon <schacon@gee-mail.com>
     Date:   Sat Mar 15 10:31:28 2008 -0700

     	first commit

     README           |  6 ++++++
     Rakefile         | 23 +++++++++++++++++++++++
     lib/simplegit.rb | 25 +++++++++++++++++++++++++
     3 files changed, 54 insertions(+)
     ```
		   
    - Another really useful option is `--pretty`. This option changes the log output to formats other than the default. A few prebuilt options are available for you to use. The `oneline` option prints each commit on a single line, which is useful if you’re looking at a lot of commits. In addition, the `short`, `full`, and `fuller` options show the output in roughly the same format but with less or more information, respectively:
		   
			```powershell
			$ git log --pretty=oneline
			ca82a6dff817ec66f44342007202690a93763949 changed the version number
			085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7 removed unnecessary test
			a11bef06a3f659402fe7563abf99ad00de2209e6 first commit
			```
		   
    - The most interesting option is `format`, which allows you to specify your own log output format. This is especially useful when you’re generating output for machine parsing – because you specify the format explicitly, you know it won’t change with updates to Git:
		   
			```powershell
			$ git log --pretty=format:"%h - %an, %ar : %s"
			ca82a6d - Scott Chacon, 6 years ago : changed the version number
			085bb3b - Scott Chacon, 6 years ago : removed unnecessary test
			a11bef0 - Scott Chacon, 6 years ago : first commit
			```
		   
		[Useful options for `git log --pretty=format`](https://git-scm.com/book/it/v2/ch00/rpretty_format) lists some of the more useful options that format takes.
		   
   
  ---
   
  #### **Limiting Log Output**
   
	In addition to output-formatting options, `git log` takes a number of useful limiting options – that is, options that let you show only a subset of commits. You’ve seen one such option already – the `-2` option, which show only the last two commits. In fact, you can do `-<n>`, where `n` is any integer to show the last `n` commits. In reality, you’re unlikely to use that often, because Git by default pipes all output through a pager so you see only one page of log output at a time.

	However, the time-limiting options such as `--since` and `--until` are very useful. For example, this command gets the list of commits made in the last two weeks:

	`$ git log --since=2.weeks`
   
	This command works with lots of formats – you can specify a specific date like `"2008-01-15"`, or a relative date such as `"2 years 1 day 3 minutes ago"`.
   
   You can also filter the list to commits that match some search criteria. The `--author` option allows you to filter on a specific author, and the `--grep` option lets you search for keywords in the commit messages. (Note that if you want to specify both author and grep options, you have to add `--all-match` or the command will match commits with either.)
   
   Another really helpful filter is the `-S` option which takes a string and only shows the commits that introduced a change to the code that added or removed that string. For instance, if you wanted to find the last commit that added or removed a reference to a specific function, you could call:
   
   `$ git log -Sfunction_name`
   
   The last really useful option to pass to `git log` as a filter is a path. If you specify a directory or file name, you can limit the log output to commits that introduced a change to those files. This is always the last option and is generally preceded by double dashes (`--`) to separate the paths from the options.
   
   In [Options to limit the output of `git log`](https://git-scm.com/book/it/v2/ch00/rlimit_options) we’ll list these and a few other common options for your reference.
   
- `$ git clone`
   
	Se desideri ottenere una copia di un repository Git esistente, il comando che ti serve è `git clone [url]`:

	```powershell
	$ git clone https://github.com/libgit2/libgit2
	```
   
- [`$ git tag](https://git-scm.com/book/it/v2/Git-Basics-Tagging) (e $ git show)`
   
	Come la maggior parte dei VCS, Git ha la capacità di contrassegnare punti specifici della storia come importanti. In genere le persone utilizzano questa funzionalità per contrassegnare i release points (v1.0 e così via). In questa sezione imparerai come elencare i tag disponibili, come crearne di nuovi e quali sono i diversi tipi di tag.

	#### **Listing Your Tags**
   
	Elencare i tag disponibili in Git è semplice. Basta digitare `git tag`:
	
	```powershell
	$ git tag
	v0.1
	v1.3
	```
   
	Questo comando elenca i tag in ordine alfabetico; l'ordine in cui appaiono non ha alcuna reale importanza.
	
	Puoi anche cercare tag con uno schema particolare. Il repository sorgente Git, ad esempio, contiene più di 500 tag. Se sei interessato solo a guardare la serie 1.8.5, puoi eseguire questo:
   
	```powershell
	$ git tag -l 'v1.8.5*'
	v1.8.5
	v1.8.5-rc0
	v1.8.5-rc1
	v1.8.5-rc2
	v1.8.5-rc3
	v1.8.5.1
	v1.8.5.2
	v1.8.5.3
	v1.8.5.4
	v1.8.5.5
	```
   
	#### **Creating Tags**
	
	Git utilizza due tipi principali di tag: leggeri (Lightweight) e annotati (Annotated).
	
	Un tag leggero è molto simile a un ramo che non cambia: è solo un puntatore a un commit specifico.
	
	I tag annotati, tuttavia, vengono archiviati come oggetti completi nel database Git. Hanno un checksum; contenere il nome del tagger, l'e-mail e la data; avere un messaggio di tag; e può essere firmato e verificato con GNU Privacy Guard (GPG). In genere è consigliabile creare tag annotati in modo da poter avere tutte queste informazioni; ma se desideri un tag temporaneo o per qualche motivo non vuoi conservare le altre informazioni, sono disponibili anche tag leggeri.
   
	#### **Annotated Tags**
	
	Creating an annotated tag in Git is simple. The easiest way is to specify `-a` when you run the `tag` command:
	
	```powershell
	$ git tag -a v1.4 -m 'my version 1.4'
	$ git tag
	v0.1
	v1.3
	v1.4
	```
	
	You can see the tag data along with the commit that was tagged by using the `git show` command:
   
	```powershell
	$ git show v1.4
	tag v1.4
	Tagger: Ben Straub <ben@straub.cc>
	Date:   Sat May 3 20:19:12 2014 -0700
	
	my version 1.4
	
	commit ca82a6dff817ec66f44342007202690a93763949
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Mar 17 21:52:11 2008 -0700
	
		changed the version number
	```

	That shows the tagger information, the date the commit was tagged, and the annotation message before showing the commit information.
   
	#### **Lightweight Tags**
	
	Another way to tag commits is with a lightweight tag. This is basically the commit checksum stored in a file – no other information is kept. To create a lightweight tag, don’t supply the `-a`, `-s`, or `-m` option:
	
	```powershell
	$ git tag v1.4-lw
	$ git tag
	v0.1
	v1.3
	v1.4
	v1.4-lw
	v1.5
	```
   
	This time, if you run `git show` on the tag, you don’t see the extra tag information. The command just shows the commit:
	
	```powershell
	$ git show v1.4-lw
	commit ca82a6dff817ec66f44342007202690a93763949
	Author: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Mar 17 21:52:11 2008 -0700
	
		changed the version number
	```
   
	#### **Tagging Later**
	
	You can also tag commits after you’ve moved past them. Suppose your commit history looks like this:
   
	```powershell
	$ git log --pretty=oneline
	15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
	a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
	0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
	6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
	0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
	4682c3261057305bdd616e23b64b0857d832627b added a todo file
	166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
	9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
	964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
	8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme
	```
   
	Now, suppose you forgot to tag the project at v1.2, which was at the “updated rakefile” commit. You can add it after the fact. To tag that commit, you specify the commit checksum (or part of it) at the end of the command:
	
	`$ git tag -a v1.2 9fceb02`
   
	You can see that you’ve tagged the commit:
	
	```powershell
	$ git tag
	v0.1
	v1.2
	v1.3
	v1.4
	v1.4-lw
	v1.5
   
	$ git show v1.2
	tag v1.2
	Tagger: Scott Chacon <schacon@gee-mail.com>
	Date:   Mon Feb 9 15:32:16 2009 -0800
	
	version 1.2
	commit 9fceb02d0ae598e95dc970b74767f19372d61af8
	Author: Magnus Chacon <mchacon@gee-mail.com>
	Date:   Sun Apr 27 20:43:35 2008 -0700
	
		updated rakefile
	...
	```
   
	#### **Sharing Tags**
	
	By default, the `git push` command doesn’t transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them. This process is just like sharing remote branches – you can run `git push origin [tagname]`.
	
	```powershell
	$ git push origin v1.5
	Counting objects: 14, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (12/12), done.
	Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
	Total 14 (delta 3), reused 0 (delta 0)
	To git@github.com:schacon/simplegit.git
* [new tag]         v1.5 -> v1.5
	```
   
	If you have a lot of tags that you want to push up at once, you can also use the `--tags` option to the `git push` command. This will transfer all of your tags to the remote server that are not already there.
	
	```powershell
	$ git push origin --tags
	Counting objects: 1, done.
	Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
	Total 1 (delta 0), reused 0 (delta 0)
	To git@github.com:schacon/simplegit.git
* [new tag]         v1.4 -> v1.4
* [new tag]         v1.4-lw -> v1.4-lw
	```
   
	Now, when someone else clones or pulls from your repository, they will get all your tags as well.
	
	### **Checking out Tags**
	
	You can’t really check out a tag in Git, since they can’t be moved around. If you want to put a version of your repository in your working directory that looks like a specific tag, you can create a new branch at a specific tag:
	
	```powershell
	$ git checkout -b version2 v2.0.0
	Switched to a new branch 'version2'
	```
	
	Of course if you do this and do a commit, your `version2` branch will be slightly different than your `v2.0.0` tag since it will move forward with your new changes, so do be careful.
   
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