---
title: "R-paketverwaltung für SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>R-paketverwaltung für SQL Server

Dieses Thema beschreibt die Paket-Verwaltungsfunktionen, die Sie verwenden können, um R-Pakete verwalten, die auf einer Instanz von SQL Server ausgeführt werden.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

## <a name="package-management-using-t-sql"></a>Verwalten von Paketen mithilfe des T-SQL

Sie können R-Pakete als Administrator auf dem Computer zu installieren, wenn Sie diese Berechtigungen verfügen, und wenn Sie die einzige Person, die mithilfe des Servers für Machine Learning-Aufträge werden weiterhin.

Allerdings ist, wenn Sie Pakete für andere Benutzer freigeben möchten, oder wenn mehrere Personen Machine Learning-Aufträge auf dem Server ausführen müssen, es effizienter, eine Bibliothek des Pakets für shared einrichten. SQL Server unterstützt über die Datenbankrollen.

Der Datenbankadministrator ist verantwortlich für das Einrichten Rollen und Hinzufügen von Benutzern zu Rollen. Über Rollen kann der Datenbankadministrator steuern, wer über die Berechtigung zum Hinzufügen oder Entfernen von R-Pakete aus der SQL Server-Umgebung verfügt, und Paketinstallation überwachen können.

### <a name="database-roles-for-package-management"></a>Datenbankrollen für die Paketverwaltung

Die folgenden neuen Datenbankrollen Unterstützung sicheren Installation und Verwaltung der R-Paket in SQL Server:

- `rpkgs-users`: Ermöglicht es Benutzern, die alle freigegebenen Pakete verwenden, die von Mitgliedern der installiert wurden die `rpkgs-shared` Rolle.

- `rpkgs-private`: Bietet Zugriff auf freigegebene Pakete mit den gleichen Berechtigungen wie die `rpkgs-users` Rolle. Mitglieder dieser Rolle können darüber hinaus Pakete mit privatem Geltungsbereich installieren, entfernen und verwenden.

-  `rpkgs-shared`: Bietet die gleichen Berechtigungen wie die `rpkgs-private` Rolle. Benutzer, die Mitglied dieser Rolle sind, können ebenfalls freigegebene Pakete installieren oder entfernen.

- `db_owner`: Hat die gleichen Berechtigungen wie die `rpkgs-shared` Rolle. Kann darüber hinaus Benutzern das Recht zum Installieren oder Entfernen von freigegebenen und/oder privaten Paketen erteilen.

### <a name="creating-an-external-package-library-using-t-sql"></a>Erstellen einer Bibliothek für externe Paket mithilfe des T-SQL

Darüber hinaus unterstützt SQL Server 2017 die T-SQL-Anweisung **externe Bibliothek erstellen**, um die Verwaltung von Datenbankadministrator von externen Bibliotheken unterstützen. Derzeit können Sie diese Anweisung verwenden, Windows-basierten Bibliotheken für zusätzliche r zu erstellen, die Unterstützung in Zukunft für Python-Pakete und für Pakete, die für die Ausführung auf anderen Plattformen wie Linux geschrieben geplant ist.

