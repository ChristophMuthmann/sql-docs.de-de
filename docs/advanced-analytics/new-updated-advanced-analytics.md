---
title: "Aktualisiert – Advanced Analytics für SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für Advanced Analytics für Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2017
ms.author: genemi
ms.workload: 
ms.openlocfilehash: c73c6295f7b6e2a23c947ab65160032ce83264e1
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/20/2017
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Neue und kürzlich aktualisierte: Advanced Analytics für SQLServer



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates*: &nbsp; **28.09.2017** &nbsp; – bis – &nbsp; **02.12.2017**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Advanced Analytics für SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Hinzufügen der SQLRUserGroup als Datenbankbenutzer](r/add-sqlrusergroup-to-database.md)
2. [So verwenden Sie RevoScaleR-Funktionen zum Suchen, oder installieren R-Pakete auf SQL Server](r/use-revoscaler-to-manage-r-packages.md)
3. [Verwendung von R in Azure SQL-Datenbank](r/using-r-in-azure-sql-database.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Bekannte Probleme in Machine Learning-Diensten](#TitleNum_1)
2. [Erstellen eines lokalen Paketrepositorys mit miniCRAN](#TitleNum_2)
3. [Bestimmen Sie, welche R-Pakete auf SQL Server installiert sind](#TitleNum_3)
4. [Installieren Sie zusätzliche R-Pakete unter SQL Server](#TitleNum_4)
5. [Installieren von SQL Server-Machine learning-Features auf virtuellen Azure-Computer](#TitleNum_5)
6. [Installieren Sie vortrainierte Machine learning-Modelle mit SQL Server](#TitleNum_6)
7. [Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert](#TitleNum_7)
8. [Bereitstellen eines virtuellen Computers für Machine Learning in Azure](#TitleNum_8)
9. [RevoScaleR](#TitleNum_9)
10. [Aktivieren Sie oder deaktivieren Sie der Verwaltung von R-Paket für SQL Server](#TitleNum_10)
11. [Einrichten eines Data Science-Clients für die Verwendung mit SQL Server](#TitleNum_11)
12. [Einrichten von SQL Server Machine Learning Services (datenbankintern)](#TitleNum_12)
13. [Unbeaufsichtigte Installation von Machine Learning-Services (Datenbankintern)](#TitleNum_13)
14. [Schritt 3: Durchsuchen und Visualisieren der Daten](#TitleNum_14)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp;[Bekannte Probleme in Machine Learning-Diensten](known-issues-for-sql-server-machine-learning-services.md)

*Aktualisiert: 2017-11 – 16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 321.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00121c648c21576d5c86494137de1d4d81e2e265 c65973f6ae9253af5ecc621916ef36d7c0398789  (PR=3980  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



**Python-code die Ausführung oder Python-Paket Probleme**


Dieser Abschnitt enthält bekannte Probleme, die zum Ausführen von Python bei SQL Server als auch Probleme mit der Python-Pakete, die von Microsoft veröffentlichten sind spezifisch sind einschließlich [Revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) und [Microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

**Vortrainierte Modell Aufruf fehlschlägt, wenn der Pfad zum Modell zu lang ist**


Bei der Installation die vortrainierte Modelle in einer Standardinstallation, je nach Ihren Computernamen und den Instanznamen, möglicherweise die resultierende vollständige Pfad zur Modelldatei trainierten zu lang für Python zu lesen. Diese Einschränkung wird in einer bevorstehenden Dienstversion behoben werden.

Es gibt mehrere mögliche problemumgehungen:

+ Wählen Sie einen benutzerdefinierten Speicherort, bei der Installation die vortrainierte Modelle.
+ Wenn möglich, installieren Sie SQL Server-Instanz ein benutzerdefinierter Installationspfad, z. B. C:\SQL\MSSQL14. MSSQLSERVER.
+ Verwenden Sie das Windows-Dienstprogramm [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) um einen Hardlink zu erstellen, die Modelldatei zu einem kürzeren Pfad entspricht.

**Fehler beim Initialisieren einer Variablen Varbinary verursacht einen Fehler in BxlServer**


Wenn das Ausführen von Python-Code in SQL Server mit `sp_execute_external_script`, und der Code hat Variablen vom Typ varbinary(max), varchar(max) oder ähnliche Typen ausgegeben, die Variable initialisiert oder als Teil Ihres Skripts festgelegt werden muss. Andernfalls löst die Exchange-Komponente, BxlServer, Fehler und angehalten.

Diese Einschränkung wird in einer bevorstehenden Dienstversion behoben werden. Dieses Problem zu umgehen sicher, dass die Variable in der Python-Skript initialisiert wird. Jeder gültiger Wert kann verwendet werden, wie in den folgenden Beispielen:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-create-a-local-package-repository-using-minicranrcreate-a-local-package-repository-using-minicranmd"></a>2. &nbsp;[Erstellen Sie ein lokales Paket-Repository mit MiniCRAN](r/create-a-local-package-repository-using-minicran.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 43.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 44b77cb127e9ffab1777216a66f0e5be9c82f3d2 65e30f10fc36acb3ce95f60f51f3501fbc98ad08  (PR=4150  ,  Filename=create-a-local-package-repository-using-minicran.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



-   **Einfacher Offlineinstallation**: beim Installieren des Pakets mit einem offline-Server erfordert, dass Sie auch alle paketabhängigkeiten herunterladen, mit MiniCRAN erleichtert es, rufen Sie alle Abhängigkeiten im richtigen Format ab.

-   **Verbesserte versionsverwaltung**: In einer mehrbenutzerumgebung, es gibt gute Gründe für die uneingeschränkte Paketversionen auf dem Server-Installation zu verhindern.

Nach dem Erstellen des Repositorys an, können Sie es durch Hinzufügen von neuen Paketen oder aktualisieren die Version der vorhandenen Pakete ändern.

**Schritt 1. Installieren Sie das Paket miniCRAN**


Sie beginnen mit dem Erstellen ein Repository MiniCRAN als Quelle verwenden. Sie sollten dieses Repository auf einem Computer erstellen, die Zugang zum Internet hat.

1.  Installieren Sie das Paket MiniCRAN und die erforderlichen **Igraph** Paket.

```
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
```

**Schritt 2. Definieren Sie eine Paketquelle: einen CRAN-Spiegel oder eine Momentaufnahme MRAN**


1. Geben Sie eine gespiegelte Site beim Abrufen der Pakete verwenden.

```
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
```

2.  Geben Sie an einen lokalen Ordner, in dem Sie die gesammelten Pakete zu speichern. Needn't benennen Sie den Ordner MiniCRAN; Es könnte einen aussagekräftigeren Namen wie "GeneticsPackages" oder "ClientRPackages1.0.2" sein.

    Achten Sie auf den Ordner im Voraus erstellen. Ein Fehler wird ausgelöst, wenn die `local_repo` Ordner ist nicht vorhanden, wenn Sie später den R-Code ausführen.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp;[Zu bestimmen, welche R-Pakete auf SQL Server installiert sind](r/determine-which-packages-are-installed-on-sql-server.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 13d93acedc6e6b4615f1a244a2a1542910feb69e 9a065066398843a4bed318fa46d4982d712915a9  (PR=4150  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



+ Wenn das Paket gefunden wird, sollte die zurückgegebene Meldung werden etwa "-Befehle erfolgreich abgeschlossen."

+ Wenn das Paket gespeichert oder geladen werden kann, erhalten Sie eine Fehlermeldung wie folgt: "ein externer Skriptfehler: Fehler in library("RevoScaleR"): ist kein Paket namens" revoscaler ""

**Abrufen einer Liste der installierten Pakete, die mithilfe von R**


Es gibt mehrere Methoden, eine Liste der installierten oder geladenen Pakete mit R-Tools und R-Funktionen zu erhalten. Viele R-Entwicklungstools bieten eine Objektkatalog oder eine Liste der installierten oder in den aktuellen R-Arbeitsbereich geladenen Pakete.

+ Aus einem lokalen R-Hilfsprogramm, verwenden Sie eine Basis R-Funktion, wie z. B. `installed.packages()`, im Lieferumfang der `utils` Paket. Um eine Liste zu erhalten, die für eine Instanz genau ist, müssen Sie Bibliothekspfad explizit angeben oder verwenden Sie die R-Tools, die der Instanz-Bibliothek zugeordnet.

+ Um für ein Paket in einen bestimmten computekontext zu überprüfen, können Sie die folgenden Funktionen aus dem "revoscaler"-Paket verwenden. Diese Funktionen können Sie die Pakete im angegebenen rechenkontexte zu identifizieren:

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

Führen Sie z. B. die folgenden R-Code zum Abrufen einer Liste von Paketen, die in der angegebenen SQL Server-computekontext verfügbar.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
**Siehe auch**




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-install-additional-r-packages-on-sql-serverrinstall-additional-r-packages-on-sql-servermd"></a>4. &nbsp;[Installieren zusätzlicher R-Pakete unter SQL Server](r/install-additional-r-packages-on-sql-server.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_3) | [Weiter](#TitleNum_5))

<!-- Source markdown line 266.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ba48f1838857d90d6692aafc48f393777ac602fa 37de2586a344a99969bcd9a20723c021db2604a4  (PR=4150  ,  Filename=install-additional-r-packages-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Dieser Abschnitt enthält verschiedene Tipps und Beispielcode im Zusammenhang mit der Installation von R-Paket für SQL Server.

**<a name="packageVersion"></a>Rufen Sie die richtige Paketversion und format**


Es gibt mehrere Quellen für R-Pakete. Die bekannteste Quellen sind CRAN und Bioconductor. Auf der offiziellen Website für die R-Sprache (<https://www.r-project.org/>) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden in GitHub veröffentlicht, in dem Sie den Quellcode erhalten können. Aber können Sie R-Pakete zugewiesen wurde, die von einer Person in Ihrem Unternehmen entwickelt wurden.

Unabhängig von der Quelle müssen Sie sicherstellen, dass das Paket, das Sie installieren möchten, ein binäres Format für die Windows-Plattform verfügt. Andernfalls kann nicht das heruntergeladene Paket in der SQL Server-Umgebung ausgeführt.

Vor dem Herunterladen, sollten Sie auch überprüfen, ob das Paket mit der Version von R kompatibel ist, die in SQL Server ausgeführt wird.

**<a name="bkmk_zipPreparation"></a>Paket als ZIP-Datei herunterladen**


Laden Sie eine Kopie des Pakets in das Format einer ZIP-Datei für die Offlineinstallation, für die Installation auf einem Server ohne Internetzugriff. Entzippen Sie das Paket nicht.

Z. B. das folgende Verfahren beschreibt jetzt, um die richtige Version von den [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) Paket von Bioconductor, vorausgesetzt, der Computer über Internetzugriff verfügt.

1.  Suchen Sie in der Liste der **Paketarchive** die **Windows-Binärdateiversion** .

2.  Mit der rechten Maustaste des Links, um die. ZIP-Datei, und wählen **Ziel speichern unter**.

3.  Navigieren Sie zu den lokalen Ordner, in dem komprimierten Pakete gespeichert sind, und klicken Sie auf **speichern**.

Dieser Vorgang erstellt eine lokale Kopie des Pakets. Sie können anschließend installieren Sie das Paket, oder kopieren das ZIP-Paket auf einen Server, die über keinen Zugriff auf das Internet.

Für Weitere Informationen zum Inhalt der Zip-Dateiformats und wie Sie ein R-Paket erstellen, empfehlen wir dieses Lernprogramm, das Sie im PDF-Format aus der R-Projektwebsite herunterladen können: [R-Pakete erstellen](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-installing-sql-server-machine-learning-features-on-an-azure-virtual-machinerinstalling-sql-server-r-services-on-an-azure-virtual-machinemd"></a>5. &nbsp;[Installieren von SQL Server-Machine learning-Features auf virtuellen Azure-Computer](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_4) | [Weiter](#TitleNum_6))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f4d287044b8bfda2dbe77fbf65b0d9cdd8f2ff42 2a8e33de6383f5d3af52256c5dfcb60184659eb8  (PR=4150  ,  Filename=installing-sql-server-r-services-on-an-azure-virtual-machine.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



6. Wenn Sie von einem remote Data Science-Client mit der Instanz herstellen möchten, führen Sie [zusätzliche Schritte--#additional-Schritte) nach Bedarf.

**Deaktivieren von Machine Learning-Features auf einer SQL Server-VM**


Sie können auch aktivieren oder deaktivieren Sie die Funktion auf einem vorhandenen SQL Server-virtuellen Computer zu einem beliebigen Zeitpunkt.

1. Öffnen Sie das Blatt für die virtuelle Maschine an.
2. Klicken Sie auf **Einstellungen**, und wählen Sie **SQL Server-Konfiguration** aus.
3. Nehmen Sie Änderungen an Funktionen, und wenden.

**<a name="existing"></a>Hinzufügen von R Services zu einer vorhandenen SQL Server 2016 Enterprise-VM**


Wenn Sie einen virtuellen Azure-Computer, der SQL Server ohne Machine learning-enthalten erstellt, können Sie die Funktion hinzufügen, durch die folgenden Schritte:

1. Erneut ausführen...! --SsNoVersion--NSCHLIEßEN-NotShown... /.. /Includes/ssnoversion-MD.MD)] einrichten, und fügen Sie das Feature für die **Serverkonfiguration** Seite des Assistenten.
2. Ausführung externer Skripts aktivieren und Starten der..! --SsNoVersion--NSCHLIEßEN-NotShown... /.. /Includes/ssnoversion-MD.MD)]-Instanz. Weitere Informationen finden Sie unter [Festlegen von SQL Server R Services –... /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Konfigurieren Sie bei Bedarf den Datenbankzugriff für R-Workerkonten für die remote Skriptausführung.
   Weitere Informationen finden Sie unter [Festlegen von SQL Server R Services –... /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Ändern Sie eine Firewallregel auf dem virtuellen Azure-Computer, wenn Sie beabsichtigen, die R-Skriptausführung von remoten Data Science-Clients zu ermöglichen. Weitere Informationen finden Sie unter [Aufheben der Sperre Firewall--#firewall).
4. Installieren oder Aktivieren von erforderlichen Netzwerkbibliotheken. Weitere Informationen finden Sie unter [Add Netzwerk Protokolle--#network).



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-install-pretrained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>6. &nbsp;[Installation pretrained Machine Learning-Modellen in SQL Server](r/install-pretrained-models-sql-server.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_5) | [Weiter](#TitleNum_7))

<!-- Source markdown line 96.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07b51584a90568cccceea382c44155e40e09c967 db083f8536fbb2ea5886fed787872867b5de5750  (PR=4150  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    For example, to enable use of the latest version of the pretrained models for Python, in a default instance of SQL Server 2017, you would run this statement:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    On a named instance, the command would be something like this:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Verwendung von Python pretrained Modelle mit Machine Learning-Server (eigenständig):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    Beispielsweise wenn eine Standardinstallation von Machine Learning-Server (eigenständig) 2017 von SQL Server-Setup, diese Anweisung ausführen:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Die folgenden Werte sind für den "Version"-Parameter unterstützt:



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-avoiding-errors-on-r-packages-installed-in-user-librariesrpackages-installed-in-user-librariesmd"></a>7. &nbsp;[Vermeiden von Fehlern in R-Paketen in benutzerbibliotheken installiert](r/packages-installed-in-user-libraries.md)

*Aktualisiert: 2017-10-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_6) | [Weiter](#TitleNum_8))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 52cb9a53d7d9c31ee9bc6977464ebd2a18081ff3 3537aa6755c66f12c19bb3448dc9b5c8abb9cc28  (PR=3619  ,  Filename=packages-installed-in-user-libraries.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=aecf422ca2289b2a417147eb402921bb8530d969) -->



Allerdings kann diese nie arbeiten, bei der Ausführung von R-Lösungen in SQL Server, da R-Pakete in einer spezifischen Bibliothek installiert werden müssen, die mit der Instanz verknüpft ist.

Wenn das Paket nicht in der Standardbibliothek installiert wurde, erhalten Sie möglicherweise diese Fehlermeldung, wenn Sie versuchen, das Paket aufzurufen:

*Fehler in library(xxx): ist kein Paket namens "Paketname"*

Es ist auch eine fehlerhafte Entwicklung Vorgehensweise zum Installieren der erforderlichen R-Pakete in einer benutzerdefinierten-Bibliothek, da es zu Fehlern führen kann, wenn eine Lösung von einem anderen Benutzer ausgeführt wird, die keinen Zugriff auf den BibliothekenSpeicherort.

**Gewusst wie: Installieren von R-Pakete in einer Bibliothek zugegriffen werden kann**


**Für SQLServer 2016**

Verwenden Sie die Paket-Bibliothek, die der Instanz zugeordnet. Weitere Informationen finden Sie unter [R-Paketen mit SQL Server--installing-and-managing-r-packages.md installiert)

**Für SQLServer 2017**

SQL Server bietet Funktionen, mit denen Sie mehrere Paketversionen verwalten und erteilen Benutzern die Berechtigung für einzelne Pakete, ohne dass der Benutzer mit Dateisystemzugriff haben.

Weitere Informationen zum Einrichten einer Bibliothek des Pakets für shared und Zuweisen von Benutzern zu Rollen finden Sie unter [SQL-Server--r-package-management-for-sql-server-r-services.md R paketverwaltung).




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-provision-a-virtual-machine-for-machine-learning-on-azurerprovision-the-r-server-only-sql-server-2016-enterprise-vm-on-azuremd"></a>8. &nbsp;[Bereitstellen eines virtuellen Computers für Machine Learning in Azure](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

*Aktualisiert: 2017-10-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_7) | [Weiter](#TitleNum_9))

<!-- Source markdown line 132.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 16439b4a8f5f4218edfcd746ed20ccbc8263dabc 1b3a8a7d1ceceaa459b3fd5640da26859df8d80b  (PR=3748  ,  Filename=provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=262e3cf5df2448bb6b532c0549c3d72daefe5a96) -->



|Name| Kommentare|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise unter Windows|R-Services integrierten erweiterten Analysen.|
|BYOL SQL Server 2016 SP1 Enterprise unter WindowsServer |R-Services integrierten erweiterten Analysen. |
|Kostenlose Lizenz: SQL Server 2016-SP1-Entwickler auf WindowsServer 2016 |R-Services integrierten erweiterten Analysen. |
| Data Science Virtual Machine - Windows 2012|Enthält die gängigen Tools für Data Science, einschließlich Microsoft R Server Developer Edition, SQL Server 2016 Developer Edition, Python Anaconda-Verteilung, Julia Pro Developer Edition und Jupyter Notebooks für r|
| Data Science Virtual Machine - Windows-2016|Enthält SQL Server 2016 Developer Edition mit Unterstützung für R-Analysen in der Datenbank an.|
|**SQL Server 2017**| ***   |
|SQL Server 2017 Enterprise, WindowsServer 2016| Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
|BYOL SQL Server 2017 Enterprise, WindowsServer 2016|Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
| Freien SQL Server-Lizenz: Entwickler SQL Server 2017 unter WindowsServer|Machine Learning-Dienste mit Unterstützung für Python und R-Sprache.|
| **Andere**| *** |
| Machine Learning-Server nur SQL Server 2017 Enterprise|Ähnlich wie in der SQL Server 2016 Enterprise-Image, aber die eigenständige Version des Machine Learning-Server und enthält den Kern ScaleR und Operationalisierung Funktionalität optimiert für Windows-Umgebungen.|
| Machine Learning-Server unter Windows|Enthält die eigenständige Version des Machine Learning-Servers mit operationalisierung-Funktionen, die für die Windows-Umgebung optimiert.|



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-revoscalerrrevoscaler-overviewmd"></a>9. &nbsp;["Revoscaler"](r/revoscaler-overview.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_8) | [Weiter](#TitleNum_10))

<!-- Source markdown line 18.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92f2dfa2e75037a932415881c55d2fd37fc6847a c6e9f17f2df82447b18beff41769ae3ebfbed562  (PR=4150  ,  Filename=revoscaler-overview.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->




"Revoscaler" ist ein Paket von Machine Learning, bereitgestellten Funktionen von Microsoft, die Data Science Größenordnungen unterstützt.

+ Funktionen unterstützen die Daten importieren, Datentransformation, Zusammenfassung, Visualisierung und Analyse.

+ _Die gatewaypooltopologie_ bedeutet, dass die Vorgänge können sehr großen Datasets können parallel ausgeführt und auf der verteilten-Dateisysteme. Algorithmen können über Datasets arbeiten, die nicht groß im Arbeitsspeicher, genug ist indem Sie die Aufteilung und vereiteln Ergebnisse, wenn Vorgänge abgeschlossen wurden.

+ "Revoscaler" bietet zahlreiche Verbesserungen gegenüber open Source-R-Funktionen. Es gibt viele der beliebtesten Basis R-Funktionen für "revoscaler"-Funktionen. RevoScaleR-Funktionen mit gekennzeichnet sind ein **Rx** oder **Rx** Präfix, das sie einfach identifizieren zu können.

+ "Revoscaler" dient als eine Plattform für die verteilte Data Science. Beispielsweise können Sie die "revoscaler" rechenkontexte und Transformationen mit dem Status der Art-Algorithmus in [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Sie können auch [RxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) Basis R-Funktionen parallel ausgeführt.

Beispiele von "revoscaler" in Aktion finden Sie in folgenden Blogs:

+ [Erstellen und Bereitstellen eines Vorhersagemodells mittels R und SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Vorhersagen von einer Million pro Sekunde mit Machine Learning-Server](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [Vorhersagen von Taxi Tipps MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [Leistungsoptimierung mit rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

**Gewusst wie: Abrufen von "revoscaler"**




&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-enable-or-disable-r-package-management-for-sql-serverrr-package-how-to-enable-or-disablemd"></a>10. &nbsp;[Aktivieren oder Deaktivieren der Verwaltung von R-Paket für SQL Server](r/r-package-how-to-enable-or-disable.md)

*Aktualisiert: 2017-11 bis 30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_9) | [Weiter](#TitleNum_11))

<!-- Source markdown line 60.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f846cd7d601459a95e694ada41e9fc5285f3de9 83a4a84adf47670c7fd4599f889f27ec3c219708  (PR=4150  ,  Filename=r-package-how-to-enable-or-disable.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    If you do not specify a user, the current security context is used.

3. Wiederholen Sie den Befehl für jede Datenbank, in dem Pakete installiert werden muss.

4.  Um sicherzustellen, dass die neuen Rollen erfolgreich erstellt wurden, klicken Sie in SQL Server Management Studio auf die Datenbank, erweitern Sie **Sicherheit**, und erweitern Sie **Datenbankrollen**.

    Sie können auch eine Abfrage auf Sys. database_principals, z. B. Folgendes ausführen:

```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,
        pr.authentication_type_desc, pe.state_desc,
        pe.permission_name, s.name + '.' + o.name AS ObjectName
    FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    JOIN sys.objects AS o
        ON pe.major_id = o.object_id
    JOIN sys.schemas AS s
        ON o.schema_id = s.schema_id;
```

4.  Nachdem die Funktion aktiviert wurde, kann jeder Benutzer mit den entsprechenden Berechtigungen verwenden die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) -Anweisung in T-SQL-Pakete hinzufügen. Ein Beispiel dafür, wie dies funktioniert, finden Sie unter [Installieren zusätzlicher Pakete unter SQL Server](r/install-additional-r-packages-on-sql-server.md).

**<a name="bkmk_disable"></a>Deaktivieren der paketverwaltung**




&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-set-up-a-data-science-client-for-use-with-sql-serverrset-up-a-data-science-clientmd"></a>11. &nbsp;[Einrichten einer Data Science-Client für die Verwendung mit SQL Server](r/set-up-a-data-science-client.md)

*Aktualisiert: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_10) | [Weiter](#TitleNum_12))

<!-- Source markdown line 52.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f674f5d329211e4c7d8dc464bd70f1cdef633350 8c65fc96c04f32d1e4777870774a11f9fd2ee219  (PR=3765  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



    For setup information, see [How to install R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

    To configure RTVS to use your Microsoft R client libraries, see [About Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio-2017

    Die kostenlose Community-Edition enthält die Data Science arbeitsauslastung aus, die Projektvorlagen für R, Python und f# installiert wird.

    Herunterladen von Visual Studio aus [Websiteansicht](https://www.visualstudio.com/vs/).

+ RStudio

    Wenn Sie RStudio verwenden möchten, sind einige zusätzliche Schritte erforderlich, um die RevoScaleR-Bibliotheken zu verwenden:

    - Installieren Sie Microsoft R-Client, um die erforderlichen Pakete und Bibliotheken zu erhalten.
    - Aktualisieren Sie Ihre R-Pfad zum Verwenden der Microsoft-R-Laufzeit.

    Weitere Informationen finden Sie unter [R-Client - konfigurieren die IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

**Konfigurieren der IDE**


+ R-Tools für Visual Studio

    Finden Sie unter [Websiteansicht](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) für einige Beispiele zum Erstellen und Debuggen von R mit R-Tools für Visual Studio-Projekte.

+ Visual Studio-2017

    Bei der Installation von Microsoft R Client- oder R **vor** Sie Visual Studio installieren, die R-Server-Bibliotheken automatisch erkannt und beim Bibliothekspfad verwendet. Wenn Sie die RevoScaleR-Bibliotheken aus nicht installiert haben die **R-Tools** klicken Sie im Menü **R-Client installieren**.

**Ausführen von R in SQLServer**


Dieses Beispiel verwendet Visual Studio 2017 Community Edition, mit der Data Science-Arbeitslast installiert.

1. Aus der **Datei** klicken Sie im Menü **neu** und wählen Sie dann **Projekt**.

2. Das - Handsymbol Bereich enthält eine Liste der vorinstallierten Vorlagen. Klicken Sie auf **R**, und wählen Sie **R Project**. In der **Namen** geben `dbtest` , und klicken Sie auf **OK**.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>12. &nbsp;[Einrichten von SQL Server Machine Learning-Services (Datenbankintern)](r/set-up-sql-server-r-services-in-database.md)

*Aktualisiert: 2017-11 – 16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_11) | [Weiter](#TitleNum_13))

<!-- Source markdown line 111.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4d355f6494b417dd90dce3943e7176eaece7336e 20bddb8ffd4cf3774b812a7376c70b95ccc57e92  (PR=3980  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



   + Datenbankmoduldienste
   + R Services (In-Database)

7. Wenn die Installation abgeschlossen ist, starten Sie den Computer neu.


**<a name="bkmk2017top"></a>Installieren von SQL Server 2017 Machine Learning-Services (Datenbankintern)**


> [!div class="checklist"]
> * Installieren von Datenbankmodul und Machine learning-Funktionen
> * Erforderliche Schritte nach der Installation: Aktivieren von Machine Learning und neu starten
> * Optionale Schritte der nach der Installation: Firewallregeln hinzufügen, fügen Sie Benutzer hinzu, ändern oder Konfigurieren von Dienstkonten, richten Sie eine remote Data Science-Client.

**Erste Schritte**

1. Führen Sie..! --SsNoVersion--NSCHLIEßEN-NotShown... /.. Setup für /Includes/ssnoversion-MD.MD)].

2. Auf der **Installation** Registerkarte **eigenständige neue SQL Server-Installation oder Hinzufügen von Funktionen zu einer vorhandenen Installation**.

     ! [Installieren Machine Learning-Dienste (In-Database)--media/2017setup-installation-page-mlsvcs.png "Starten der Installation des Datenbankmoduls mit Machine Learning-Dienste")

3. Auf der **Funktionsauswahl** Seite, wählen Sie die folgenden Optionen:

    + Wählen Sie **Datenbankmoduldienste**. Das Datenbankmodul ist in jeder Instanz erforderlich, die Machine Learning verwendet.

    + Wählen Sie **Machine Learning-Services (Datenbankintern)**. Diese Option installiert die Unterstützung für in der Datenbank mithilfe von r Nachdem Sie diese Option ausgewählt haben, können Sie Machine learning Sprache auswählen. Sie können nur R auswählen oder können Sie R und Python hinzufügen.

    ! [Machine Learning-Dienstfeature selection--media/2017setup-features-page-mls-rpy.png "Wählen Sie diese Funktionen für R Services In-Database")

    Wenn Sie nicht die R- oder Python Sprachoptionen auswählen, installiert der Setup-Assistent nur die Erweiterbarkeitsframework, die SQL Server vertrauenswürdige Launchpad enthält und sprachspezifische Komponenten nicht installiert.  Im Allgemeinen wird empfohlen, dass Sie mindestens eine Sprache zu installieren. Allerdings können Sie diese Option verwenden, wenn Sie beabsichtigen, das den Bindungsprozess sofort zu verwenden, um Machine learning-Komponenten zu aktualisieren. Weitere Informationen finden Sie unter [SqlBindR zum Aktualisieren einer Instanz des R-Services--use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md verwenden.)



&nbsp;

&nbsp;

---

<a name="TitleNum_13"/>

### <a name="13-nbsp-unattended-installation-of-machine-learning-services-in-databaserunattended-installs-of-sql-server-r-servicesmd"></a>13. &nbsp;[Für die unbeaufsichtigte Installation von Machine Learning-Services (Datenbankintern)](r/unattended-installs-of-sql-server-r-services.md)

*Aktualisiert: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_12) | [Weiter](#TitleNum_14))

<!-- Source markdown line 75.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ad203c90adff3f515b5f16472fad9753be7a421d 6925a9276bcd4a80babc7504de50400f1a5a2940  (PR=3765  ,  Filename=unattended-installs-of-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2017 Machine Services (Datenbankintern) mit der Python-Programmiersprache hinzugefügt installieren.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Beachten Sie die Flags für Python in SQL Server-2017 erforderlich:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

**Installieren von R und Python auf einer benannten Instanz**


Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2017 Machine Services (In-Database) installieren, auf einer benannten Instanz. R und Python-Sprachen werden hinzugefügt.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

**<a name="OldInstall"></a>Installation für SQL Server 2016 über die Befehlszeile**


Das folgende Beispiel zeigt, dass die Argumente erforderlich, um ein automatisches, unbeaufsichtigtes Ausführen von SQL Server 2016 installieren, mit der Sprache "R" hinzugefügt.



&nbsp;

&nbsp;

---

<a name="TitleNum_14"/>

### <a name="14-nbsp-step-3-explore-and-visualize-the-datatutorialssqldev-py3-explore-and-visualize-the-datamd"></a>14. &nbsp;[Schritt 3: Durchsuchen und Visualisieren von Daten](tutorials/sqldev-py3-explore-and-visualize-the-data.md)

*Aktualisiert: 30.11.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_13))

<!-- Source markdown line 66.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 47edcfbd8da7cf1ea1ad03a05f86d3cd26014827 674a7c7d0e8290fc91970ed2aeda3b97d5165d75  (PR=4150  ,  Filename=sqldev-py3-explore-and-visualize-the-data.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    Class 4: `tip_amount` > $20

**Erstellen von Darstellungen, die mithilfe von Python in T-SQL**


Das Entwickeln einer Data Science-Lösung bringt normalerweise die intensive Untersuchung und Visualisierung von Daten mit sich. Da Visualisierung ein leistungsstarkes Tool für die Verteilung der Daten und Ausreißer ist, stellt Python viele Pakete für die visuelle Darstellung der Daten bereit. Die **Matplotlib** Modul ist eine der gängigeren Bibliotheken für Visualisierung und beinhaltet zahlreiche Funktionen zum Erstellen von Histogrammen, Punktdiagrammen Feld Zeichnungen und andere Daten zum Durchsuchen von Diagrammen.

In diesem Abschnitt erfahren Sie, wie zur Bearbeitung der Darstellungen, die mithilfe von gespeicherten Prozeduren. Stattdessen als das Abbild auf dem Server zu öffnen, speichern Sie die Python-Objekt `plot` als **Varbinary** Daten, und klicken Sie dann schreiben, dass in einer Datei, kann freigegeben oder an anderer Stelle angezeigt.

**Erstellen Sie eine grafische Ausgabe als Varbinary-Daten**


Die **Revoscalepy** Lieferumfang von SQL Server 2017 Machine Learning-Services-Modul unterstützt Funktionen ähnlich denen in der **"revoscaler"** -Paket für R.  Dieses Beispiel verwendet die Python-Entsprechung des `rxHistogram` , zeichnen ein Histogramm, das basierend auf Daten aus einer..! --Tsql--NSCHLIEßEN-NotShown... /.. /Includes/TSQL-MD.MD)]-Abfrage.

Die gespeicherte Prozedur gibt eine serialisierten Python `figure` Objekt als Datenstrom von **Varbinary** Daten. Sie können die Binärdaten direkt, sondern Sie können mithilfe von Python-Code auf dem Client zum Deserialisieren und die Zahlen anzeigen und speichern Sie die Bilddatei auf einem Clientcomputer.

1. Erstellen Sie die gespeicherte Prozedur _SerializePlots_, wenn das PowerShell-Skript nicht bereits geschehen ist.

    - Die Variable `@query` definiert den Abfragetext `SELECT tipped FROM nyctaxi_sample`, die an die Python-Code-Block übergeben wird, als Argument für das Skript Eingabevariable `@input_data_1`.
    - Python-Skript ist recht einfach: **Matplotlib** `figure` Objekte werden verwendet, um die Zeichnung Histogramm und Punktdiagrammen vornehmen und diese Objekte werden dann mit serialisiert die `pickle` Bibliothek.







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu + Aktualisiert (3+14): Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (1+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (1+0): Analysis Services für SQL-Dokumente)](../analysis-services/new-updated-analysis-services.md)
- [Neu + Aktualisiert (87+0): Dokumente zu **Analyseplattformsystem für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu + Aktualisiert (5+4): Dokumente zu **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu + Aktualisiert (0+1): Dokumente zum **Datenbankmodul für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu + Aktualisiert (2+2):Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu + Aktualisiert (10+9): Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu + Aktualisiert (2+4): Dokumente zu **Relationale Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu + Aktualisiert (4+2): Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu + Aktualisiert (0+1): Dokumente zu **Beispiele für SQL**](../sample/new-updated-sample.md)
- [Neu + Aktualisiert (21+0): Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu + Aktualisiert (5+1): Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1): **SQL Server Data Tools (SSDT)** docs (Neu + Aktualisiert (0+1): SQL Server Data Tools-Dokumente (SSDT))](../ssdt/new-updated-ssdt.md)
- [Neu + Aktualisiert (1+0): Dokumente zu **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [New + Updated (0+1): **SQL Server Management Studio (SSMS)** docs (Neu + Aktualisiert (0+1): SQL Server Management Studio-Dokumente (SSMS))](../ssms/new-updated-ssms.md)
- [Neu + Aktualisiert (0+2): Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)


