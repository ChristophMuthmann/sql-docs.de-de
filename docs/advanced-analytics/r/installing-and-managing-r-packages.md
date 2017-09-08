---
title: Installieren und Verwalten von R-Paketen | Microsoft-Dokumenation
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae30bfc42e42b69158dbba5a38b0bccbe93523b4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="installing-and-managing-r-packages"></a>Installieren und Verwalten von R-Paketen
 Jede R-Lösung, die in [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ausgeführt wird, muss Pakete verwenden, die in der R-Standardbibliothek installiert sind. In der Regel beziehen sich R-Lösungen auf Benutzerbibliotheken, indem sie einen Dateipfad in R-Code angeben. Dies wird jedoch nicht in der Produktion empfohlen.

Daher ist es die Aufgabe des Datenbankadministrators oder eines anderen Administrators auf dem Server, sicherzustellen, dass alle erforderlichen Pakete auf der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz installiert sind. Wenn Sie nicht über Administratorberechtigungen auf dem Computer verfügen, der die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanz hostet, können Sie dem Administrator die Vorgehensweise erläutern, wie R-Pakete installiert werden sowie Zugriff auf ein sicheres Paketrepository bereitstellen, wo von Benutzern angeforderte Pakete abgerufen werden können. Dieser Abschnitt enthält diese Informationen. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bietet neue Funktionen zum Installieren und Verwalten von R-Paketen, mit denen sowohl der Datenbankadministrator als auch der Datenanalyst größere Freiheiten und Kontrolle über die Paketverwendung und -einrichtung erhalten. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Installierte Pakete
Bei der Installation von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] werden standardmäßig **Basispakete** installiert, z.B. `stats` und `utils` zusammen mit dem **RevoScaleR**-Paket, das Verbindungen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt.  
  
 
> [!NOTE]  
>  Eine Liste der Pakete, die standardmäßig installiert werden, finden Sie unter [Mit Microsoft R Open installierte Pakete](https://mran.microsoft.com/rro/installed/).  

 Wenn Sie ein zusätzliches Paket von CRAN oder einem anderen Repository benötigen, müssen Sie das Paket auf Ihre Arbeitsstation herunterladen und installieren.  
  
 Muss das neue Paket im Kontext des Servers ausgeführt werden, muss ein Administrator das Paket auf dem Server installieren.   
   
## <a name="where-and-how-to-get-new-packages"></a>Wo und wie Sie neue Pakete erhalten  
 Es gibt mehrere Quellen für R-Pakete. Die bekannteste Quellen sind CRAN und Bioconductor. Auf der offiziellen Website für die R-Sprache ([https://www.r-project.org/](https://www.r-project.org/)) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden auch in GitHub veröffentlicht. Dort können Sie auch den Quellcode erhalten. Möglicherweise haben Sie aber auch R-Pakete erhalten, die von einer Person in Ihrem Unternehmen entwickelt wurden.  
  
 Unabhängig von der Quelle müssen die Pakete im Format einer ZIP-Datei für die Installation bereitgestellt werden. Um darüber hinaus das Paket mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zu verwenden, stellen Sie sicher, die ZIP-Datei im Windows-Binärformat zu erhalten. (Einige Pakete unterstützen möglicherweise dieses Format nicht.) Weitere Informationen zum Inhalt des ZIP-Dateiformats und wie ein R-Paket erstellt wird, empfehlen wir dieses Tutorial, das Sie im PDF-Format von der R-Projektwebsite herunterladen können: [Friedrich Leisch: Creating R Packages (Friedrich Leisch: Erstellen von R-Paketen)](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf). 
  
 Grundsätzlich können R-Pakete ganz einfach über die Befehlszeile installiert werden, ohne sie zuvor herunterzuladen, wenn der Computer Zugang zum Internet hat.  Im Allgemeinen ist dies nicht bei Servern der Fall, die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ausführen.  Um ein R-Paket auf einem Computer zu installieren, der **keinen** Zugriff auf das Internet hat, müssen Sie das Paket vorab in einem korrekt komprimierten Format herunterladen und die ZIP-Dateien in einen Ordner kopieren, auf den der Computer zugreifen kann. 
 
 Die folgenden Themen beschreiben zwei Methoden zur Offlineinstallation von Paketen: 

+ [Create an Offline Package Repository using miniCRAN (Erstellen eines Offlinepaketrepositorys mit miniCRAN)](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  Beschreibt, wie **miniCRAN** des R-Pakets verwendet wird, um ein Offlinerepository zu erstellen. Dies ist wahrscheinlich die effizienteste Methode, wenn Sie Pakete auf mehreren Servern installieren und das Repository an einem zentralen Ort verwalten müssen. 
+ [Install New R Packages from the Internet (Installieren von neuen R-Paketen aus dem Internet)](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  Enthält Anleitungen für die Offlineinstallation von Paketen durch manuelles Kopieren von ZIP-Dateien.   

## <a name="permissions-required-for-installing-r-packages"></a>Erforderliche Berechtigungen zum Installieren von R-Paketen  
  
Um ein neues R-Paket auf einem Computer zu installieren, auf dem [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ausgeführt wird, benötigen Sie Administratorrechte für den Computer.   

Wenn Sie nicht über diese Rechte verfügen, wenden Sie sich an Ihren Administrator, und geben Sie ihm die Informationen zu dem zu installierenden Paket.  
  

Wenn Sie ein neues R-Paket auf einem Computer installieren möchten, der als R-Arbeitsstation dient, und auf dem Computer **keine** Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] installiert ist, benötigen Sie dennoch Administratorrechte für den Computer, um das Paket zu installieren. Nachdem Sie das Paket installiert haben, können Sie es lokal ausführen.  
 
> [!NOTE]
> In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] wurden neue Datenbankrollen hinzugefügt, um die Inhaltskontrolle der Paketinstallationsberechtigungen auf Instanzebene und Datenbankebene zu unterstützen. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Speicherort des Standardspeicherorts der R-Bibliothek für R Services

Wenn Sie [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mithilfe der Standardinstanz installiert haben, befindet sich die R-Paketbibliothek, die von der Instanz verwendet wird, im [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Instanzordner. Beispiel: 

+ Standardinstanz: _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Benannte Instanz: _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Sie können die folgende Anweisung ausführen, um die Standardbibliothek für die aktuelle Instanz von R zu überprüfen. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Weitere Informationen finden Sie unter [Ermitteln der auf SQL Server installierten Pakete](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Verwalten Installierter Pakete

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bietet neue Funktionen zum Installieren und Verwalten von R-Paketen, mit denen sowohl der Datenbankadministrator als auch der Datenanalyst größere Freiheiten und Kontrolle über die Paketverwendung und -einrichtung erhalten. Weitere Informationen finden Sie unter [R-Paketverwaltung für SQL Server](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Wenn Sie SQL Server 2106 R Services verwenden, sind die neuen Paketverwaltungsfunktionen zu diesem Zeitpunkt nicht verfügbar. In der Zwischenzeit stehen Ihnen diese Optionen zur Verfügung, um zu bestimmen, welche Pakete auf dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]-Computer installiert sind; verwenden Sie eine der folgenden Optionen:

+ Anzeigen der Standardbibliothek, wenn Sie über Berechtigungen für den Ordner verfügen
+ Ausführen eines Befehls vom R-Befehl, um Pakete im Speicherort der R_SERVICES-Bibliothek aufzulisten
+ Verwenden einer gespeicherten Prozedur auf der Instanz, z.B. eine der folgenden:
   ```SQL
   EXECUTE sp_execute_external_script  @language=N'R'  
        ,@script = N'str(OutputDataSet);  
        packagematrix <- installed.packages();  
        NameOnly <- packagematrix[,1];  
        OutputDataSet <- as.data.frame(NameOnly);'  
        ,@input_data_1 = N'SELECT 1 as col'  
        WITH RESULT SETS ((PackageName nvarchar(250) ))   
   ```


 ## <a name="see-also"></a>Siehe auch  
 [Verwalten und Überwachen von R-Lösungen](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  

