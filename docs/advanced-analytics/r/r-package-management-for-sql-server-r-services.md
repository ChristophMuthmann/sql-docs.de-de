---
title: "R-paketverwaltung für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5cd3924b79ce5d33adf88bb6c7c267cdc43a3418
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/01/2017
---
# <a name="r-package-management-for-sql-server"></a>R-paketverwaltung für SQL Server

Dieser Artikel beschreibt die Funktionen für die Verwaltung von R-Paketen in SQL Server-2017 und SQL Server 2016.

+ Änderungen in Methoden zur Installation von R-Paket zwischen 2016 und 2017
+ Empfohlene Methoden zum Verwalten von R-Pakete
+ Neue Datenbankrollen für die paketverwaltung in SQL Server-2017
+ Neue T-SQL-Anweisung für die paketverwaltung in SQL Server-2017

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>Unterschiede bei der paketverwaltung zwischen SQL Server 2016 und SQL Server-2017

In **SQL Server-2017**, paketverwaltung auf Instanzebene zu aktivieren und Verwalten von Benutzerberechtigungen zum Hinzufügen oder verwenden Pakete auf Datenbankebene.

Dies erfordert, dass der Datenbankadministrator die Paket-Management-Funktion aktivieren, durch Ausführen eines Skripts, das die erforderlichen Datenbankobjekte erstellt. Weitere Informationen finden Sie unter [zum Aktivieren der R-paketverwaltung](r-package-how-to-enable-or-disable.md).

In **SQL Server 2016**, muss ein Administrator R-Pakete installieren, in der R-Bibliothek, die der Instanz zugeordnet. Diese Pakete verwenden alle Benutzer, die R-Code in der Instanz ausgeführt wird. R-Code, die in SQLServer ausgeführt wird, kann nicht im benutzerbibliotheken installierten Pakete verwenden. Allerdings kann der Administrator einzelne Benutzer die Fähigkeit zur Ausführung von R-Skripts in einer bestimmten Datenbank gewähren.

**Zusammenfassung der Unterschiede und Vorteile**

+ Bei Verwendung von Machine Learning Services in SQL Server-2017 können Sie verwalten und Installieren von R-Pakete, die entweder zur herkömmliche Methode, die basierend auf R-Tools oder mit dem neuen Datenbankrollen und die T-SQL-Anweisungen.

+ Es wird empfohlen, dass die zweite Methode, da es sich um eine präzisere Kontrolle von Administratoren, bietet mit mehr Freiheit für Benutzer gekoppelt. Angenommen, Benutzer können Installationspakete ihre eigenen, entweder mithilfe einer gespeicherten Prozedur oder durch R-Code und Freigabe von Paketen mit anderen. 

    Da Pakete in einer Datenbank festgelegt werden können, und jeder Benutzer eine isolierte Paket Sandkasten erhält, ist es einfacher, verschiedene Versionen der gleichen R-Paket installieren. Sie können auch einfach kopieren oder Verschieben von Benutzern und ihren Paketen zwischen Datenbanken. 

+ Die Verwendung der Paket-Management-Funktion in SQL Server kann die sicherungs-und Wiederherstellungsvorgänge viel einfacher. Wenn Sie Ihre Datenbank zu einem neuen Server migrieren, können Sie die Paket-Synchronisierung-Funktion verwenden, liest eine Liste mit allen Paketen und in einer Datenbank auf dem neuen Server installieren.

+ Sie finden es vielleicht einfacher zum Installieren von R-Pakete als Administrator auf dem Computer mit herkömmlichen R-Tools, wenn Sie die einzige Person, die mithilfe des Servers für Machine Learning-Aufträge sind.

+ Bei Verwendung von SQL Server 2016 R Services sollten Sie zum Installieren von R-Pakete, die von der Instanz, die mithilfe von R-Tools verwendet weiterhin > Achten Sie darauf, die der Instanz zugeordnete R-Bibliothek verwenden.

Die folgenden Abschnitte enthalten weitere Details dazu, wie paketverwaltung mit diesen beiden Optionen ausgeführt.

## <a name="r-package-management-using-t-sql"></a>R-paketverwaltung mit T-SQL

SQL Server-2017 umfasst neue T-SQL-Anweisungen, die der DBA mehr Kontrolle über die R-Pakete auf Datenbankebene erteilen. Zur gleichen Zeit kann der Datenbankadministrator Benutzern die Möglichkeit zum Installieren der Pakete benötigten und andere Benutzer freizugeben.

