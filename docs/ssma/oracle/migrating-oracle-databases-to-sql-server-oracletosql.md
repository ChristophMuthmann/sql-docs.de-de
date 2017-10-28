---
title: Migrieren von Oracle-Datenbanken zu SQLServer (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e4d283fe3329fb7d2a656720e9e6b72583a95f6b
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migrieren von Oracle-Datenbanken zu SQLServer (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for Oracle ist eine umfassende Umgebung, mit denen Sie schnell zu Oracle-Datenbanken migrieren kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. SSMA für Oracle verwenden, können Sie überprüfen von Datenbankobjekten und Daten, Datenbanken für die Migration zu bewerten, migrieren Sie Datenbankobjekte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, und Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank. Beachten Sie, dass SYS und SYSTEM-Oracle-Schemas nicht migriert werden können.  
  
## <a name="recommended-migration-process"></a>Migrationsprozess empfohlen  
Für eine erfolgreiche Migration von Objekten und Daten aus Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure SQL-Datenbank, das folgende Verfahren verwenden:  
  
1.  [Erstellen Sie ein neues SSMA-Projekt](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b).  
  
    Nachdem Sie das Projekt erstellt haben, können Sie die projektkonvertierung, Migrations- und Optionen des Typmappings festlegen. Informationen zu projekteinstellungen finden Sie unter [Einstellung Projektoptionen &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Informationen zum Anpassen der datentypzuordnungen finden Sie unter [Zuordnen von Oracle und SQL Server-Datentypen &#40; OracleToSQL &#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Herstellen einer Verbindung mit dem Oracle-Datenbankserver](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
3.  [Herstellen einer Verbindung mit einer Instanz von SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
4.  [Zuordnen von Oracle-Datenbankschemas zu SQL Server-Datenbankschemas](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc).  
  
5.  Optional, [erstellen Bewertungsberichte](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) zum Bewerten der Datenbankobjekte für die Konvertierung und schätzen Sie die Konvertierungszeit.  
  
6.  [Konvertieren von Oracle-Datenbankschemas in SQL Server-Schemas](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272).  
  
7.  [Laden Sie die konvertierte Datenbankobjekte in SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
    Sie können dies in eine der folgenden Arten erfolgen:  
  
    -   Speichern Sie ein Skript aus, und führen Sie es in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Synchronisieren Sie die Datenbankobjekte.  
  
8.  [Migrieren von Daten mit SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
9. Bei Bedarf datenbankanwendungen zu aktualisieren.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Erste Schritte mit SSMA für Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  

