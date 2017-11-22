---
title: Bestimmen, welche R-Pakete installiert sind, auf SQL Server | Microsoft Docs
ms.custom: 
ms.date: 10/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 63e5b575bb9f1894470b615bc975cd84fb0bffff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Bestimmen Sie, welche R-Pakete auf SQL Server installiert sind

Bei der Installation von Machine Learning in SQL Server mit der R-Sprachoption erstellt Setup eine R-Paket-Bibliothek, die der Instanz zugeordnet. Jede Instanz verfügt über ein separates Paket-Bibliothek. Paket-Bibliotheken sind **nicht** mehreren Instanzen gemeinsam verwendet, sodass es ist möglich für verschiedene Pakete auf verschiedenen Instanzen installiert werden.

In diesem Artikel wird beschrieben, wie Sie feststellen können, welche R-Pakete für eine bestimmte Instanz installiert werden.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Generieren Sie die Liste der R-Pakete mithilfe einer gespeicherten Prozedur

Im folgenden Beispiel wird die R-Funktion `installed.packages()` in einem [!INCLUDE [tsql](..\..\includes\tsql-md.md)] gespeicherte Prozedur, eine Matrix aus Paketen abzurufen, die in der Bibliothek R_SERVICES für die aktuelle Instanz installiert wurden. Um zu vermeiden, dass die Felder in der DESCRIPTION-Datei analysiert werden, wird nur der Name zurückgegeben.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

Weitere Informationen zu den optionalen und Standardfelder für die R-Paket-Beschreibungsdatei finden Sie unter [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Überprüfen Sie, ob ein Paket mit einer Instanz installiert ist

Wenn Sie ein Paket installiert haben und möchten sicherstellen, dass er für eine bestimmte SQL Server-Instanz verfügbar ist, können Sie durch Ausführen der folgenden Aufruf der gespeicherten Prozedur, laden Sie das Paket und nur Nachrichten zurück.

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

In diesem Beispiel sucht und lädt die RevoScaleR-Bibliothek.

+ Wenn das Paket gefunden wird, sollte die zurückgegebene Meldung werden etwa "-Befehle erfolgreich abgeschlossen."

+ Wenn das Paket gespeichert oder geladen werden kann, erhalten Sie eine Fehlermeldung wie folgt: "ein externer Skriptfehler: Fehler in library("RevoScaleR"): ist kein Paket namens" revoscaler ""

## <a name="get-a-list-of-installed-packages-using-r"></a>Abrufen einer Liste der installierten Pakete, die mithilfe von R

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
## <a name="see-also"></a>Siehe auch

[Installieren Sie zusätzliche R-Pakete unter SQL Server](install-additional-r-packages-on-sql-server.md)