Wenn Sie Pakete für andere Benutzer freigeben möchten, oder wenn mehrere Personen Machine Learning-Aufträge auf dem Server ausführen müssen, sollten Sie paketverwaltung aktivieren, Zuweisen von Benutzern zu Datenbankrollen und uploadpakete, damit Benutzer freigegeben werden können.

Verwalten von Paketen in SQL Server-2017 stützt sich auf diese neue Datenbankobjekte und Funktionen:

+ Neue Datenbankrollen für die Verwaltung von Paketzugriff und Verwendung
+ Paketbereich separaten freigegebenen und privaten Pakete
+ Erstellen EXTERNEN LIBRARY-Anweisung für das Hochladen von neuen Codebibliotheken mit dem server
+ Neue R-Funktionen im "revoscaler" zur Unterstützung der Installation von Paketen in einer SQL Server-computekontext
+ Paketsynchronisierung, um sicherzustellen, dass seine sichern und Wiederherstellen von Paketen

### <a name="database-roles-for-package-management"></a>Datenbankrollen für die Paketverwaltung

Der Datenbankadministrator muss die Rollen, die für die paketverwaltung verwendet werden, mithilfe eines Skripts beschriebenen hier erstellen: [aktivieren oder Deaktivieren der paketverwaltung](r-package-how-to-enable-or-disable.md).

Nachdem Sie dieses Skript ausgeführt haben, sehen Sie die folgenden neuen Datenbankrollen:

+ `rpkgs-users`: Mitglieder dieser Rolle können alle freigegebenen Pakete, die von einem anderen installiert wurde `rpkgs-shared` Mitglied der Rolle.

+ `rpkgs-private`: Mitglieder dieser Rolle haben Zugriff auf freigegebene Pakete, mit den gleichen Berechtigungen als Mitglieder der `rpkgs-users` Rolle. Mitglieder dieser Rolle können auch installieren, entfernen und privat Bereichsbezogene Pakete verwenden.

+ `rpkgs-shared`: Mitglieder dieser Rolle haben die gleichen Berechtigungen als Mitglieder der `rpkgs-private` Rolle. Darüber hinaus können Mitglieder dieser Rolle installieren oder Entfernen von freigegebenen Paketen.

+ `db_owner`: Mitglieder dieser Rolle haben die gleichen Berechtigungen als Mitglieder der `rpkgs-shared` Rolle. Darüber hinaus Mitglieder dieser Rolle können **gewähren** anderen Benutzern das Recht zum Installieren oder Entfernen von beiden gemeinsam genutzt und privater Pakete.

Der Datenbankadministrator Hinzufügen von Benutzern für die Rollen auf der Grundlage einer pro Datenbank zum Steuern der Möglichkeit des Benutzers, um Pakete zu installieren.

### <a name="package-scope"></a>Paketbereich

Neue Features für das Paket zu Pakete unterscheiden, ob diese privat sind, oder von mehreren Benutzern gemeinsam genutzt werden können.

+ **Freigegebener Bereich**

    *Freigegebener Bereich* bedeutet, dass dieser Benutzer, die Berechtigung mit der gemeinsam genutzten Bereich angegeben wurden (`rpkgs-shared`) installieren und Deinstallieren von Paketen mit einer angegebenen Datenbank können. Ein Paket, das in einer Bibliothek des freigegebenen Bereichs installiert wurde, kann von anderen Benutzern der Datenbank auf SQL Server verwendet werden, sofern diesen Benutzern die Verwendung der installierten R-Pakete erlaubt ist.

+ **Privater Bereich**

    *Private Bereich* bedeutet, dass dieser Benutzer, die Mitgliedschaft in der privaten Bereich-Rolle zugewiesen wurde (`rpkgs-private`) installieren oder Deinstallieren von Paketen in einem privaten Speicherort pro Benutzer definierte können. Daher können alle Pakete, die im privaten Bereich installiert wurden, nur von dem Benutzer verwendet werden, der sie installiert hat. Anders gesagt kann ein Benutzer von SQL Server keine privaten Pakete verwenden, die von einem anderen Benutzer installiert wurden.

Diese Modelle für den *freigegebenen* und den *privaten* Bereich können kombiniert werden, um benutzerdefinierte Sicherheitssysteme zum Bereitstellen und Verwalten von Paketen auf SQL Server zu entwickeln.

Beispielsweise kann dem Leiter oder Manager einer Gruppe von Datenwissenschaftlern die Berechtigung zum Installieren von Paketen erteilt werden, und diese Pakete können dann von allen anderen Benutzern oder Datenwissenschaftlern in der gleichen SQL Server-Instanz verwendet werden.

