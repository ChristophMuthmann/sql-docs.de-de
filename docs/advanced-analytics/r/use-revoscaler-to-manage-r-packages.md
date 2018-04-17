---
title: So verwenden Sie RevoScaleR-Funktionen zum Suchen, oder installieren Sie R-Paketen auf SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5e2fd6276e3429b7a59dc0729ce8901a984ec694
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>So verwenden Sie RevoScaleR-Funktionen zum Suchen, oder installieren R-Pakete auf SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft R Server-Version 9.0.1 eingeführten neue RevoScaleR-Funktionen, dass die Verwendung in einer SQL Server-computekontext Pakete installiert. Diese neuen Funktionen vereinfachen Datenanalysten zum Ausführen von R-Code und Installieren von Paketen auf SQL Server ohne direkten Zugriff auf den Server.

## <a name="how-does-it-work"></a>Wie funktioniert es

Wenn Sie R-Server 9.0.1 oder höher Sie können die [RxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages) Funktion von einem Remoteclient "R" zum Installieren der Pakete in einer SQL Server-computekontext. Um diese Option verwenden zu können, müssen Sie paketverwaltung auf dem Server und die Datenbank aktiviert haben. Dieses Feature erfordert auch, dass eine entsprechende Version von R Services "oder" Machine Learning-Dienste auf dem Server installiert werden.

Die neue Version von "revoscaler" enthält auch diese Funktionen: 

+ Die [RxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) Funktion ruft den Pfad für ein oder mehrere Pakete in der angegebenen computekontext ab.

    Eine Kombination aus Benutzer und Bereich können Sie Pakete suchen oder eine bestimmte Datenbank Pakete hinzugefügt werden:

+ Die [RxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) Funktion ruft eine Liste der Pakete installiert, die in der angegebenen computekontext ab.

+ Die [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) -Funktion installiert die Pakete in einen computekontext, entweder aus einem angegebenen Repository oder durch Lesen lokal gespeicherte ZIP-Paketen.

    Diese Funktion überprüft, ob Abhängigkeiten und stellt sicher, dass alle zugehörigen Pakete zu SQL Server, wie durch die Installation von R-Paket im lokalen rechenkontext installiert werden können.

+ Die [RxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) -Funktion entfernt Pakete aus einem angegebenen computekontext.

    Außerdem Abhängigkeiten berechnet, und es wird sichergestellt, dass Pakete, die von anderen Paketen in SQL Server nicht mehr verwendet werden entfernt werden, um Ressourcen freizugeben.

+ Verwenden der [RxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) Funktion, um Informationen zu einer Bibliothek Paket zwischen dem Dateisystem und die Datenbank, für die angegebene computekontext zu kopieren.

+ Verwenden der [RxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) Funktion, um zu bestimmen, den Pfad der Instanz-Bibliothek auf einem SQL Server-computekontext.

**Gilt für:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]. Wird auch unterstützt [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] mit einem Upgrade auf R Server 9.0 oder höher. Andere Einschränkungen gelten.

## <a name="requirements"></a>Anforderungen

+ Um diese Funktionen ausführen zu können, benötigen Sie Berechtigungen für die Verbindung mit dem Server und Ihrer Datenbank und R-Befehle ausführen.

+ Bei Verwendung dieser Funktionen aus einem R-Remoteclient müssen zuerst erstellen Sie eine Compute Context-Objekt, mit der [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) Funktion. Übergeben Sie für jede Paket-Management-Funktion, die Sie verwenden und danach computekontext als Argument.

+ Wenn Sie nicht angeben einen Benutzernamen und das Kennwort bei der Erstellung des computekontexts, dient die Identität des Benutzers, den R-Code ausführt.

+ Es ist auch möglich, führen Sie die Paket-Verwaltungsfunktionen in `sp_execute_external_script`. Wenn Sie dies tun, wird die Funktion mithilfe des Sicherheitskontexts des Aufrufers gespeicherte Prozedur ausgeführt.

+ Pakete in **freigegebener Bereich** installiert werden, indem der Benutzer, die die `rpkgs-shared` Rolle in einer angegebenen Datenbank. Alle Benutzer in dieser Rolle können freigegebene Pakete zu deinstallieren.

+ Pakete in **privaten Bereich** kann installiert werden, von jedem Benutzer, die zu gehören die `rpkgs-private` Rolle in einer Datenbank. Allerdings können Benutzer sehen und nur ihre eigenen Pakete zu deinstallieren.

