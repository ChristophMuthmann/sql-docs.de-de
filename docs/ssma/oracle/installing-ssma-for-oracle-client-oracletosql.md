---
title: "Installieren von SSMA für Oracle-Client (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: "19"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 90e1f2b745ef0a093fb7a5b2ebf662aa969154f1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Installieren von SSMA für die Oracle-Client (OracleToSQL)
Die SSMA-Client besteht aus der Programmdateien an, die die folgenden Aufgaben ausführen:  
  
-   Stellen Sie eine Verbindung mit einer Oracle-Datenbank her.  
  
-   Verbinden mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]  
  
-   Konvertieren von Oracle-Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax.  
  
-   Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Dieses Thema enthält die Installationsvoraussetzungen und Anweisungen zum Installieren von SSMA.  
  
## <a name="prerequisites"></a>Voraussetzungen  
SSMA ist dienen zum Arbeiten mit Oracle 9 oder höher und allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Bevor Sie SSMA installiert haben, stellen Sie sicher, dass der Computer die folgenden Anforderungen erfüllt:  
  
-   Windows 7 oder höher oder Windows Server 2008 oder höher.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 oder höher.  
  
-   Die [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 oder höher. Die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 steht auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produktmedien. Sie können auch erhalten sie über die [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Oracle-Client 9.0 oder eine höhere Version und Verbindung mit der Oracle-Datenbanken, die Sie migrieren möchten. Die Version des Oracle-Client muss die gleiche Version wie oder eine höhere Version als die Version der Oracle-Datenbank sein.  
  
    Sie können die Oracle-Client aus dem Oracle-Produktdatenträger oder von der Oracle-Website installieren. Informationen zur Konnektivität finden Sie unter [Herstellen einer Verbindung mit Oracle-Datenbank &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Zugriff auf sowie ausreichende Berechtigungen auf dem Computer, der die Zielinstanz des hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, in dem Sie Datenbankobjekte und Daten migrieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB RAM empfohlen.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>SSMA installieren für Oracle-Client  
SSMA ist ein Webdownload. Informationen zum Herunterladen der neuesten Version finden Sie unter der [Downloadseite für SQL Server Migration Assistant](http://aka.ms/ssmafororacle).  
  
Nachdem Sie die neueste Version heruntergeladen haben, müssen Sie die Installationsdateien aus dem Extrahieren, vor der Installation von SSMA.  
  
**Zum Installieren des SSMA-Clients**  
  
1.  Doppelklicken Sie auf SSMA für Oracle  *n* . Install.exe, wobei  *n*  Nummer des Builds.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
    Wenn Sie nicht die erforderlichen Komponenten installiert haben, wird eine Meldung angezeigt, der angibt, dass Sie zuerst die erforderlichen Komponenten installieren müssen. Stellen Sie sicher, dass Sie alle erforderlichen Komponenten installiert haben, und führen Sie das Installationsprogramm erneut aus.  
  
3.  Lesen Sie den Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, aktivieren **ich stimme den Bedingungen des Lizenzvertrags**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
5.  Klicken Sie auf **Installieren**.  
  
> [!IMPORTANT]  
> 1.  Deinstallieren Sie alle vorherige Versionen von SSMA für die Oracle vor der Installation der neuen Version ein.  
  
Der Standardinstallationspfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Migration Assistant für Oracle.  
  
Zusätzlich zu den SSMA-Programmdateien, müssen Sie auch die SSMA für die Oracle-Erweiterung Pack installieren, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [SSMA-Komponenten installieren, auf SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA-Komponenten für SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
