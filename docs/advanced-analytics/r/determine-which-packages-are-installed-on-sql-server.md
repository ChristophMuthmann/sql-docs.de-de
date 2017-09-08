---
title: Ermitteln der auf SQL Server installierten Pakete | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90e7146bde123ca8ac8a8e6ff3e11d212fd4a35a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>Ermitteln der auf SQL Server installierten Pakete
  In diesem Thema wird beschrieben, wie Sie ermitteln können, welche R-Pakete in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz installiert sind.  
  
Standardmäßig erstellt die Installation von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] eine R-Paketbibliothek, die jeder Instanz zugeordnet ist. Daher müssen Sie diese Abfrage für jede separate Instanz ausführen, in der R Services installiert ist, um zu wissen, welche Pakete auf einem Computer installiert sind. Beachten Sie, dass die Paketbibliotheken **nicht** für Instanzen freigegeben sind, sodass für verschiedene Pakete auf verschiedenen Instanzen installiert werden kann.

Informationen zum Ermitteln des Standardspeicherort für die Bibliothek für eine Instanz finden Sie unter [Installing and Managing R Packages (Installieren und Verwalten von R-Paketen)](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>Abrufen einer Liste der installierten Pakete mithilfe von R  
 Es gibt mehrere Methoden, eine Liste der installierten oder geladenen Pakete mit R-Tools und R-Funktionen zu erhalten.  
  
+   Viele R-Entwicklungstools bieten eine Objektkatalog oder eine Liste der installierten oder in den aktuellen R-Arbeitsbereich geladenen Pakete.  

+ Wir empfehlen die folgenden Funktionen aus dem Paket RevoScaleR, die speziell für das Verwalten von Paketen in berechnetem Kontext bereitgestellt werden:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)   
  
+   Sie können eine R-Funktion wie `installed.packages()`verwenden. Diese finden Sie im installierten `utils` -Paket. Die Funktion durchsucht die DESCRIPTION-Dateien der einzelnen Pakete, die in der angegebenen Bibliothek gefunden wurden, und gibt eine Matrix der Paketnamen, Bibliothekspfade und Versionsnummern zurück.  
 
### <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird die Funktion `rxInstalledPackages` beim Abrufen einer Liste von Paketen verwendet, die im angegebenen SQL Server-Computekontext verfügbar sind.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 Im folgenden Beispiel wird die grundlegende R-Funktion `installed.packages()` in einer gespeicherten Prozedur [!INCLUDE[tsql](../../includes/tsql-md.md)] verwendet, um eine Matrix von Paketen abzurufen, die in der Bibliothek R_SERVICES für die aktuelle Instanz installiert wurden. Um zu vermeiden, dass die Felder in der DESCRIPTION-Datei analysiert werden, wird nur der Name zurückgegeben.  
  
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
  
 Weitere Informationen finden Sie in der Beschreibung der optionalen und Standardfelder für die R-Paket-Beschreibungsdatei unter [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren zusätzlicher R-Pakete unter SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

