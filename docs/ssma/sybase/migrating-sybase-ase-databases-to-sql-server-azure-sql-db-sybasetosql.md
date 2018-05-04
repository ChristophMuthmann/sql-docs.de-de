---
title: Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 60f4310c484f2587f53414590aac8743fb5c1561
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrieren von SAP ASE-Datenbanken zu SQL Server - Azure SQL-Datenbank (SybaseToSQL)
SQL Server Migration Assistant (SSMA) für SAP Adaptive Server Enterprise (ASE) ist eine umfassende Umgebung, mit denen Sie schnell zu SAP ASE Datenbanken migrieren kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. SSMA für SAP ASE verwenden, können Sie überprüfen von Datenbankobjekten und Daten, Datenbanken für die Migration zu bewerten, migrieren Sie Datenbankobjekte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank.  
  
## <a name="recommended-migration-process"></a>Empfohlene Migrationsprozess  
Zur erfolgreichen Migration der Objekte und Daten von SAP ASE Datenbanken [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank das folgende Verfahren verwenden:  
  
1.  [Erstellen Sie ein neues SSMA-Projekt](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Nachdem Sie das Projekt erstellt haben, können Sie die projektkonvertierung, Migrations- und Optionen des Typmappings festlegen. Informationen zu projekteinstellungen finden Sie unter [Einstellung Projektoptionen &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Informationen zum Anpassen der datentypzuordnungen finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Herstellen einer Verbindung mit dem Datenbankserver SAP ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Herstellen einer Verbindung mit einer Instanz von SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) oder [Herstellen einer Verbindung mit einer Instanz von Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Zuordnen von SAP ASE Datenbankschemas zu SQL Server / Azure SQL-Datenbank-Datenbankschemas](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Optional, [erstellen Bewertungsberichte](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) zum Bewerten der Datenbankobjekte für die Konvertierung und schätzen Sie die Konvertierungszeit.  
  
6.  [Konvertieren von SAP ASE-Datenbankschemas in SQL Server / Azure SQL-Datenbank-Schemas](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQL Server / Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Entweder ein Skript zu speichern, und führen Sie es in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank oder die Datenbankobjekte synchronisieren.  
  
8.  [Migrieren von Daten mit SQL Server / Azure SQL-Datenbank](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Aktualisieren Sie bei Bedarf die datenbankanwendungen.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Erste Schritte mit SSMA für SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
