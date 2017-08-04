---
title: Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63dc9188d93def41a5116386f93bf29e3b744e8e
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-databases-to-sql-server---azure-sql-db-sybasetosql"></a>Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank (SybaseToSQL)
SQL Server Migration Assistant (SSMA) for Sybase ist eine umfassende Umgebung, mit dem Sie schnell Migrieren von Sybase Adaptive Server Enterprise (ASE) Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. SSMA für Sybase verwenden, können Sie überprüfen von Datenbankobjekten und Daten, Datenbanken für die Migration zu bewerten, migrieren Sie die Datenbankobjekte, die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
## <a name="recommended-migration-process"></a>Migrationsprozess empfohlen  
Für eine erfolgreiche Migration von Objekten und Daten aus Datenbanken ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, das folgende Verfahren verwenden:  
  
1.  [Erstellen Sie ein neues SSMA-Projekt](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Nachdem Sie das Projekt erstellt haben, können Sie die projektkonvertierung, Migrations- und Optionen des Typmappings festlegen. Informationen zu projekteinstellungen finden Sie unter [Einstellung Projektoptionen &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md). Informationen zum Anpassen der datentypzuordnungen finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Herstellen einer Verbindung mit dem Datenbankserver Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Herstellen einer Verbindung mit einer Instanz von SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) oder [Herstellen einer Verbindung mit einer Instanz von Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Zuordnen von ASE Datenbankschemas zu SQLServer / Azure SQL-Datenbank-Datenbankschemas](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Optional, [erstellen Bewertungsberichte](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) zum Bewerten der Datenbankobjekte für die Konvertierung und schätzen Sie die Konvertierungszeit.  
  
6.  [Konvertieren von Sybase ASE-Datenbankschemas in SQLServer / Azure SQL-Datenbank-Schemas](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQLServer / Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Sie können entweder durch ein Skript zu speichern und führen Sie es in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, oder Sie können die Datenbankobjekte synchronisieren.  
  
8.  [Migrieren von Daten mit SQLServer / Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Aktualisieren Sie bei Bedarf die datenbankanwendungen.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Erste Schritte mit SSMA für Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

