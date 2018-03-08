---
title: Versionshinweise (Odbcdriver for SQLServer) | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 2b0846781a17fdad4c8cf9e39cab743595a20e7e
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="release-notes"></a>Versionsanmerkungen
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Versionsanmerkungen für Microsoft ODBC Driver for SQL Server on Windows.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Neuigkeiten in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC-Treiber 17 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows

**Funktionen**:

Always Encrypted-Unterstützung für BCP-API

Neues Verbindungszeichenfolgen-Attribut UseFMTOnly bewirkt, dass Treiber ältere Metadaten in besonderen Fällen, dass temporäre Tabellen verwenden.

Unterstützung für die verwaltete Azure SQL-Instanz (Erweiterte privater Ansicht). 
> [!NOTE]
> Es gibt eine Reihe von Unterschieden bei Verwendung verwalteter Instanzen:
> -   FILESTREAM wird nicht unterstützt. 
> -   Lokalen Dateisystem Zugriff wird nicht unterstützt, aber für Angaben wie Tracefiles erforderlich 
> -   Erstellen Sie UDT aus lokalen Pfad wird nicht unterstützt. 
> -   Integrierte Windows-Authentifizierung wird nicht unterstützt. 
> -   DTC wird nicht unterstützt. 
> -   Konto'sa' ist nicht vorhanden (Standardkonto ist "CloudSA" genannt)
> -   TDS-token-Fehler (0xAA) gibt falsche Servernamen zurück.
> -   Sonderzeichen im Datenbanknamen werden nicht unterstützt. 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] wird nicht unterstützt.
> -   Die Fehlermeldungen werden immer auf Englisch angezeigt, unabhängig von der Sprache Einstellungen (wie Azure) 
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Neuigkeiten in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Odbcdriver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows  
 ODBC Driver 13.1 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] bietet Unterstützung für [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) und [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) in Verbindung mit Microsoft SQL Server 2016.  Entsprechende Connection pooling Schlüsselwörter/Attribute werden in beschrieben [-Treiber von Treiberfähiges Verbindungspooling im ODBC-Treiber für SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Neuigkeiten in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Odbcdriver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows  
 ODBC Driver 13 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] enthält die vorherigen Funktionen von ODBC Driver 11 für SQL Server und bietet Unterstützung für Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Neuigkeiten in der [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Odbcdriver 11 für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows  
 ODBC Driver 11 für SQL Server enthält neue [Funktionen](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md) sowie alle Funktionen, die mit dem ODBC in SQL Server 2012 Native Client ausgeliefert wurden.  
