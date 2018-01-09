---
title: "R-paketverwaltung für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 576178e53a28f877ac91d99f14ce9ba6a44e506d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="r-package-management-for-sql-server"></a>R-paketverwaltung für SQL Server

Dieser Artikel beschreibt die Funktionen für die Verwaltung von R-Paketen in SQL Server-2017 und SQL Server 2016.

+ Empfohlene Methoden zum Verwalten von R-Paketen (und Python-Pakete)
+ Änderungen bei der paketverwaltung zwischen SQL Server 2016 und 2017

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="recommended-methods-for-package-management"></a>Empfohlene Methoden zum Verwalten von Paketen

In SQL Server 2016 und SQL Server-2017 kann ein Computeradministrator Pakete für jede Instanz installieren, auf dem Computer Learning aktiviert wurde. 

Pakete werden in das Dateisystem, mit der Instanz-Bibliotheken, installiert und nicht von Instanzen gemeinsam genutzt werden. Dies ist derzeit die empfohlene Methode für SQL Server 2016 und SQL Server-2017.

+ [Installieren Sie zusätzliche R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md)
+ [Ermitteln der auf SQL Server installierten Pakete](determine-which-packages-are-installed-on-sql-server.md)

Darüber hinaus haben **Dbo** Rollenmitgliedschaft auf einer Instanz von SQL Server, auf dem Computer Learning aktiviert wurde, können Sie R-Pakete von einem Remoteclient aus installieren, indem Sie die Verwendung neuer Funktionen in "revoscaler".

