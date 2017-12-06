---
title: Zuordnen von DB2-Schemas in SQL Server-Schemas (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
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
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ea0c28ff859b6ca3c54016b808389647e814e22
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>Zuordnen von DB2-Schemas in SQL Server-Schemas (DB2ToSQL)
In DB2 hat jede Datenbank eine oder mehrere Schemas. Standardmäßig werden alle Objekte in einem DB2-Schema, um SSMA migriert eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mit dem Namen für das Schema. Sie können jedoch die Zuordnung zwischen DB2 Schemas anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 und SQL Server-Schemas  
Schemas werden von eine DB2-Datenbank enthält. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] enthält mehrere Datenbanken, von denen jede kann mehrere Schemas haben.  
  
Ordnet die DB2-Konzept eines Schemas die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Konzept einer Datenbank und eines seiner Schemas. Z. B. möglicherweise DB2 ein Schema mit dem Namen **HR**. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] möglicherweise eine Datenbank namens **HR**, und innerhalb dieser Datenbank sind Schemas. Ein Schema ist die **Dbo** (oder Datenbankbesitzer) Schema. Standardmäßig wird der DB2-Schema **HR** zugeordnet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank- und Schemaobjekte **HR.dbo**. SSMA bezieht sich auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Kombination von Datenbank und das Schema als ein Schema.  
  
Sie können die Zuordnung zwischen DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Ändern der Zieldatenbank und Schema  
Sie können einem DB2-Schema, keine verfügbaren zuordnen, in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schema.  
  
**So ändern Sie die Datenbank und schema**  
  
1.  Wählen Sie in der DB2-Metadaten-Explorer **Schemas**.  
  
    Die **Schema zuordnen** Registerkarte ist auch verfügbar, wenn Sie eine einzelne Datenbank, wählen Sie die **Schemas** Ordner oder einzelne Schemas. Die Liste in die **Schema zuordnen** Registerkarte für das ausgewählte Objekt angepasst wird.  
  
2.  Klicken Sie im rechten Bereich auf die **Schema zuordnen** Registerkarte.  
  
    Sie sehen eine Liste aller DB2-Schemas, gefolgt von einem Zielwert. Dieses Ziel wird in zwei Teilen Vermerk gekennzeichnet (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , in dem die Objekte und Daten migriert werden.  
  
3.  Wählen Sie die Zeile, die die Zuordnung, die Sie ändern möchten enthält, und klicken Sie dann auf **ändern**.  
  
    In der **Zielschema auswählen** (Dialogfeld), können Sie für die Zieldatenbank verfügbar "und" Schema "oder" Geben Sie die Datenbank und das Schema in das Textfeld in einer zweiteiligen-Schreibweise (database.schema) und klicken Sie dann auf Durchsuchen **OK**.  
  
4.  Das Ziel ändert sich die **Schema zuordnen** Registerkarte.  
  
**Modi für eine Zuordnung**  
  
-   Zuordnen von SQL Server  
  
Sie können keiner Zieldatenbank Quelldatenbank zuordnen. Standardmäßig wird die Quelldatenbank zugeordnet Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, mit denen Sie über SSMA verbunden haben. Wenn die Zieldatenbank zuzuordnenden auf nicht vorhandene wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann mit einer Meldung werden Sie aufgefordert **"die Datenbank bzw. das Schema ist nicht im Ziel vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen?"** Klicken Sie auf "Ja". Auf ähnliche Weise können Sie Schemas unter Ziel nicht vorhandenen Schema zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, der während der Synchronisierung erstellt wird.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Zurücksetzen auf die Standarddatenbank und das Schema  
Wenn Sie die Zuordnung zwischen einem DB2-Schema anpassen und eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schema können Sie die Zuordnung wieder auf die Standardwerte zurückgesetzt.  
  
**Um die Standarddatenbank und das Schema wiederherzustellen**  
  
1.  Klicken Sie unter der Registerkarte "Schema-Zuordnung" Wählen Sie eine beliebige Zeile, und klicken Sie auf **auf Standard zurücksetzen** , um die Standarddatenbank und das Schema wiederherzustellen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie die Konvertierung von DB2-Datenbankobjekte in analysieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte aufweist, können Sie [(SSMA häufigen Spalten) Data-Migrationsbericht](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung mit SQLServer &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Migrieren von DB2-Datenbanken zu SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
