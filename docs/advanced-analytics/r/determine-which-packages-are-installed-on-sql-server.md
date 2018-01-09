---
title: Bestimmen, welche R-Pakete installiert sind, auf SQL Server | Microsoft Docs
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
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3f906e0c5290b6aa2cab375e4761390f84e718d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Bestimmen Sie, welche R-Pakete auf SQL Server installiert sind

Bei der Installation von Machine Learning in SQL Server mit der R-Language-Option wird eine R-Paket-Bibliothek für die Verwendung von der Instanz erstellt. Jede Instanz auf dem Server hat eine eigenen Paket-Bibliothek. Paket-Bibliotheken können nicht über Instanzen freigegeben werden.

In diesem Artikel wird beschrieben, wie Sie ermitteln können, welche R-Pakete für eine bestimmte SQL Server-Instanz installiert sind.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Generieren Sie die Liste der R-Pakete mithilfe einer gespeicherten Prozedur

Im folgenden Beispiel wird die R-Funktion `installed.packages()` in einem [!INCLUDE [tsql](..\..\includes\tsql-md.md)] gespeicherte Prozedur, eine Matrix aus Paketen abzurufen, die in der Bibliothek R_SERVICES für die aktuelle Instanz installiert wurden. Um zu vermeiden, dass die Felder in der DESCRIPTION-Datei analysiert werden, wird nur der Name zurückgegeben.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Weitere Informationen zu den optionalen und Standardfelder für das Beschreibungsfeld der R-Paket finden Sie unter [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Überprüfen Sie, ob ein Paket mit einer Instanz installiert ist

Wenn Sie ein Paket installiert haben und möchten sicherstellen, dass er für eine bestimmte SQL Server-Instanz verfügbar ist, können Sie durch Ausführen der folgenden Aufruf der gespeicherten Prozedur, laden Sie das Paket und nur Nachrichten zurück. In diesem Beispiel sucht und lädt die Bibliothek "revoscaler" aus, falls verfügbar.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ Wenn das Paket gefunden wird, wird eine Meldung zurückgegeben: "Befehle wurde erfolgreich abgeschlossen."

+ Wenn das Paket gespeichert oder geladen werden kann, erhalten Sie eine Fehlermeldung, die mit dem Text: "ist kein Paket namens"MissingPackageName""

## <a name="get-a-list-of-installed-packages-using-r"></a>Abrufen einer Liste der installierten Pakete, die mithilfe von R

Es gibt mehrere Methoden, eine Liste der installierten oder geladenen Pakete mit R-Tools und R-Funktionen zu erhalten. Viele R-Entwicklungstools bieten eine Objektkatalog oder eine Liste der installierten oder in den aktuellen R-Arbeitsbereich geladenen Pakete. Dieser Abschnitt enthält einige kurze Befehle, die Sie, über alle R-Befehlszeile oder SP verwenden können\_ausführen\_externen\_Skript.

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

## <a name="get-library-location-and-version"></a>Speicherort der Bibliothek und Version abrufen

Im folgenden Beispiel wird der Speicherort von "revoscaler" im lokalen rechenkontext und die Paketversion.

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>Bestimmen der Bibliothek, die von SQL Server verwendeten Pfad

Wenn Sie Machine learning-Komponenten mithilfe von Bindung aktualisiert haben, kann der Pfad zum R-Bibliothek ändern. In diesem Fall möglicherweise vorherigen Verknüpfungen zu R-Tools mit eine frühere Version verweisen. Der Pfad und der Paket-Version von SQL Server verwendet, können Sie sicherstellen, dass einen Befehl wie folgt ausführen:

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**Ergebnisse**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>Siehe auch

[Installieren Sie zusätzliche R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md)
