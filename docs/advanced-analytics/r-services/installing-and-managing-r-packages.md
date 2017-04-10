---
title: "Installieren und Verwalten von R-Pakete | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Installieren und Verwalten von R-Pakete
 Alle R-Lösungen, die ausgeführt, im wird [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Striches Pakete, die in der Standardbibliothek R installiert sind. In der Regel, R-Lösungen werden benutzerbibliotheken verweisen, indem Sie einen Dateipfad in der R-Code angeben, aber dies wird nicht empfohlen, für die Produktion.

Daher ist es die Aufgabe der Datenbankadministrator oder anderer Administrator auf dem Server, um sicherzustellen, dass alle erforderlichen Pakete installiert sind, auf die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz. Wenn Sie nicht über Administratorrechte auf dem Computer, der als Host verfügen die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]  Instanz, Sie ermöglichen dem Administrator Informationen zum Installieren von R-Pakete und ermöglichen den Zugriff auf eine sichere paketrepository, in denen Pakete, die vom Benutzer angeforderten abgerufen werden können. Dieser Abschnitt enthält diese Informationen. 

> [!TIP]
> [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bietet neue Features für die Installation und Verwaltung von R-Pakete, mit die sowohl der Datenbankadministrator und die Data scientists größere Flexibilität und Kontrolle über die Verwendung des Pakets und Setup zu erhalten. Weitere Informationen finden Sie unter [Paketverwaltung für SQL Server R](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

## <a name="installed-packages"></a>Installierte Pakete
Bei der Installation  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)],  standardmäßig R **Basis** Pakete installiert sind, z. B. `stats` und `utils`, zusammen mit der **"revoscaler"** Paket, das Verbindungen mit unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 
> [!NOTE]  
>  Eine Liste der Pakete, die standardmäßig installiert, finden Sie unter [Pakete installiert, mit Microsoft R Open](https://mran.microsoft.com/rro/installed/).  

 Wenn Sie ein zusätzliches Paket aus CRAN oder ein anderes Repository benötigen, müssen Sie das Paket herunterladen und installieren Sie es auf der Arbeitsstation.  
  
 Wenn Sie das neue Paket im Kontext des Servers ausführen müssen, muss ein Administrator auf dem Server zu installieren.   
   
## <a name="where-and-how-to-get-new-packages"></a>Wo und wie Sie neue Pakete erhalten  
 Es gibt mehrere Quellen für R-Pakete. Die bekannteste Quellen sind CRAN und Bioconductor. Die offizielle Website für die Sprache "R" ([https://www.r-project.org/](https://www.r-project.org/)) sind viele dieser Ressourcen aufgeführt. Viele Pakete werden auch in GitHub veröffentlicht. Dort können Sie auch den Quellcode erhalten. Möglicherweise haben Sie aber auch R-Pakete erhalten, die von einer Person in Ihrem Unternehmen entwickelt wurden.  
  
 Unabhängig von der Quelle müssen die Pakete im Format einer ZIP-Datei für die Installation bereitgestellt werden. Darüber hinaus verwendet das Paket mit [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], achten Sie darauf, dass Sie die ZIP-Datei in das Windows-Binärformat zu erhalten. (Einige Pakete können dieses Format nicht unterstützt.) Für Weitere Informationen zum Inhalt der Zip-Dateiformats und wie Sie ein R-Paket erstellen, empfehlen wir dieses Lernprogramm, das Sie im PDF-Format aus der R-Projektwebsite herunterladen können: [Freidrich Leisch: R-Pakete erstellen](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf). 
  
 Im Allgemeinen können R-Pakete problemlos über die Befehlszeile installieren ohne im Voraus herunterladen, wenn der Computer über Internetzugriff verfügt.  Im Allgemeinen Dies ist nicht der Fall mit Servern mit [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] .  Aus diesem Grund ein R-Paket auf einem Computer installieren, die **nicht** Zugriff auf das Internet haben, müssen Sie das Paket in das richtige ZIP-Format voraus herunterladen und kopieren Sie die ZIP-Dateien in einen Ordner, den Computer zugänglich ist. 
 
 Die folgenden Themen beschreiben, zwei Methoden zum Installieren von Paketen, die offline geschaltet wird: 

+ [Erstellen Sie eine Offline-Paket-Repository mit miniCRAN](../../advanced-analytics/r-services/create-a-local-package-repository-using-minicran.md)

  Beschreibt, wie das R-Paket **MiniCRAN** einem Offline-Repository erstellen. Dies ist wahrscheinlich die effizienteste Methode, wenn Sie Pakete mit mehreren Servern installiert, und das Repository von einem zentralen Ort verwalten müssen. 
+ [Installieren Sie neue R-Pakete aus dem Internet](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)

  Enthält Anweisungen zur Installation von Paketen, die offline bereitgestellten ZIP-Dateien manuell kopieren.   

## <a name="permissions-required-for-installing-r-packages"></a>Erforderliche Berechtigungen zum Installieren von R-Paketen  
  
Um ein neues R-Paket auf einem Computer installieren, auf denen ausgeführt wird, ist [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], benötigen Sie Administratorrechte auf dem Computer.   

Wenn Sie nicht über diese Rechte verfügen, wenden Sie sich an Ihren Administrator, und geben Sie ihm die Informationen zu dem zu installierenden Paket.  
  

Wenn Sie installieren ein neues R-Paket auf einem Computer, der als R-Arbeitsstation verwendet wird und der Computer führt **nicht** eine Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] installiert, Sie benötigen Administratorrechte auf dem Computer zum Installieren des Pakets. Nachdem Sie das Paket installiert haben, können Sie es lokal ausführen.  
 
> [!NOTE]
> In [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], neue Datenbankrollen unterstützen eine Bereichsdefinition für Installationsberechtigungen zur Instanzebene und Datenbankebene im Paket hinzugefügt wurden. Weitere Informationen finden Sie unter [Paketverwaltung für SQL Server R](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).
 

### <a name="location-of-default-r-library-location-for-r-services"></a>Speicherort der R-Bibliothek Standardspeicherort für R Services

Wenn Sie installiert  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] die Standardinstanz verwenden, die von der Instanz verwendeten R-Paket-Bibliothek befindet sich unter dem [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instanzordner. Zum Beispiel: 

+ Standardinstanz _MSSQLSERVER_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
+ Benannte Instanz _MyNamedInstance_
  `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library` 


Sie können die folgende Anweisung aus, um zu überprüfen, die Standardbibliothek für die aktuelle Instanz von r ausführen. 
~~~~
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
~~~~

Weitere Informationen finden Sie unter [bestimmen Pakete auf SQL Server installiert sind](../../advanced-analytics/r-services/determine-which-packages-are-installed-on-sql-server.md).

## <a name="managing-installed-packages"></a>Verwalten von installierte Pakete

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] bietet neue Features für die Installation und Verwaltung von R-Pakete, mit die sowohl der Datenbankadministrator und die Data scientists größere Flexibilität und Kontrolle über die Verwendung des Pakets und Setup zu erhalten. Weitere Informationen finden Sie unter [Paketverwaltung für SQL Server R](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 

Bei Verwendung von SQL Server-2106 R Services sind neue Features für das Paket zu diesem Zeitpunkt nicht verfügbar. In der Zwischenzeit können Sie verfügen über folgende Optionen zur Bestimmung, welche Pakete installiert sind, auf die [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Computer, verwenden Sie eine der folgenden Optionen:

+ Zeigen Sie die Standardbibliothek, wenn Sie Berechtigungen für den Ordner verfügen.
+ Führen Sie einen Befehl aus R-Befehl zum Auflisten der Pakete in den Speicherort der R_SERVICES-Bibliothek
+ Verwenden Sie eine gespeicherte Prozedur z. B. die folgenden, für die Instanz:
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