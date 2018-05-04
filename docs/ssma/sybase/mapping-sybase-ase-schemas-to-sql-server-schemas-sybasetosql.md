---
title: Zuordnen von Sybase ASE Schemas in SQL Server-Schemas (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c712831f4db10fd10f0d635fc43779c39b0f8953
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Zuordnen von Sybase ASE Schemas in SQL Server-Schemas (SybaseToSQL)
In Sybase Adaptive Server Enterprise (ASE), dass jede Datenbank eine oder mehrere Schemas. Standardmäßig migriert SSMA alle Objekte innerhalb einer Datenbank und des Schemas in derselben Datenbank und Schema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können jedoch die Zuordnung zwischen ASE anpassen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken und Schemas.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE und SQLServer oder SQL Azure Schemas  
ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbanken und ihre Schemas zwei Teil Notierung angeben als *database.schema*. Beispielsweise ist in einer ASE **Demo** Datenbank, die möglicherweise eine **Dbo** Schema. Die Datenbank und Schema-Paar, als angegeben sind **demo.dbo**. Wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure hat die gleiche Datenbank und das Schema, das Paar auch als **demo.dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Ändern der Zieldatenbank und Schema  
Sie können ein Schema ASE zum keine verfügbaren zuordnen, in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schema.  
  
**So ändern Sie die Datenbank und schema**  
  
1.  Wählen Sie im Metadaten-Explorer Sybase **Datenbanken**.  
  
    Die **Schema zuordnen** Registerkarte ist auch verfügbar, wenn Sie eine einzelne Datenbank, wählen Sie die **Schemas** Ordner oder einzelne Schemas. Die Liste in die **Schema zuordnen** Registerkarte für das ausgewählte Objekt angepasst wird.  
  
2.  Klicken Sie im rechten Bereich auf die **Schema zuordnen** Registerkarte.  
  
    Sie sehen eine Liste aller ASE Datenbanken mit ihrer Schemas, gefolgt von einem Zielwert. Dieses Ziel wird in zwei Teilen Vermerk gekennzeichnet (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, in dem die Objekte und Daten migriert werden.  
  
3.  Wählen Sie die Zeile, die die Zuordnung, die Sie ändern möchten enthält, und klicken Sie dann auf **ändern**.  
  
4.  In der **Zielschema auswählen** (Dialogfeld), können Sie für die Zieldatenbank verfügbar "und" Schema "oder" Geben Sie die Datenbank und das Schema in das Textfeld in einer zweiteiligen-Schreibweise (database.schema) und klicken Sie dann auf Durchsuchen **OK**.  
  
5.  Das Ziel ändert sich die **Schema zuordnen** Registerkarte.  
  
**Modi für eine Zuordnung**  
  
-   Zuordnen von SQL Server  
  
Sie können keiner Zieldatenbank Quelldatenbank zuordnen. Standardmäßig wird die Quelldatenbank zugeordnet Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, mit denen Sie über SSMA verbunden haben. Wenn die Zieldatenbank zuzuordnenden auf nicht vorhandene wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann mit einer Meldung werden Sie aufgefordert **"die Datenbank bzw. das Schema ist nicht im Ziel vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen?"** Klicken Sie auf "Ja". Auf ähnliche Weise können Sie Schemas unter Ziel nicht vorhandenen Schema zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, der während der Synchronisierung erstellt wird.  
  
-   Zuordnen zu SQL Azure  
  
Sie können die Quelldatenbank in die verbundene SQL Azure-Zieldatenbank oder eines beliebigen Schemas in der verbundenen SQL Azure-Zieldatenbank zuordnen. Wenn Sie alle nicht vorhandenen Schema unter verbundenen Zieldatenbank Quelle Schema zuordnen, werden Sie mit einer Meldung aufgefordert **"das Schema ist im Ziel-Metadaten nicht vorhanden. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen? "** Klicken Sie auf "Ja".  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Zurücksetzen auf die Standarddatenbank und das Schema  
Wenn Sie die Zuordnung zwischen einem Schema ASE anpassen und eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schema können Sie die Zuordnung wieder auf die Standardwerte zurückgesetzt.  
  
**Um die Standarddatenbank und das Schema wiederherzustellen**  
  
1.  Klicken Sie unter der Registerkarte "Schema-Zuordnung" Wählen Sie eine beliebige Zeile, und klicken Sie auf **auf Standard zurücksetzen** , um die Standarddatenbank und das Schema wiederherzustellen.  
  
## <a name="next-steps"></a>Nächste Schritte  
Wenn Sie die Konvertierung von Sybase ASE-Objekten in analysieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte können Sie [erstellen Sie ein Konvertierungsbericht](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c). Andernfalls können Sie [konvertieren ASE Datenbankobjektdefinitionen](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
