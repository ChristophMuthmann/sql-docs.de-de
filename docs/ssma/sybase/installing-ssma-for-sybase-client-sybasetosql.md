---
title: Installieren von SSMA für Sybase-Clients (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5757f632e7e1c784be35a682f25a49a28aa0e200
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Installieren von SSMA für Sybase-Clients (SybaseToSQL)
Die SSMA-Client besteht aus der Programmdateien an, die verwendet werden, für die Verbindung zum Datenbankserver Sybase Adaptive Server Enterprise (ASE) und einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, ASE Datenbankobjekte, die zu konvertierende [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder eine ungültige Syntax für Azure SQL-Datenbank, laden die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQLDB.  
  
Dieses Thema enthält die Installationsvoraussetzungen und Anweisungen zum Installieren von SSMA.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
SSMA ist dienen zum Arbeiten mit ASE 11.9.2 oder höheren Versionen und allen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Bevor Sie SSMA installiert haben, stellen Sie sicher, dass der Computer die folgenden Anforderungen erfüllt:  
  
-   Windows 7 oder höher oder Windows Server 2008 oder höher.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 oder höher.  
  
-   Die [!INCLUDE[msCoName](../../includes/msconame_md.md)] Version von .NET Framework 4.0 oder höher. .NET Framework, Version 4.0 wird über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Produktmedien. Sie können auch erhalten sie über die [.NET Framework Developer Center](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Der Anbieter für Sybase OLEDB/ADO.Net/ODBC und eine Verbindung mit der Sybase ASE-Datenbankserver mit den Datenbanken, die Sie migrieren möchten. Sie können von dem Produktdatenträger Sybase ASE Anbieter installieren. Informationen zur Konnektivität finden Sie unter [Herstellen einer Verbindung mit der Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Zugriff auf sowie ausreichende Berechtigungen auf dem Computer, der die Zielinstanz des hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, in dem Sie Datenbankobjekte und Daten migrieren. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[Herstellen einer Verbindung mit Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB RAM empfohlen.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>SSMA installieren für Sybase-Client  
SSMA ist ein Webdownload. Informationen zum Herunterladen der neuesten Version finden Sie unter der [Downloadseite für SQL Server Migration Assistant](http://aka.ms/ssmaforsybase).  
  
Nachdem Sie die neueste Version heruntergeladen haben, müssen Sie die Installationsdateien aus dem Extrahieren, vor der Installation von SSMA.  
  
**Zum Installieren des SSMA-Clients**  
  
1.  Doppelklicken Sie auf SSMA für Sybase *n*. Install.exe, wobei *n* Nummer des Builds.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
    Wenn Sie nicht die erforderlichen Komponenten installiert haben, wird eine Meldung angezeigt, der angibt, dass Sie zuerst die erforderlichen Komponenten installieren müssen. Stellen Sie sicher, dass Sie alle erforderlichen Komponenten installiert haben, und führen Sie das Installationsprogramm erneut aus.  
  
3.  Lesen Sie den Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, aktivieren **ich stimme den Bedingungen des Lizenzvertrags**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
5.  Klicken Sie auf **Installieren**.  
  
> [!IMPORTANT]  
> 1.  Deinstallieren Sie alle vorherige Versionen von SSMA für Sybase, bevor die neue Version installiert.  
  
Der Standardinstallationspfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Migration Assistant für Sybase.  
  
Zusätzlich zu den SSMA-Programmdateien, müssen Sie auch die SSMA für Sybase Erweiterung Pack installieren, auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Weitere Informationen finden Sie unter [SSMA-Komponenten installieren, auf SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA-Komponenten in SQLServer &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
