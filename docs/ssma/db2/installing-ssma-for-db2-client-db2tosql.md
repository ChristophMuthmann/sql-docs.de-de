---
title: "Installieren von SSMA für DB2-Client (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cddb418e373c5ac61d2788f7e8a41d51c5976b6b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Installieren von SSMA für die DB2-Client (DB2ToSQL)
Die SSMA-Client besteht aus der Programmdateien an, die die folgenden Aufgaben ausführen:  
  
-   Verbinden Sie mit einer DB2-Datenbank.  
  
-   Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Konvertieren von DB2-Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax.  
  
-   Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Dieses Thema enthält die Installationsvoraussetzungen und Anweisungen zum Installieren von SSMA.  
  
## <a name="prerequisites"></a>Voraussetzungen  
SSMA ist dienen zum Arbeiten mit DB2 für Z/OS, Version 9.0 und 10.0 oder DB2 für LUW Version 9,8 und 10.1 oder höheren Versionen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014.  
  
Bevor Sie SSMA installiert haben, stellen Sie sicher, dass der Computer die folgenden Anforderungen erfüllt:  
  
-   Windows 7 oder höher oder Windows Server 2008 oder höher.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 oder höher.  
  
-   Die [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 oder höher. Die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 steht auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produktmedien. Sie können auch erhalten sie über die [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Microsoft OLE DB-Anbieter für DB2, Version 5 oder eine höhere Version und eine Verbindung mit der DB2-Datenbanken, die Sie migrieren möchten.  
  
-   Zugriff auf sowie ausreichende Berechtigungen auf dem Computer, der die Zielinstanz des hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, in dem Sie Datenbankobjekte und Daten migrieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
-   4 GB RAM empfohlen.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLE DB-Anbieter für DB2  
Informationen zum Herunterladen der OLE DB-Anbieter für DB2, Version 5.0 wechseln Sie zu [Microsoft® SQL Server® 2014 Feature Pack](http://www.microsoft.com/download/details.aspx?id=42295).  
  
SSMA ist ein Webdownload. Informationen zum Herunterladen der neuesten Version finden Sie unter der [Downloadseite für SQL Server Migration Assistant](http://aka.ms/ssmafordb2).  
  
Nachdem Sie die neueste Version heruntergeladen haben, müssen Sie die Installationsdateien aus dem Extrahieren, vor der Installation von SSMA.  
  
**Zum Installieren des SSMA-Clients**  
  
1.  Doppelklicken Sie auf SSMA für DB2  *n* . Install.exe, wobei  *n*  Nummer des Builds.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
    Wenn Sie nicht die erforderlichen Komponenten installiert haben, wird eine Meldung angezeigt, der angibt, dass Sie zuerst die erforderlichen Komponenten installieren müssen. Stellen Sie sicher, dass Sie alle erforderlichen Komponenten installiert haben, und führen Sie das Installationsprogramm erneut aus.  
  
3.  Lesen Sie den Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, aktivieren **ich stimme den Bedingungen des Lizenzvertrags**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
5.  Klicken Sie auf **Installieren**.  
  
> [!IMPORTANT]  
> 1.  Deinstallieren Sie alle vorherige Versionen von SSMA für DB2, bevor die neue Version installiert.  
  
Der Standardinstallationspfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Migration Assistant für DB2.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA-Komponenten für SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Migrieren von DB2-Datenbanken zu SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
