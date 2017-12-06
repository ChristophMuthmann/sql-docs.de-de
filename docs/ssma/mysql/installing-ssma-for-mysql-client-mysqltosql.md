---
title: "Installieren von SSMA für MySQL-Client (MySQLToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
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
helpviewer_keywords: Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d90df6e2df45b099867240c8d8272871ce5333cf
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Installieren von SSMA für die MySQL-Client (MySQLToSQL)
SSMA für MySQL-Client besteht aus der Programmdateien an, die die folgenden Aufgaben ausführen:  
  
-   Verbinden Sie mit einer MySQL-Datenbank.  
  
-   Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
-   Konvertieren Sie die MySQL-Datenbankobjekte, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte.  
  
-   Laden Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
-   Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
Dieses Thema enthält die Installationsvoraussetzungen und die Anweisungen zum Installieren von SSMA für MySQL-Client.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
SSMA für die MySQL dient zum Arbeiten mit MySQL 4.1 oder höher und allen Editionen von SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016 und Azure SQL-Datenbank.  
  
Bevor Sie SSMA installiert haben, stellen Sie sicher, dass der Computer die folgenden Anforderungen erfüllt:  
  
-   Windows 7 oder höher oder Windows Server 2008 oder höher.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 oder höher.  
  
-   Die [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 oder höher. Die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] Version 4.0 ist auf dem SQL Server-Produktdatenträger verfügbar. Sie können auch erhalten sie über die [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   MySQL 5.1 Odbcdriver und eine Verbindung mit MySQL-Datenbanken, die Sie migrieren möchten. Sie können die MySQL von der MySQL-Website installieren. Informationen zur Konnektivität finden Sie unter [Herstellen einer Verbindung mit MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Zugriff auf und über ausreichende Berechtigungen auf dem Computer, der die Zielinstanz von SQL Server hostet, in dem Sie Datenbankobjekte und Daten migrieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   Bei einem SQL Azure-Projekte Datenbank den Zugriff auf und Berechtigungen für die Instanz von Azure SQL-Datenbank, in dem Sie migrieren werden, Objekte und Daten. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit Azure SQL-Datenbank &#40; MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB RAM empfohlen.  
  
## <a name="installing-ssma-for-mysql-client"></a>SSMA für MySQL-Client installieren  
SSMA ist ein Webdownload. Informationen zum Herunterladen der neuesten Version finden Sie unter der [Downloadseite für SQL Server Migration Assistant](http://aka.ms/ssmaformysql).  
  
Nachdem Sie die neueste Version heruntergeladen haben, müssen Sie die Installationsdateien zu entpacken vor der Installation von SSMA.  
  
**Zum Installieren des SSMA-Clients**  
  
1.  Doppelklicken Sie auf SSMA für MySQL  *n* . Install.exe, wobei  *n*  Nummer des Builds.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
    Wenn Sie nicht die erforderlichen Komponenten installiert haben, wird eine Meldung angezeigt, der angibt, müssen Sie zuerst die erforderlichen Komponenten installieren. Stellen Sie sicher, dass Sie alle erforderlichen Komponenten installiert haben, bevor Sie das Installationsprogramm erneut ausführen.  
  
3.  Lesen Sie den Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, aktivieren **ich stimme den Bedingungen des Lizenzvertrags**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
5.  Klicken Sie auf **Installieren**.  
  
> [!IMPORTANT]  
> 1.  Deinstallieren Sie alle vorherige Versionen von SSMA für MySQL, bevor die neue Version installiert.  
  
Der Standardinstallationspfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Migration Assistant für MySQL.  
  
Auf 64-Bit-Windows-Computer ist das Produkt in C:\Microsoft SQL Server Migration Assistant für MySQL installiert.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
