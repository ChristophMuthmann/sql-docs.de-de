---
title: Zuordnen von Oracle-Schemas in SQL Server-Schemas (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 592c5385efd4c9457405ffec77eac723109fdf6e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Zuordnen von Oracle-Schemas in SQL Server-Schemas (OracleToSQL)
In Oracle hat jede Datenbank eine oder mehrere Schemas. Standardmäßig SSMA migriert alle Objekte in einem Oracle-Schema, um eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank mit dem Namen für das Schema. Sie können jedoch die Zuordnung zwischen dem Oracle-Schemas anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle und SQL Server-Schemas  
Schemas werden von eine Oracle-Datenbank enthält. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] enthält mehrere Datenbanken, von denen jede kann mehrere Schemas haben.  
  
Das Oracle-Konzept eines Schemas ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Konzept einer Datenbank und eines seiner Schemas. Z. B. möglicherweise Oracle ein Schema mit dem Namen **HR**. Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] möglicherweise eine Datenbank namens **HR**, und innerhalb dieser Datenbank sind Schemas. Ein Schema ist die **Dbo** (oder Datenbankbesitzer) Schema. Standardmäßig werden Oracle-Schema **HR** zugeordnet der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank- und Schemaobjekte **HR.dbo**. SSMA bezieht sich auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Kombination von Datenbank und das Schema als ein Schema.  
  
Sie können die Zuordnung zwischen Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Ändern der Zieldatenbank und Schema  
Sie können ein Oracle-Schema, keine verfügbaren zuordnen, in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schema.  
  
**So ändern Sie die Datenbank und schema**  
  
1.  Wählen Sie in der Oracle-Metadaten-Explorer **Schemas**.  
  
    Die **Schema zuordnen** Registerkarte ist auch verfügbar, wenn Sie eine einzelne Datenbank, wählen Sie die **Schemas** Ordner oder einzelne Schemas. Die Liste in die **Schema zuordnen** Registerkarte für das ausgewählte Objekt angepasst wird.  
  
2.  Klicken Sie im rechten Bereich auf die **Schema zuordnen** Registerkarte.  
  
    Sie sehen eine Liste aller Oracle-Schemas, gefolgt von einem Zielwert. Dieses Ziel wird in zwei Teilen Vermerk gekennzeichnet (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , in dem die Objekte und Daten migriert werden.  
  
3.  Wählen Sie die Zeile, die die Zuordnung, die Sie ändern möchten enthält, und klicken Sie dann auf **ändern**.  
  
    In der **Zielschema auswählen** (Dialogfeld), können Sie für die Zieldatenbank verfügbar "und" Schema "oder" Geben Sie die Datenbank und das Schema in das Textfeld in einer zweiteiligen-Schreibweise (database.schema) und klicken Sie dann auf Durchsuchen **OK**.  
  
4.  Das Ziel ändert sich die **Schema zuordnen** Registerkarte.  
  
**Modi für eine Zuordnung**  
  
-   Zuordnen von SQL Server  
  
Sie können keiner Zieldatenbank Quelldatenbank zuordnen. Standardmäßig wird die Quelldatenbank zugeordnet Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, mit denen Sie über SSMA verbunden haben. Wenn die Zieldatenbank zuzuordnenden auf nicht vorhandene wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann mit einer Meldung werden Sie aufgefordert **"die Datenbank bzw. das Schema ist nicht im Ziel vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen?"** Klicken Sie auf "Ja". Auf ähnliche Weise können Sie Schemas unter Ziel nicht vorhandenen Schema zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, der während der Synchronisierung erstellt wird.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Zurücksetzen auf die Standarddatenbank und das Schema  
Wenn Sie die Zuordnung zwischen einem Oracle-Schema anpassen und eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Schema können Sie die Zuordnung wieder auf die Standardwerte zurückgesetzt.  
  
**Um die Standarddatenbank und das Schema wiederherzustellen**  
  
1.  Klicken Sie unter der Registerkarte "Schema-Zuordnung" Wählen Sie eine beliebige Zeile, und klicken Sie auf **auf Standard zurücksetzen** , um die Standarddatenbank und das Schema wiederherzustellen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie die Konvertierung von Oracle-Objekten in analysieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte aufweist, können Sie [erstellen Sie ein Konvertierungsbericht](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357). Andernfalls können Sie [konvertieren Sie die Oracle-Datenbank-Objektdefinitionen](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Objektdefinitionen.  
  
## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung mit SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
