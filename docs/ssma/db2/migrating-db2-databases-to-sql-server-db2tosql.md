---
title: Migrieren von DB2-Datenbanken zu SQLServer (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c908cafeb92acc982bb74d96c4cc6fc2f40bf9a6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migrieren von DB2-Datenbanken zu SQLServer (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) for DB2 ist eine umfassende Umgebung, mit denen Sie schnell zu DB2-Datenbanken migrieren kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. SSMA für DB2 verwenden, können Sie überprüfen von Datenbankobjekten und Daten, Datenbanken für die Migration zu bewerten, migrieren Sie Datenbankobjekte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Beachten Sie, dass Schemas SYS und DB2-SYSTEM migriert werden können.  
  
## <a name="recommended-migration-process"></a>Migrationsprozess empfohlen  
Zur erfolgreichen Migration der Objekte und Daten von DB2-Datenbanken auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, das folgende Verfahren verwenden:  
  
1.  [Neues SSMA-Projekt](http://msdn.microsoft.com/en-us/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Nachdem Sie das Projekt erstellt haben, können Sie die projektkonvertierung, Migrations- und Optionen des Typmappings festlegen. Informationen zu projekteinstellungen finden Sie unter [Projekteinstellungen &#40;Konvertierung&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) und Verwandte Abschnitte. Informationen zum Anpassen der datentypzuordnungen finden Sie unter [DB2 zuordnen und SQL Server-Datentypen &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Herstellen einer Verbindung mit der DB2-Datenbank](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Herstellen einer Verbindung mit SQLServer](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Zuordnen von DB2-Schemas in SQL Server-Schemas](http://msdn.microsoft.com/en-us/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Optional, [Bewertungsberichte](http://msdn.microsoft.com/en-us/9e13eba0-e3cf-4205-974f-c00f982061de) zum Bewerten der Datenbankobjekte für die Konvertierung und schätzen Sie die Konvertierungszeit.  
  
6.  [Konvertieren von DB2 Schemas](http://msdn.microsoft.com/en-us/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Sie können dies in eine der folgenden Arten erfolgen:  
  
    -   Speichern Sie ein Skript aus, und führen Sie es in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Synchronisieren Sie die Datenbankobjekte.  
  
8.  [Migrieren von DB2-Daten in SQLServer](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Bei Bedarf datenbankanwendungen zu aktualisieren.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren von SSMA für DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Erste Schritte mit SSMA für DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
