---
title: "Ermitteln der auf SQL Server installierten Pakete | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Ermitteln der auf SQL Server installierten Pakete
  In diesem Thema wird beschrieben, wie Sie ermitteln können, welche R-Pakete installiert sind, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz.  
  
Standardmäßig die Installation von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] erstellt eine R-Paket-Bibliothek jeder Instanz zugeordnet. Daher müssen um zu wissen, welche Pakete auf einem Computer installiert sind, Sie diese Abfrage für jede separate Instanz ausführen, R Services installiert ist. Beachten Sie, dass die Paket-Bibliotheken sind **nicht** für Instanzen freigegeben, so kann für verschiedene Pakete auf verschiedenen Instanzen installiert werden.

Informationen zum Ermitteln des Standardspeicherort für die Bibliothek für eine Instanz finden Sie unter [Installieren und Verwalten von R-Pakete](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).   
   
 
## Abrufen einer Liste der installierten Pakete, die mithilfe von R  
 Es gibt mehrere Methoden, um eine Liste der installierten oder geladen Pakete, die mit R-Tools und R-Funktionen.  
  
+   Viele R-Entwicklungstools bieten eine Objektkatalog oder eine Liste der installierten oder in den aktuellen R-Arbeitsbereich geladenen Pakete.  

+ Wir empfehlen die folgenden Funktionen aus dem Paket RevoScaleR, die speziell für das Verwalten von Paketen in bereitgestellt werden Kontexte berechnen:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   Sie verwenden eine R-Funktion, z. B. `installed.packages()`, das enthalten ist in den installierten `utils` Paket. Die Funktion durchsucht die Dateien der Beschreibung der einzelnen Pakete, die in der angegebenen Bibliothek gefunden wurde, und gibt eine Matrix der Paketnamen Library-Pfade und Versionsnummern.  
 
### Beispiele  
Im folgenden Beispiel wird die Funktion `rxInstalledPackages` beim Abrufen einer Liste von Paketen, die in der angegebenen SQL Server-Compute-Kontext verfügbar.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 Im folgenden Beispiel wird die grundlegende R-Funktion `installed.packages()` in einem [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur, eine Matrix von Paketen abrufen, die in der Bibliothek R_SERVICES für die aktuelle Instanz installiert wurden. Um zu vermeiden, dass die Felder in der DESCRIPTION-Datei analysiert werden, wird nur der Name zurückgegeben.  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 Weitere Informationen zu den standardmäßigen und die optionalen Felder in der R-Paket-Beschreibungsdatei finden Sie unter [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html).  
  
## Siehe auch  
 [Installieren zusätzlicher R-Pakete unter SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  