---
title: "Vorgängerversionen von SQL Server Data Tools (SSDT und SSDT-BI) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
caps.latest.revision: "23"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4b1dab5e822c5ef2f9ac580f4d4cd2e5b43b7ae6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>Vorgängerversionen von SQL Server Data Tools (SSDT und SSDT-BI)

SQL Server Data Tools (SSDT) stellt Projektvorlagen und Entwurfsoberflächen zum Erstellen von SQL Server-Inhaltstypen bereit: relationale Datenbanken, Analysis Services-Modelle, Reporting Services-Berichte und Integration Services-Pakete.  
  
SSDT basiert auf einer Visual Studio-Shell und wird zusammen mit SQL Server veröffentlicht. Neue Versionen von SSDT umfassen die neuesten Funktionen von SQL Server. Ältere Versionen enthalten die Vorlagen und die Entwurfsumgebung, die für diese Version aktuell waren.  
  
SSDT ist abwärtskompatibel, d.h., Sie können jederzeit [das neueste SSDT](download-sql-server-data-tools-ssdt.md) verwenden, um Datenbanken, Modelle, Berichte und Pakete zu entwerfen und bereitzustellen, die für ältere Versionen von SQL Server vorgesehen sind.  
  
> [!NOTE]  
> Die Visual Studio-Shell, mit der SQL Server-Inhaltstypen erstellt werden, wurde unter verschiedenen Namen veröffentlicht, etwa **SQL Server Data Tools**, **SQL Server Data Tools - Business Intelligence**und **Business Intelligence Development Studio**. Zum Lieferumfang von früheren Versionen gehörten unterschiedliche Sätze von Projektvorlagen. Möchten Sie alle Projektvorlagen zusammen in einem SSDT haben, benötigen Sie [die neueste Version](download-sql-server-data-tools-ssdt.md). Andernfalls müssen Sie wahrscheinlich mehrere frühere Versionen installieren, um alle Vorlagen zu erhalten, die in SQL Server verwendet werden.  Pro Version von Visual Studio ist nur eine Shell installiert. Wird ein zweites SSDT installiert, werden nur die fehlenden Vorlagen hinzugefügt.  

## <a name="recent-downloads"></a>Neueste Downloads

Die letzten Downloads werden für den unwahrscheinlichen Fall bereitgestellt, dass Sie mit der [aktuellen Version](download-sql-server-data-tools-ssdt.md) Probleme haben. 

|Release| Visual Studio 2015|Visual Studio 2013|
|:---|:---|:---|
|17.2|[SSDT für VS2015 17.2](https://go.microsoft.com/fwlink/?linkid=852922)| \* n/v|
|17.1|[SSDT für VS2015 17.1](https://go.microsoft.com/fwlink/?linkid=849393)| \* n/v|
|17.0|[SSDT für VS2015 17.0](https://go.microsoft.com/fwlink/?linkid=846626)| \* n/v|
|16.5|[SSDT für VS2015 16.5](https://go.microsoft.com/fwlink/?LinkID=832313)|[SSDT für VS2013 16.5](https://go.microsoft.com/fwlink/?LinkID=832308)|

\* SSDT unterstützt die letzten beiden Versionen von Visual Studio. SSDT für VS2013 wird mit dem Release von Visual Studio 2017 nicht mehr aktualisiert. Weitere Informationen finden Sie im Abschnitt *Häufig gestellte Fragen* dieses [Blogbeitrags des SSDT-Teams](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/).

  
## <a name="links-to-download-pages"></a>Links zu Downloadseiten 
**SQL Relational: Datenbankmodul**  
  
Stellt Vorlagen bereit, mit denen relationale Datenbanken für das RDBMS und Azure SQL-Datenbank erstellt werden können. SSDT ist versionsunabhängig im Hinblick auf das Design einer relationalen Datenbank. Sie können Visual Studio 2012 oder 2013 mit jeder Version des SQL Server-Datenbankmoduls oder von Azure SQL-Datenbank verwenden.  
  
**Datenbank-Designer**  
  
-   [Herunterladen von SSDT für Visual Studio 2013](https://msdn.microsoft.com/dn864412)  
  
-   [Herunterladen von SSDT für Visual Studio 2012](https://msdn.microsoft.com/jj650015)  
  
-   **SSDT für Visual Studio 2010** ist nicht mehr verfügbar. Bitte wählen Sie eine neuere Version aus. Neuere Versionen von SSDT laufen parallel zu Ihren vorhandenen Installationen von Visual Studio 2010. SSDT muss nicht mit der Visual Studio-Vollversion übereinstimmen, die auf Ihrem Computer gespeichert ist.  
  
Visual Studio 2013-Kunden können eine Vorschauversion von SSDT herunterladen, um die neuen Funktionen zu testen, die es in der Produktversion noch nicht gibt.  
  
**SQL BI: Analysis Services, Reporting Services und Integration Services**  
  
BI-Vorlagen werden verwendet, um SSAS-Modelle, SSRS-Berichte und SSIS-Pakete zu erstellen. BI-Designer sind an bestimmte Versionen von SQL Server gebunden. Damit Sie die neueren BI-Funktionen nutzen können, installieren Sie den BI-Designer in einer neueren Version.  
  
**BI-Designer**  
  
[Herunterladen von SSDT-BI für Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014, SQL Server 2012, SQL Server 2008 und 2008 R2)  
  
[Herunterladen von SSDT-BI für Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014, SQL Server 2012, SQL Server 2008 und 2008 R2)  
  
Business Intelligence Development Studio (BIDS) wird über SQL Server-Setup installiert. Es gibt keinen Webdownload. (SQL Server 2008 und 2008 R2)  
  
Für SQL Server 2012 oder 2014 können Sie entweder **SSDT-BI für Visual Studio 2012** oder **SSDT-BI foder Visual Studio 2013**. Der einzige Unterschied zwischen den beiden besteht in der Visual Studio-Version.  
  
## <a name="see-also"></a>Siehe auch  
[Herunterladen von SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Herunterladen von SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[SQL Tools and Utilities (Tools und Hilfsprogramme für SQL)](../tools/overview-sql-tools.md)