+ [Neue R-Funktionen für die Paketinstallation](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>Installation auf Servern ohne Internetzugang

Damit sie einfacher Bestimmen der erforderlichen Versionen der R-Paket, und geben Sie alle Abhängigkeiten Verpacken, können Sie [MiniCRAN](https://mran.microsoft.com/package/miniCRAN). Diese R-Paket kann eine Liste der Ziel-Pakete und erstellt ein lokales Repository, das die Ziel-Pakete sowie alle zugehörigen Abhängigkeiten im ZIP-Format enthält. Sie können anschließend kopieren, die auf dem Offlineserver oder das Repository zwischen mehreren Instanzen freigeben.

Weitere Informationen finden Sie unter [erstellen Sie ein lokales Paket-Repository mit MiniCRAN](create-a-local-package-repository-using-minicran.md).

### <a name="python-packages"></a>Python-Pakete

Installation des neuen Python-Pakete folgt dieselben Richtlinien: 

+ Überprüfen Sie die Python-Pakete im voraus, um Kompatibilität mit der aktuellen Python-Version zu bestimmen
+ Bewerten von Python-Paket Eignung für einen festgeschriebene SQL Server-Umgebung
+ Verwenden Sie Python-Tools, um Pakete als Administrator installieren
+ Installieren von Paketen, die in der SQL Server-Kontext nur in der Bibliothek für die Instanz ausgeführt werden müssen. 
+ Wenn Sie mehrere Umgebungen für Tests verwenden, Produktion usw., stellen Sie sicher, dass die gleiche Version von Python-Paket in der Bibliothek für die Instanz installiert ist.

Installationsschritte finden Sie unter [Installieren neuer Python-Pakete unter SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>Funktionen zum Verwalten von Paketen in SQL Server 2016 und SQL Server-2017

SQL Server-2017 hinzugefügt einige neuen Funktionen zur Unterstützung von vereinfacht die Verwaltung von R (und Python)-Paketen von Datenbankadministratoren. Zu diesen neuen Funktionen gehören:

+ Die Möglichkeit zum Installieren oder Verwalten von Paket-Bibliotheken, die mithilfe von T-SQL
+ Verwaltung von Berechtigungen auf Datenbankebene über die Datenbankrollen. 

In zukünftigen Versionen werden diese Features bieten die primäre Methode zum paketverwaltung von Datenbankadministratoren und Datenanalysten Installation die Laufzeitbibliotheken benötigten erleichtern erwartet.

Am hinzugefügt zur gleichen Zeit Microsoft R Server und Machine Learning-Server neue R-Funktionen zu installieren und Freigeben von Paketen in einer SQL Server-computekontext zu vereinfachen. Diese Funktionen ausgeführt werden, unabhängig von der SQL Server-Funktionen, die anhand der T-SQL und von einem Remoteclient von R ausgeführt werden sollen.

Dieser Abschnitt enthält einen Überblick über diese Funktionen.

### <a name="bkmk_remoteInstall"></a>Neue RevoScaleR-Funktionen für die Paketinstallation 

Benutzer mit eine aktuelle Version von R-Server "oder" Machine Learning-Server können auch neue Funktionen in [ **"revoscaler"** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) zum Installieren von Paketen auf einer Instanz, die als SQL Server-computekontext angegeben.

+ Der Data Scientist kann erforderlichen R-Pakete auf SQL Server installieren, ohne direkten Zugriff auf die SQL Server-Computer. Allerdings muss der Benutzer ein Mitglied der Datenbankbesitzer (**Dbo**) Rolle.

+ Die Benutzer kann Pakete mit anderen, freigeben, indem Installieren von Paketen mit freigegebenen Bereich. Andere autorisierte Benutzer die gleiche SQL Server-Datenbank können das Paket zugreifen.

+ Benutzer können privater Pakete, die für andere, nicht sichtbar sind installieren und einen privaten Sandkastens für R-Pakete erstellen.

+ Paketsynchronisierung kann mühelos sichern und Wiederherstellen von Paketen

#### <a name="package-installation-functions"></a>Funktionen der Paket-installation

Die folgenden Paketverwaltungsfunktionen werden in "revoscaler", für die Installation und Deinstallation von Paketen in einen angegebenen computekontext bereitgestellt:

-   [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): erfahren Sie mehr über Pakete, die in der angegebenen computekontext installiert.

-   [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): Installieren von Paketen in einer computekontext, aus einem angegebenen Repository oder durch Lesen, lokal gespeichert, die ZIP-Paketen.

-   [RxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): installierte Pakete über einen computekontext entfernen.

-   [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): Rufen Sie den Pfad für ein oder mehrere Pakete in der angegebenen computekontext.

-   [RxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): eine Bibliothek Paket zwischen dem Dateisystem und Datenbanken in der angegebenen rechenkontexte kopiert.

-   [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): den Suchpfad für die Bibliothek Strukturen für Pakete während der Ausführung in der SQL-Server abrufen.

Verbinden Sie für die Verwendung dieser Funktionen mit einer Instanz von SQL Server, auf dem Sie die erforderlichen Berechtigungen mithilfe einen SQL Server-computekontext. 

> [!IMPORTANT]
> Die in der Verbindung verwendeten Anmeldeinformationen bestimmen, ob der Vorgang auf dem Server abgeschlossen werden kann.

Diese Funktionen der Paket-Installation Abhängigkeiten überprüfen und sicherstellen, dass alle zugehörigen Pakete zu SQL Server, wie durch die Installation von R-Paket im lokalen rechenkontext installiert werden können. Die Funktion, die Pakete deinstalliert, berechnet ebenfalls Abhängigkeiten und stellt sicher, dass Pakete, die nicht mehr von anderen Paketen in SQL Server verwendet werden, entfernt werden, um Ressourcen freizugeben.

Diese neuen Funktionen sind in der Version von "revoscaler" enthalten, die in SQL Server-2017 installiert ist. Sie können diese Funktionen auch abrufen, indem [Aktualisieren von SQL Server-Instanz](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) verwenden Sie eine aktuelle Version von [Microsoft R Server oder Computer Learning](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server). Erfordert Version 9.0.1 oder höher.

#### <a name="package-synchronization-functions"></a>Paket-Synchronisierungsfunktionen

Paketsynchronisierung ist ein neues Feature für nur die R-Pakete. Das Datenbankmodul verfolgt die Pakete, die von einem bestimmten Besitzer und die Gruppe verwendet werden, und können diese Pakete in das Dateisystem schreiben, bei Bedarf. In der Regel verwenden Sie die paketsynchronisierung in diesen Szenarien:

+ R-Pakete zwischen Instanzen von SQL Server verschoben werden sollen.
+ Sie müssen zum Installieren der Pakete für einen bestimmten Benutzer oder eine Gruppe, nachdem eine Datenbank wiederhergestellt wird.

Weitere Informationen zum Aktivieren und verwenden Sie dieses Feature finden Sie unter [R-Paket-Synchronisierung für SQL Server](package-install-uninstall-and-sync.md).

### <a name="package-management-using-t-sql"></a>Verwalten von Paketen mithilfe des T-SQL

SQL Server-2017 hinzugefügt neue T-SQL-Anweisungen aus, um der DBA mehr Kontrolle über die R-Pakete auf Datenbankebene erteilen. Der Datenbankadministrator sollte keine Informationen zum Verwenden von R oder Python-Tools, aber stattdessen sollte der Lage R oder Python-Benutzer bieten die Möglichkeit zum Installieren der Pakete benötigten und andere Benutzer freizugeben.

Diese Funktion dient, Zusammenarbeit und versionsverwaltung in mehrbenutzerumgebungen vereinfachen: z. B.:

+ Möchten Sie die Pakete freigeben, die Sie für andere Personen in Ihrem Team entwickelt haben.
+ Mehrere Analysten in der gleichen Datenbank arbeiten, und unterschiedliche Versionen des gleichen Pakets verwenden müssen.
+ Pakete und deren Berechtigungen zur gleichen Zeit zu verschieben, die Sie beim Ausführen der Sicherung und Wiederherstellung eine Datenbank oder verschieben möchten.

Verwalten von Paketen in SQL Server-2017 stützt sich auf diese neue Datenbankobjekte und Funktionen:

+ [Neue Datenbankrollen](#bkmk_roles), für die Verwaltung von Packen Zugriff sowie die Verwendung
+ [Erstellen eines EXTERNEN Bibliothek](#bkmk_createExternalLibrary) Anweisung für den Upload von Paket-Bibliotheken mit dem Server

Verwendung dieser Funktionen erfordert einige zusätzliche Vorbereitung auf die Instanz- und Datenbankebene: 

+  Der Datenbankadministrator muss die Paket-Verwaltungsfunktion explizit aktivieren, durch Ausführen eines Skripts, das die erforderlichen Datenbankobjekte erstellt. Weitere Informationen finden Sie unter [zum Aktivieren der R-paketverwaltung](r-package-how-to-enable-or-disable.md).

+ Benutzer müssen Rollen, die auf einer Ebene pro Datenbank zugewiesen werden. Diese Rollen bieten Benutzern die Möglichkeit, freigegeben oder privat Pakete installieren.

+ Paket-Bibliotheken können installiert werden, mit der neuen T-SQL-Anweisung, externe Bibliothek erstellen. Allerdings müssen alle paketabhängigkeiten im Voraus vorbereitet und als Teil einer einzelnen ZIP-Datei installiert werden.

> [!NOTE]
> Obwohl die hier beschriebenen Funktionen zu diesem Zeitpunkt voll funktionsfähig sind, enthalten zukünftige Versionen zusätzliche Verbesserungen, sodass es einfacher Paket Bibliotheken vorbereitet und zum Verwalten der Abhängigkeiten, an. Wenn Sie mit der Installation von R-Paket vertraut sind, wird empfohlen, dass Sie weiterhin die R-Tools für jetzt verwenden.

#### <a name="bkmk_createExternalLibrary"></a>EXTERNE BIBLIOTHEK ERSTELLEN 

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

Um sicherzustellen, dass alle paketabhängigkeiten angegeben werden, es wird empfohlen, [MiniCRAN](create-a-local-package-repository-using-minicran.md) um ein lokales Repository zu erstellen. Diese ZIP-Datei können dann um das Zielpaket und seine Abhängigkeiten zu installieren.

#### <a name="bkmk_roles"></a>Datenbankrollen für paketverwaltung 

Die neuen Rollen, die im SQL Server für paketverwaltung bereitgestellt sind nicht standardmäßig auch in Instanzen enthalten, wobei Machine Learning installiert und aktiviert wurde. Sie müssen die Rollen hinzufügen, durch Ausführen eines Skripts, wie beschrieben hier: [aktivieren oder Deaktivieren der paketverwaltung](r-package-how-to-enable-or-disable.md).

Nachdem Sie dieses Skript ausgeführt haben, sehen Sie die folgenden neuen Datenbankrollen:

+ `rpkgs-users`: Mitglieder dieser Rolle können alle freigegebenen Pakete, die von einem anderen installiert wurde `rpkgs-shared` Mitglied der Rolle.

+ `rpkgs-private`: Mitglieder dieser Rolle haben Zugriff auf freigegebene Pakete, mit den gleichen Berechtigungen als Mitglieder der `rpkgs-users` Rolle. Mitglieder dieser Rolle können auch installieren, entfernen und privat Bereichsbezogene Pakete verwenden.

+ `rpkgs-shared`: Mitglieder dieser Rolle haben die gleichen Berechtigungen als Mitglieder der `rpkgs-private` Rolle. Darüber hinaus können Mitglieder dieser Rolle installieren oder Entfernen von freigegebenen Paketen.

+ `db_owner`: Mitglieder dieser Rolle haben die gleichen Berechtigungen als Mitglieder der `rpkgs-shared` Rolle. Darüber hinaus Mitglieder dieser Rolle können **gewähren** anderen Benutzern das Recht zum Installieren oder Entfernen von beiden gemeinsam genutzt und privater Pakete.

Der Datenbankadministrator kann Benutzer zu Rollen auf jeweils pro Datenbank hinzufügen.



## <a name="next-steps"></a>Nächste Schritte

[Paketverwaltung für SQL Server-Machine Learning](r-package-management-for-sql-server-r-services.md)