+ Datenbankbesitzer können freigegeben oder privat Pakete verwenden.

## <a name="package-installation-from-machine-learning-server-or-remote-r-client"></a>Paketinstallation von Machine Learning-Server oder remote-R-client

Bevor Sie beginnen, stellen Sie sicher, dass diese Bedingungen erfüllt sind:

+ Der Client hat RevoScale 9.0.1 oder höher.
+ Eine entsprechende Version von "revoscaler" wurde auf SQL Server-Instanz installiert.
+ Die [Paket Verwaltungsfeature](..\r\r-package-how-to-enable-or-disable.md) für die Instanz aktiviert wurde.
+ Sie sind Mitglied einer Datenbankrolle, die Ihnen ermöglicht, die Pakete auf die angegebene Instanz und die Datenbank zu installieren. In Zukunft werden Rollen Installieren von Paketen auf einen Speicherort freigegeben oder privaten unterstützt. Jetzt können Sie Pakete installieren, wenn Sie ein Datenbankbesitzer sind.

1. Definieren Sie über eine Befehlszeile R eine Verbindungszeichenfolge für die Instanz und die Datenbank ein.
2. Verwenden der [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) Konstruktor, um einen SQL Server-computekontext, mithilfe der Verbindungszeichenfolge zu definieren.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. Erstellen Sie eine Liste der Pakete, die Sie verwenden möchten, installieren, und speichern Sie die Liste in einer Zeichenfolgenvariablen.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. Rufen Sie [RxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) und übergeben des computekontexts und die Zeichenfolgenvariable, die mit den Paketnamen.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    Wenn die abhängigen Programme erforderlich sind, werden sie auch installiert, vorausgesetzt, dass eine Internetverbindung auf dem Client verfügbar ist.
    
    Pakete werden mit den Anmeldeinformationen des Benutzers vornimmt, die Verbindung in den Standardbereich für diesen Benutzer installiert.

## <a name="examples"></a>Beispiele

Dieser Abschnitt enthält Beispiele zur Verwendung dieser Funktionen von einem Remoteclient aus, bei der Verbindung mit einer SQL Server-Instanz oder Datenbank als computekontext.

Für alle Beispiele müssen Sie eine Verbindungszeichenfolge oder einen computekontext, wofür eine Verbindungszeichenfolge bereitstellen. In diesem Beispiel bietet eine Möglichkeit, einen computekontext für SQL Server zu erstellen:

```R
instance_name <- "Machine name/Instance name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

Je nachdem, wo sich der Server befindet, und das Sicherheitsmodell müssen Sie eine Domäne und ein Subnetz-Spezifikation in der Verbindungszeichenfolge bereitstellen, oder verwenden Sie eine SQL-Anmeldung. Beispiel:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"


### Get package path on a remote SQL Server compute context

This example gets the path for the **RevoScaleR** package on the compute context, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**Ergebnisse**

"C: / Program Programme/Microsoft SQL Server/MSSQL14. MSSQLSERVER/R_SERVICES/Library / "revoscaler""

> [!TIP]
> Wenn Sie die Option aus, um die Ausgabe des SQL-Konsole finden Sie unter aktiviert haben, möglicherweise erhalten Sie statusmeldungen aus der Funktion, die vor der `print` Anweisung. Legen Sie Sie nach dem Testen von Code `consoleOutput` auf "false" in der Compute-Kontext-Konstruktor, um Nachrichten zu vermeiden.

### <a name="get-locations-for-multiple-packages"></a>Abrufen von Speicherorten für mehrere Pakete

Im folgende Beispiel ruft die Pfade für die **"revoscaler"** und **Vektorgitters** -Pakete, auf die computekontext `sqlcc`. Übergeben Sie zum Abrufen von Informationen über mehrere Pakete einen Zeichenfolge-Vektor mit den Paketnamen ein.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>Abrufen von Paketversionen auf einem remote-computekontext.

Führen Sie diesen Befehl aus einer R-Konsole zum Abrufen der Build-Nummer und Versionsnummern für Pakete, die auf die computekontext installiert *SqlServer*.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**Ergebnisse**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>Installieren eines Pakets in SQL Server

In diesem Beispiel installiert die **prognostizieren** Paket und dessen Abhängigkeiten in der computekontext.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>Entfernen eines Pakets aus SQL Server

In diesem Beispiel wird die **prognostizieren** Paket und seine Abhängigkeiten aus dem computekontext.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
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
