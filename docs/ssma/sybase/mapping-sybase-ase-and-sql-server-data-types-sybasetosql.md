---
title: Zuordnen von Sybase ASE und SQL Server-Datentypen (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1e23b31985fac096a05b2735c19abae8e4002a8
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Zuordnen von Sybase ASE und SQL Server-Datentypen (SybaseToSQL)
Datenbanktypen Sybase Adaptive Server Enterprise (ASE) unterscheiden sich von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank-Datentypen. Bei der Konvertierung ASE Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte, müssen Sie angeben, Zuordnen von Datentypen aus ASE zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können die standardmäßigen datentypzuordnungen übernehmen, oder die Zuordnungen können angepasst werden, wie in den folgenden Abschnitten gezeigt.  
  
## <a name="default-mappings"></a>Standardzuordnungen  
SSMA ist einen Standardsatz von datentypzuordnungen. Die Liste der standardzuordnungen finden Sie [Projekteinstellungen &#40; Typzuordnung &#41; &#40; SybaseToSQL &#41; ](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Vererbung des Typmappings  
Sie können Zuordnungen auf Projektebene, Objekt Category-Ebene (z. B. alle gespeicherten Prozeduren) oder Objektebene anpassen. Einstellungen werden von der höheren Ebene geerbt, es sei denn, die auf einer niedrigeren Ebene überschreiben. Angenommen, Sie ordnen **Smallmoney** auf **Money** der Ebene der Projekte werden alle Objekte im Projekt verwenden, diese Zuordnung, es sei denn, Sie die Zuordnung auf der Objektebene-Kategorie oder Objektebene anpassen.  
  
Beim Anzeigen der **Type Mapping** Registerkarte im Hintergrund SSMA ist farbcodiert, um anzuzeigen, welche Typmappings geerbt werden. Der Hintergrund einer Zuordnung ist gelb alle geerbten Typzuordnung und weiß für eine beliebige Zuordnung auf der aktuellen Ebene angegeben.  
  
## <a name="customizing-data-type-mappings"></a>Anpassen von Datentypzuordnungen  
Das folgende Verfahren veranschaulicht das Zuordnen von Datentypen auf das Projekt, Datenbank oder Objektebene.  
  
**Zuordnen von Datentypen**  
  
1.  Datentypzuordnung für das gesamte Projekt anpassen möchten, öffnen Sie die **Projekteinstellungen** (Dialogfeld):  
  
    1.  Auf der **Tools** klicken Sie im Menü **Projekteinstellungen**.  
  
    2.  Wählen Sie im linken Bereich **Type Mapping**.  
  
        Der Typ Zuordnung Diagramm und Schaltflächen werden im rechten Bereich angezeigt.  
  
    Oder zum Anpassen von Datentyp Zuordnung an die Datenbank, Tabelle, Sicht oder gespeicherte Prozedur auf, wählen Sie Datenbank, des Objektkategorie oder des Objekts in Sybase-Metadaten-Explorer:  
  
    1.  Wählen Sie in der Sybase-Metadaten-Explorer den Ordner oder das Objekt, das Sie anpassen möchten.  
  
    2.  Klicken Sie im rechten Bereich auf die **Type Mapping** Registerkarte.  
  
2.  Wenn eine neue Zuordnung hinzufügen möchten, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen Sie die ASE-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** , und geben Sie die maximale Datenlänge für die Zuordnung in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld.  
  
    5.  Klicken Sie auf **OK**.  
  
3.  Führen Sie folgende Schritte aus, um eine datentypzuordnung zu bearbeiten:  
  
    1.  Klicken Sie auf **Bearbeiten**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen Sie die ASE-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** , und geben Sie die maximale Datenlänge für die Zuordnung in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld, und klicken Sie dann auf **OK**.  
  
4.  Um eine benutzerdefinierte datentypzuordnung zu entfernen, führen Sie folgende Schritte aus:  
  
    1.  Wählen Sie die Zeile, in der Liste ' datentypzuordnung ', die die datentypzuordnung enthält, die Sie entfernen möchten.  
  
    2.  Klicken Sie auf **Entfernen**.  
  
        Geerbte Zuordnungen kann nicht entfernt werden. Allerdings werden geerbte Zuordnungen von benutzerdefinierten Zuordnungen auf einem bestimmten Objekt bzw. die Objektkategorie überschrieben.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt des Migrationsvorgangs besteht entweder [Erstellen eines Berichts Assessment](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) oder [konvertieren Sybase ASE-Datenbankobjekte, die SQL Server- oder SQL Azure-Syntax](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3). Wenn Sie einen Assessment-Bericht erstellen, sind Sybase ASE Objekte automatisch während der Bewertung konvertiert.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
