---
title: So verwenden Sie RevoScaleR-Funktionen zum Suchen, oder installieren Sie R-Paketen auf SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/08/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: e10435c2a0cdc5ed181aeab9bdd0bbfefa9a7f25
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>So verwenden Sie RevoScaleR-Funktionen zum Suchen, oder installieren R-Pakete auf SQL Server

Microsoft R Server-Version 9.0.1 eingeführten neue RevoScaleR-Funktionen, dass die Verwendung in einer SQL Server-computekontext Pakete installiert. Diese neuen Funktionen vereinfachen Datenanalysten R-Code in SQL Server ohne direkten Zugriff auf den Server ausgeführt.

Jede Datenanalysten kann privater Pakete installieren, die nicht für andere Personen sichtbar sind. Da Pakete in einer Datenbank festgelegt werden können, und jeder Benutzer eine isolierte Paket Sandkasten in jeder Datenbank erhält, ist es einfacher, verschiedene Versionen der gleichen R-Paket installieren.

Wenn Sie Ihre Datenbank zu einem neuen Server migrieren, können Sie auch die Paket-Synchronisierung-Funktion verwenden, liest eine Liste mit allen Paketen und in einer Datenbank auf dem neuen Server installieren.

Dieser Artikel beschreibt diese Funktionen und bietet Beispiele für die Funktionsverwendung.

## <a name="requirements"></a>Anforderungen

+ Um diese Funktionen ausführen zu können, benötigen Sie die Berechtigung zum Ausführen von R-Befehle auf der Instanz.

+ Wenn Sie nicht angeben einen Benutzernamen und das Kennwort bei der Erstellung des computekontexts, dient die Identität des Benutzers, den R-Code ausführt.

+ Bei Verwendung dieser Funktionen aus einem R-Remoteclient müssen zuerst erstellen Sie eine Compute Context-Objekt, mit der [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) Funktion. Übergeben Sie für jede Paket-Management-Funktion, die Sie verwenden und danach computekontext als Argument.

+ Es ist möglich, führen Sie die Paket-Verwaltungsfunktionen, die mit `sp_execute_external_script`. Wenn Sie dies tun, wird die Funktion mithilfe des Sicherheitskontexts des Aufrufers gespeicherte Prozedur ausgeführt.

## <a name="list-of-package-management-functions"></a>Liste der Paket-Verwaltungsfunktionen

Die folgenden Paketverwaltungsfunktionen werden in "revoscaler", für die Installation und Deinstallation von Paketen in einen angegebenen computekontext bereitgestellt:

+ [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): erfahren Sie mehr über Pakete, die in der angegebenen computekontext installiert.

+ [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): Installieren von Paketen in einer computekontext, aus einem angegebenen Repository oder durch Lesen, lokal gespeichert, die ZIP-Paketen.

+ [RxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): installierte Pakete über einen computekontext entfernen.

+ [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): Rufen Sie den Pfad für ein oder mehrere Pakete in der angegebenen computekontext.

+ [RxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): eine Bibliothek Paket zwischen dem Dateisystem und Datenbanken in der angegebenen rechenkontexte kopiert.

+ [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): den Suchpfad für die Bibliothek Strukturen für Pakete während der Ausführung in der SQL-Server abrufen.