Weitere Informationen finden Sie unter [externe Bibliothek erstellen](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="package-management-using-r"></a>Verwalten von Paketen mithilfe von R

Die **"revoscaler"** Paket enthält nun Funktionen zur Unterstützung von einfacher Installation und Verwaltung von R-Pakete. Diese neuen Funktionen, die zusammen mit Datenbankrollen für die paketverwaltung unterstützt folgende Szenarien:

- Der datenanalyst kann erforderlichen R-Pakete auf SQL Server installieren, ohne Sie administrativen Zugriff auf die SQL Server-Computer.
- Die Pakete auf jede Datenbank separat installiert sind, und wenn die Datenbank verschoben wurde, verschieben Sie die Pakete mit.
- Es ist einfacher, die Pakete für andere Benutzer freigeben. Wenn Sie ein lokales paketrepository eingerichtet haben, können jede Datenanalysten Repository zum Installieren der Pakete an sein eigenes Datenbank aus.
- Der Datenbankadministrator muss sich nicht um zu erfahren, wie Sie R-Befehle ausführen und Nachverfolgen von komplexen paketabhängigkeiten muss nicht.
- Der Datenbankadministrator können Datenbankrollen vertraut, um zu steuern, welche SQL Server-Benutzer zulässig sind, installieren, deinstallieren oder das Pakete verwenden.

### <a name="r-package-management-functions"></a>Verwaltungsfunktionen für R-Paket

Die folgenden Paketverwaltungsfunktionen werden in "revoscaler", für die Installation und Deinstallation von Paketen in einen angegebenen computekontext bereitgestellt:

+ [RxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): erfahren Sie mehr über Pakete, die in der angegebenen computekontext installiert.

+ [RxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): Installieren von Paketen in einer computekontext, aus einem angegebenen Repository oder durch Lesen, lokal gespeichert, die ZIP-Paketen.

+ [RxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): installierte Pakete über einen computekontext entfernen.

+ [RxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): Rufen Sie den Pfad für ein oder mehrere Pakete in der angegebenen computekontext.

+ [RxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): eine Bibliothek Paket zwischen dem Dateisystem und Datenbanken in der angegebenen rechenkontexte kopiert.

+ [RxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): den Suchpfad für die Bibliothek Strukturen für Pakete während der Ausführung in der SQL-Server abrufen.

Diese Pakete sind ebenfalls standardmäßig in SQL Server-2017 enthalten. Sie können die Pakete mit einer Instanz von SQL Server 2016 hinzufügen, wenn Sie ein der Instanz Upgrade, mit der mindestens Microsoft R 9.0.1. Weitere Informationen finden Sie unter [verwenden SqlBindR.exe so aktualisieren Sie R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Informationen zu diesen Funktionen finden Sie unter dem "revoscaler"-Funktion Referenzseiten: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>Funktionsweise der paketverwaltung

Wenn Sie über die Berechtigung zum Installieren von Paketen verfügen, führen Sie eine der Paketverwaltungsfunktionen aus Ihrem R-Code aus und geben den Rechenkontext an, zu dem Pakete hinzugefügt bzw. aus dem sie entfernt werden sollen. Der Rechenkontext kann Ihr lokaler Computer oder eine Datenbank auf der SQL Server-Instanz sein. Wenn der Aufruf zum Installieren von Paketen auf SQL Server ausgeführt wird, entscheiden Ihre Anmeldeinformationen darüber, ob der Vorgang auf dem Server abgeschlossen werden kann. Die Funktionen zur Paketinstallation prüfen Abhängigkeiten und stellen sicher, dass alle zugehörigen Pakete in SQL Server installiert werden können, gerade wie bei der Installation von R-Paketen im lokalen Rechenkontext. Die Funktion, die Pakete deinstalliert, berechnet ebenfalls Abhängigkeiten und stellt sicher, dass Pakete, die nicht mehr von anderen Paketen in SQL Server verwendet werden, entfernt werden, um Ressourcen freizugeben.

Jede Datenanalysten kann privater Pakete, die für andere, nicht sichtbar sind installieren und einen privaten Sandkastens für R-Pakete erstellen. Da Pakete in einer Datenbank festgelegt werden können, und jeder Benutzer eine isolierte Paket Sandkasten in jeder Datenbank erhält, ist es einfacher, verschiedene Versionen der gleichen R-Paket installieren.

Wenn Sie Ihre Datenbank zu einem neuen Server migrieren, können Sie die Paket-Synchronisierung-Funktion verwenden, liest eine Liste mit allen Paketen und in einer Datenbank auf dem neuen Server installieren.

> [!NOTE]
> 
> Die R-Funktionen für die paketverwaltung werden beginnend mit Microsoft R Server 9.0.1 bereitgestellt. Wenn Sie die Funktionen im "revoscaler" nicht finden können, müssen Sie auf die neueste Version aktualisieren.

### <a name="bkmk_scope"></a>Eine Bereichsdefinition für Pakete von Rolle

Die neuen Paketverwaltungsfunktionen stellen zwei Gültigkeitsbereiche für die Installation und Verwaltung von Paketen in SQL Server für eine bestimmte Datenbank bereit:

- **Freigegebener Bereich**

  *Freigegebener Bereich* bedeutet, dass dieser Benutzer, die Berechtigung mit der gemeinsam genutzten Bereich angegeben wurden (`rpkgs-shared`) installieren und Deinstallieren von Paketen mit einer angegebenen Datenbank können. Ein Paket, das in einer Bibliothek des freigegebenen Bereichs installiert wurde, kann von anderen Benutzern der Datenbank auf SQL Server verwendet werden, sofern diesen Benutzern die Verwendung der installierten R-Pakete erlaubt ist.

- **Privater Bereich**

  *Private Bereich* bedeutet, dass dieser Benutzer, die Mitgliedschaft in der privaten Bereich-Rolle zugewiesen wurde (`rpkgs-private`) installieren oder Deinstallieren von Paketen in einem privaten Speicherort pro Benutzer definierte können. Daher können alle Pakete, die im privaten Bereich installiert wurden, nur von dem Benutzer verwendet werden, der sie installiert hat. Anders gesagt kann ein Benutzer von SQL Server keine privaten Pakete verwenden, die von einem anderen Benutzer installiert wurden.

Diese Modelle für den *freigegebenen* und den *privaten* Bereich können kombiniert werden, um benutzerdefinierte Sicherheitssysteme zum Bereitstellen und Verwalten von Paketen auf SQL Server zu entwickeln.

Beispielsweise kann dem Leiter oder Manager einer Gruppe von Datenwissenschaftlern die Berechtigung zum Installieren von Paketen erteilt werden, und diese Pakete können dann von allen anderen Benutzern oder Datenwissenschaftlern in der gleichen SQL Server-Instanz verwendet werden.

Für ein anderes Szenario ist möglicherweise eine stärkere Abgrenzung der Benutzer untereinander oder eine andere Verwendung von Paketen erforderlich. In einem solchen Fall kann der private Bereich verwendet werden, um Datenwissenschaftlern Einzelberechtigungen zu erteilen, die nur für das Installieren und Verwenden der von ihnen benötigten Pakete verantwortlich sind. Da Pakete auf Benutzerbasis installiert werden, wirken sich die von einem Benutzer installierten Pakete nicht auf die Arbeit anderer Benutzer aus, die die gleiche SQL Server-Datenbank verwenden.

### <a name="synchronizing-r-package-libraries"></a>Synchronisieren von R-Paket-Bibliotheken

Die CTP-Version 2.0-Version von SQL Server-2017 (und der Version April 2017 von Microsoft R Server) enthält neue R-Funktionen für *synchronisieren Pakete*.

Paket synchronisieren bedeutet, dass das Datenbankmodul die Pakete, die von einem bestimmten Besitzer und die Gruppe verwendet werden nachverfolgt, und können diese Pakete in das Dateisystem schreiben, bei Bedarf. Paketsynchronisierung können in diesen Szenarien:

+ R-Pakete zwischen Instanzen von SQL Server verschoben werden soll
+ Sie müssen erneut Installationspakete für einen bestimmten Benutzer oder eine Gruppe, nachdem eine Datenbank wiederhergestellt wird

Weitere Informationen finden Sie unter [RxSyncPackages](../r/package-install-uninstall-and-sync.md).

## <a name="examples"></a>Beispiele

Diese Beispiele zeigen die grundlegende Verwendung der Paket-Verwaltungsfunktionen. Zum Ausführen dieser Befehle erfordert, dass Sie die Berechtigung zum Ausführen von R-Befehle für die Instanz verfügen.

+ Bei der Ausführung von einem Remoteserver R terminal, die Sie erstellen eine Compute Context-Objekt, eine SQL Server-Instanz angibt und führen Sie dann die Funktionen des computekontexts als Argument übergeben.

+ Zum Ausführen von Paket-Management-Funktionen in einer gespeicherten Prozedur müssen Sie sie in einem Aufruf umschließen `sp_execute_external_script`.

### <a name="package-scoping"></a>Paket Bereichsauswahl

In diesem Beispiel wird überprüft, für Pakete, die für die Instanz installiert wurden `myServer`, in der Datenbank `TestDB`. Paketverwaltung wird auf eine bestimmte Datenbank und den Benutzer begrenzt. Wenn der Benutzer nicht angegeben ist, wird davon ausgegangen, dass der Benutzer, die Compute-kontextaufruf ausführt. Weitere Informationen finden Sie unter [Scoping der Pakete nach Rolle](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>Speicherort des Pakets auf einen Remoteserver SQL Server-computekontext abrufen

Dieses Paket ruft den Pfad für das **RevoScaleR** -Paket im Rechenkontext *sqlServer*ab.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Abrufen von Speicherorten für mehrere Pakete

Die folgenden Beispiele rufen die Pfade für die Pakete **RevoScaleR** und **lattice** im Rechenkontext *sqlServer*ab. Übergeben Sie zum Abrufen von Informationen über mehrere Pakete einen Zeichenfolge-Vektor mit den Paketnamen ein.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>Verwenden einer gespeicherten Prozedur in der Liste von Paketen in SQL Server

Führen Sie diesen Befehl in Management Studio oder ein anderes Tool, das T-SQL, um eine Liste der installierten Pakete auf der aktuellen Instanz erhalten unterstützt mit `rxInstalledPackages` in einer gespeicherten Prozedur.

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Abrufen von Paketversionen auf einem remote-computekontext.

Führen Sie diesen Befehl aus einer R-Konsole zum Abrufen der Build-Nummer und Versionsnummern für Pakete, die auf die computekontext installiert *SqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Installieren eines Pakets in SQL Server

In diesem Beispiel wird das Paket **ggplot2** mit seinen Abhängigkeiten im Rechenkontext *sqlServer*installiert.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>Entfernen eines Pakets aus SQL Server

In diesem Beispiel wird das Paket **ggplot2** mit seinen Abhängigkeiten aus dem Rechenkontext *sqlServer*entfernt.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="package-synchronization"></a>Paketsynchronisierung

Im folgende Beispiel synchronisiert die Pakete installiert, die im Dateisystem mit der Liste der Pakete, die in der Datenbank verwaltet. Wenn einige Pakete fehlen, werden sie im Dateisystem installiert.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren oder Deaktivieren der R-Paket-Verwaltung](../r/r-package-how-to-enable-or-disable.md)

