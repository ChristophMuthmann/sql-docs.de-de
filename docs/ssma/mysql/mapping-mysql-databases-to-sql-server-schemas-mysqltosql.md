---
title: Zuordnen von MySQL-Datenbanken zu SQL Server-Schemas (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6f6472656dbfd31ca64348d066cca19f303b4a5f
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Zuordnen von MySQL-Datenbanken zu SQL Server-Schemas (MySQLToSQL)
Standardmäßig SSMA für die MySQL migriert alle Objekte in einer MySQL-Schema in einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank mit dem Namen für das Schema. Sie können jedoch die Zuordnung zwischen Schemas MySQL anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL und SQLServer oder SQL Azure Schemas  
Der MySQL-Konzept eines Schemas ist das SQL Server-Konzept einer Datenbank und eines seiner Schemas zugeordnet. SSMA bezieht sich auf die SQL Server-Kombination der Datenbank und Schema als ein Schema.  
  
Der MySQL-Konzept eines Schemas ist das SQL Server-Konzept einer Datenbank und eines seiner Schemas zugeordnet. Z. B. möglicherweise MySQL ein Schema mit dem Namen **HR**. Eine Instanz von SQL Server möglicherweise eine Datenbank namens **HR**, und innerhalb dieser Datenbank sind Schemas. Ein Schema ist die **Dbo** (oder Datenbankbesitzer) Schema. Standardmäßig wird der MySQL-Schema **HR** zugeordnet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank- und Schemaobjekte **HR.dbo**. SSMA bezieht sich auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Kombination von Datenbank und das Schema als ein Schema.  
  
Sie können die Zuordnung zwischen MySQL ändern und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Azure-Schemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Ändern der Zieldatenbank und Schema  
Sie können eine MySQL-Schema, keine verfügbaren zuordnen, in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schema.  
  
**So ändern Sie die Datenbank und schema**  
  
1.  Wählen Sie im MySQL-Metadaten-Explorer **Schemas**.  
  
    Die **Schema zuordnen** Registerkarte ist auch verfügbar, wenn Sie einzelne Schemas auswählen. Die Liste in die **Schema zuordnen** Registerkarte für das ausgewählte Objekt angepasst wird.  
  
2.  Klicken Sie im rechten Bereich auf die **Schema zuordnen** Registerkarte.  
  
    Sie sehen eine Liste aller MySQL-Schemas, gefolgt von einem Zielwert. Dieses Ziel wird in zwei Teilen Vermerk gekennzeichnet (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, in dem die Objekte und Daten migriert werden.  
  
3.  Wählen Sie die Zeile, die die Zuordnung, die Sie ändern möchten enthält, und klicken Sie dann auf **ändern**.  
  
    In der **Zielschema auswählen** (Dialogfeld), können Sie für die Zieldatenbank verfügbar "und" Schema "oder" Geben Sie die Datenbank und das Schema in das Textfeld in einer zweiteiligen-Schreibweise (database.schema) und klicken Sie dann auf Durchsuchen **OK**.  
  
4.  Das Ziel ändert sich die **Schema zuordnen** Registerkarte.  
  
**Modi für eine Zuordnung**  
  
-   Zuordnen von SQL Server  
  
Sie können keiner Zieldatenbank Quelldatenbank zuordnen. Standardmäßig wird die Quelldatenbank zugeordnet Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, mit denen Sie über SSMA verbunden haben. Wenn die Zieldatenbank zuzuordnenden auf nicht vorhandene wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann mit einer Meldung werden Sie aufgefordert **"die Datenbank bzw. das Schema ist nicht im Ziel vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen?"** Klicken Sie auf "Ja". Auf ähnliche Weise können Sie Schemas unter Ziel nicht vorhandenen Schema zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, der während der Synchronisierung erstellt wird.  
  
-   Zuordnen zu SQL Azure  
  
Sie können die Quelldatenbank zuordnen, mit dem Ziel verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank oder alle Schemas in der verbundenen Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Wenn Sie alle nicht vorhandenen Schema unter verbundenen Zieldatenbank Quelle Schema zuordnen, werden Sie mit einer Meldung aufgefordert **"das Schema ist im Ziel-Metadaten nicht vorhanden. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen? "** Klicken Sie auf "Ja".  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Zurücksetzen auf die Standarddatenbank und das Schema  
Wenn Sie die Zuordnung zwischen einer MySQL-Schema und eine SQL Server-Datenbankschemas anpassen, können die Zuordnung wieder auf die Standardwerte zurückgesetzt werden.  
  
**Um die Standarddatenbank und das Schema wiederherzustellen**  
  
1.  Klicken Sie unter der Registerkarte "Schema-Zuordnung" Wählen Sie eine beliebige Zeile, und klicken Sie auf **auf Standard zurücksetzen** , um die Standarddatenbank und das Schema wiederherzustellen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie die Konvertierung von MySQL-Objekten in SQL Server- bzw. SQL Azure-Objekte analysieren möchten, können Sie [erstellen Sie ein Konvertierungsbericht](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) andernfalls können Sie [konvertieren Sie die MySQL-Datenbank-Objektdefinitionen](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7) in SQL Server oder SQL Azure-Schemas  
  
## <a name="see-also"></a>Siehe auch  
[Projekteinstellungen &#40; Konvertierung &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Herstellen einer Verbindung mit Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Herstellen einer Verbindung mit SQLServer &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  