Diese Pakete sind in SQL Server-2017 standardmäßig enthalten. Informationen zu diesen Funktionen finden Sie unter dem "revoscaler"-Funktion Referenzseiten: (https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> R-Funktionen für die paketverwaltung sind mit Microsoft R Server 9.0.1 ab. Wenn Sie die Funktionen im "revoscaler" nicht finden können, müssen Sie auf die neueste Version aktualisieren. 

## <a name="examples"></a>Beispiele

Dieser Abschnitt enthält Beispiele zum Verwenden der Paket-Verwaltungsfunktionen mit einer Datenbank oder SQL Server-Instanz. 

+ Die Funktionen zur Paketinstallation prüfen Abhängigkeiten und stellen sicher, dass alle zugehörigen Pakete in SQL Server installiert werden können, gerade wie bei der Installation von R-Paketen im lokalen Rechenkontext.

+ Die Funktion, die _deinstalliert_ Pakete auch Abhängigkeiten berechnet und stellt sicher, dass Pakete, die von anderen Paketen in SQL Server nicht mehr verwendet werden entfernt werden, um Ressourcen freizugeben,.

+ Eine Kombination aus Benutzer und Bereich können Sie Pakete suchen oder eine bestimmte Datenbank Pakete hinzugefügt werden:

    + Pakete in **freigegebener Bereich** installiert werden, indem der Benutzer, die die `rpkgs-shared` Rolle in einer angegebenen Datenbank. Alle Benutzer in dieser Rolle können freigegebene Pakete zu deinstallieren.
    + Pakete in **privaten Bereich** kann installiert werden, von jedem Benutzer, die zu gehören die `rpkgs-private` Rolle in einer Datenbank. Allerdings können Benutzer sehen und nur ihre eigenen Pakete zu deinstallieren.
    + Datenbankbesitzer können freigegeben oder privat Pakete verwenden.

**Von R-code**

Wenn Sie über die Berechtigung zum Installieren der Pakete haben, führen Sie einen des Pakets Verwaltungsfunktionen von Ihrem R-Client, und geben Sie den computekontext, in denen Pakete sind, hinzugefügt oder entfernt werden soll.  Der Rechenkontext kann Ihr lokaler Computer oder eine Datenbank auf der SQL Server-Instanz sein. Ihre Anmeldeinformationen bestimmen, ob der Vorgang auf dem Server abgeschlossen werden kann.

**From Transact-SQL**

Zum Ausführen von Paket-Management-Funktionen in einer gespeicherten Prozedur umschließen Sie sie in einem Aufruf von `sp_execute_external_script`.

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>Rufen Sie die Liste der Pakete in einer SQL Server-computekontext.

In diesem Beispiel wird überprüft, für Pakete, die für die Instanz installiert wurden `myServer`, in der Datenbank `TestDB`. Paketverwaltung wird auf eine bestimmte Datenbank und den Benutzer begrenzt. Wenn der Benutzer nicht angegeben ist, wird davon ausgegangen, dass der Benutzer, die Compute-kontextaufruf ausführt. Weitere Informationen finden Sie unter [Scoping der Pakete nach Rolle](#bkmk_scope).

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>Abrufen von Paketpfad auf einen Remoteserver SQL Server-computekontext

Dieses Paket ruft den Pfad für das **RevoScaleR** -Paket im Rechenkontext *sqlServer*ab.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>Abrufen von Speicherorten für mehrere Pakete

Die folgenden Beispiele rufen die Pfade für die Pakete **RevoScaleR** und **lattice** im Rechenkontext *sqlServer*ab. Übergeben Sie zum Abrufen von Informationen über mehrere Pakete einen Zeichenfolge-Vektor mit den Paketnamen ein.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>Abrufen von Paketversionen auf einem remote-computekontext.

Führen Sie diesen Befehl aus einer R-Konsole zum Abrufen der Build-Nummer und Versionsnummern für Pakete, die auf die computekontext installiert *SqlServer*.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>Installieren eines Pakets in SQL Server

In diesem Beispiel installiert die **prognostizieren** Paket und dessen Abhängigkeiten in den computekontext *SqlServer*.

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

### <a name="synchronize-packages-between-database-and-file-system"></a>Synchronisieren Sie Pakete zwischen Datenbank und Dateisystem

Das folgende Beispiel überprüft die Datenbank **TestDB**, und bestimmt, ob alle Pakete im Dateisystem installiert werden. Wenn einige Pakete fehlen, werden sie im Dateisystem installiert.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

Paketsynchronisierung funktioniert auf einer pro Datenbank und pro Benutzer. Weitere Informationen finden Sie unter [R-Paket-Synchronisierung für SQL Server](../r/package-install-uninstall-and-sync.md).

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

Die `rxSqlLibPaths` -Funktion kann verwendet werden, um zu bestimmen, der aktiven Library von SQL Server-Machine Learning-Services verwendet. Dieses Skript kann nur den Pfad für den aktuellen Server zurückzugeben. 

```SQL
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```