Für ein anderes Szenario ist möglicherweise eine stärkere Abgrenzung der Benutzer untereinander oder eine andere Verwendung von Paketen erforderlich. In einem solchen Fall kann der private Bereich verwendet werden, um Datenwissenschaftlern Einzelberechtigungen zu erteilen, die nur für das Installieren und Verwenden der von ihnen benötigten Pakete verantwortlich sind. Da Pakete auf Benutzerbasis installiert werden, wirken sich die von einem Benutzer installierten Pakete nicht auf die Arbeit anderer Benutzer aus, die die gleiche SQL Server-Datenbank verwenden.

### <a name="create-external-library"></a>EXTERNE BIBLIOTHEK ERSTELLEN

Die [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) ist eine neue T-SQL-Anweisung in SQL Server-2017 um den Datenbankadministrator mit Paketen arbeiten, ohne R-Benutzertools unterstützen eingeführt. 

Verwenden Sie die **externe Bibliothek erstellen** Anweisung zum Hochladen von externer Bibliotheken in eine Instanz im ZIP-Datei-Format. Autorisierte Benutzer können dann Zugriff auf die Bibliotheken und installieren sie zur eigenen Nutzung verwenden.

Beispielsweise konnten Sie mehrere Kopien des R-Projekts, jeweils für eine andere Version erstellen. Diese als separate Bibliotheken hochladen, können Sie einige Versionen privat zu halten und einige Versionen für andere Benutzer freigeben.

Eine "Library" ist im Grunde eine Auflistung von externen Pakete, die Sie für Benutzer unter einem einzigen Namen verfügbar machen möchten. Zum Beispiel könnten Sie keines der folgenden mit SQL Server als eine externe Bibliothek veröffentlichen:

+ Eine einzelne R-Paket, das Sie, das ohne Abhängigkeiten geschrieben haben
+ Ein Paket, das Sie installieren möchten, und für die Installation erforderlichen Abhängigkeiten
+ Eine Auflistung von R-Pakete, die im Zusammenhang mit der einen bestimmten Task oder ein Projekt, mit deren Abhängigkeiten

Der Bibliotheksname ist zum Verwalten der das Paket oder eine Auflistung von Paketen in SQL Server und kann unabhängig von den Paketen, die installiert werden. Bibliotheksnamen müssen jedoch in einer Instanz eindeutig sein.

Um diese Anweisung verwenden, muss die Paket-Verwaltungsfunktion für die Instanz aktiviert worden sein. Weitere Informationen finden Sie unter [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

> [!NOTE]
> Mit dieser Anweisung können Sie derzeit um nur auf Windows basierenden Bibliotheken zu erstellen, für die Unterstützung für r geplante wird in Zukunft für Python-Pakete und für Pakete, die auf anderen Plattformen wie Linux ausgeführt.

Nachdem Sie die externe Bibliothek an den Server hochgeladen wurde, müssen Sie es der R-Paket-Bibliothek, die der Instanz zugeordneten installieren. Es gibt mehrere Möglichkeiten:

+ Führen Sie den Standardbefehl R `install.packages` in Sp_execute_external_script. Achten Sie darauf, dass Sie eine Verbindung über ein Konto mit Berechtigungen zum Installieren der Pakete.

+ Verbinden mit SQL Server von einem Remoteclient von R, und führen Sie [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) in der SQL Server-computekontext. Berechtigungen zum Installieren von Paketen müssen Sie erneut, entweder in private oder freigegebene Bereich dazu verfügen.

Beispiele für die Installation mittels R und T-SQL finden Sie unter [Installieren zusätzlicher Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md).

### <a name="new-r-functions-for-package-installation"></a>Neue R-Funktionen für die Paketinstallation

Nach dem Datenbankrollen für die paketverwaltung aktiviert wurden, Benutzer können auch neuer Funktionen in [ **"revoscaler"** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) zum Installieren von Paketen für die Instanz, die als SQL Server-computekontext angegeben.

+ Der Data Scientist kann erforderlichen R-Pakete auf SQL Server installieren, ohne direkten Zugriff auf die SQL Server-Computer.

+ Ein Benutzer kann ein Paket installieren und freigeben, durch die Installation des Pakets mit freigegebenen Bereich. Andere autorisierte Benutzer die gleiche SQL Server-Datenbank können Sie dann das Paket zugreifen.

+ Benutzer können privater Pakete, die für andere, nicht sichtbar sind installieren und einen privaten Sandkastens für R-Pakete erstellen.

Die folgenden Paketverwaltungsfunktionen werden in "revoscaler", für die Installation und Deinstallation von Paketen in einen angegebenen computekontext bereitgestellt:

-   [RxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): erfahren Sie mehr über Pakete, die in der angegebenen computekontext installiert.

-   [RxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): Installieren von Paketen in einer computekontext, aus einem angegebenen Repository oder durch Lesen, lokal gespeichert, die ZIP-Paketen.

-   [RxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): installierte Pakete über einen computekontext entfernen.

-   [RxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): Rufen Sie den Pfad für ein oder mehrere Pakete in der angegebenen computekontext.

-   [RxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): eine Bibliothek Paket zwischen dem Dateisystem und Datenbanken in der angegebenen rechenkontexte kopiert.

-   [RxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): den Suchpfad für die Bibliothek Strukturen für Pakete während der Ausführung in der SQL-Server abrufen.

Verbinden Sie für die Verwendung dieser Funktionen mit einer Instanz von SQL Server, auf dem Sie die erforderlichen Berechtigungen mithilfe einen SQL Server-computekontext. Wenn Sie eine Verbindung herstellen, bestimmen Ihre Anmeldeinformationen an, ob der Vorgang auf dem Server abgeschlossen werden kann.

Die Funktionen zur Paketinstallation prüfen Abhängigkeiten und stellen sicher, dass alle zugehörigen Pakete in SQL Server installiert werden können, gerade wie bei der Installation von R-Paketen im lokalen Rechenkontext. Die Funktion, die Pakete deinstalliert, berechnet ebenfalls Abhängigkeiten und stellt sicher, dass Pakete, die nicht mehr von anderen Paketen in SQL Server verwendet werden, entfernt werden, um Ressourcen freizugeben.

> [!NOTE]
> 
> Diese neuen Funktionen sind in SQL Server-2017 standardmäßig enthalten. Sie können Ihre Version von "revoscaler" abzurufenden dieser Funktionen durch ein Upgrade der Instanz für eine höhere Version von Microsoft R Server, z. B. Microsoft R Server 9.0.1 aktualisieren.
> 
> Weitere Informationen finden Sie unter [verwenden SqlBindR.exe auf UpgradeR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="synchronization-of-r-package-libraries"></a>Synchronisierung von R-Paket-Bibliotheken

Die CTP-Version 2.0-Version von SQL Server-2017 (und der Version April 2017 von Microsoft R Server) enthält neue R-Funktionen für *synchronisieren Pakete*.

Paket synchronisieren bedeutet, dass das Datenbankmodul die Pakete, die von einem bestimmten Besitzer und die Gruppe verwendet werden nachverfolgt, und können diese Pakete in das Dateisystem schreiben, bei Bedarf. Paketsynchronisierung können in diesen Szenarien:

+ R-Pakete zwischen Instanzen von SQL Server verschoben werden sollen.
+ Sie müssen zum Installieren der Pakete für einen bestimmten Benutzer oder eine Gruppe, nachdem eine Datenbank wiederhergestellt wird.

Weitere Informationen zum Aktivieren und verwenden Sie dieses Feature finden Sie unter [R-Paket-Synchronisierung für SQL Server](package-install-uninstall-and-sync.md).

## <a name="r-package-management-using-traditional-r-tools"></a>R-paketverwaltung mit herkömmlichen R-tools

Die herkömmliche Methode zur Verwaltung von R-Pakete auf einer Instanz ist zum Installieren und die Liste der Pakete mithilfe von R-Tools und Befehle. 

+ Diese Option möglicherweise die einzige Option, wenn Sie eine frühe Version von SQL Server 2016 verwenden.  
+ Diese Option kann auch einfacher wird, wenn Sie der einzige Benutzer der R-Pakete und verfügen über Administratorzugriff auf den Server.
+ Verwalten von Versionen der R-Paket zu vereinfachen, können Sie [MiniCRAN](create-a-local-package-repository-using-minicran.md) zu erstellen, ein lokales Repository, die zwischen Instanzen freigeben.

Einzelheiten finden Sie in folgenden Artikeln:

+ [Installieren Sie zusätzliche R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Ermitteln der auf SQL Server installierten Pakete](determine-which-packages-are-installed-on-sql-server.md)

Für SQL Server-2017, wir empfehlen die Verwendung von EXTERNEN Bibliothek erstellen und die Datenbankrollen zum Verwalten von Benutzern und ihre R-Pakete enthält.

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren oder Deaktivieren der R-Paket-Verwaltung](../r/r-package-how-to-enable-or-disable.md)
