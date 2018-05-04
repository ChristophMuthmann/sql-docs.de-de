---
title: Zuordnen von DB2 und SQL Server-Datentypen (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dfee3ae96aadbb2f498b605aaacc818d96ce60a6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>Zuordnen von DB2 und SQL Server-Datentypen (DB2ToSQL)
DB2-Datenbank-Datentypen unterscheiden sich von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank-Datentypen. Bei der Konvertierung von DB2-Datenbankobjekte auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte aufweist, müssen Sie angeben, wie Datentypen von DB2 zugeordnet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können die standardmäßigen datentypzuordnungen übernehmen, oder die Zuordnungen können angepasst werden, wie in den folgenden Abschnitten gezeigt.  
  
## <a name="default-mappings"></a>Standardzuordnungen  
SSMA ist einen Standardsatz von datentypzuordnungen. Die Liste der standardzuordnungen finden Sie [Projekteinstellungen &#40;Type Mapping&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="type-mapping-inheritance"></a>Vererbung des Typmappings  
Sie können Zuordnungen auf Projektebene, Objekt Category-Ebene (z. B. alle gespeicherten Prozeduren) oder Objektebene anpassen. Einstellungen werden von der höheren Ebene geerbt, es sei denn, sie auf einer niedrigeren Ebene überschrieben werden. Angenommen, Sie ordnen **Smallmoney** auf **Money** auf Projektebene, werden alle Objekte im Projekt verwenden Sie diese Zuordnung, es sei denn, Sie anpassen, dass die Zuordnung auf der Ebene Objekt oder Kategorie.  
  
Beim Anzeigen der **Type Mapping** Registerkarte im Hintergrund SSMA ist farbcodiert, um anzuzeigen, welche Typmappings geerbt werden. Der Hintergrund einer Zuordnung ist gelb alle geerbten Typzuordnung und weiß für eine beliebige Zuordnung, die auf der aktuellen Ebene angegeben ist.  
  
## <a name="customizing-data-type-mappings"></a>Anpassen von Datentypzuordnungen  
Das folgende Verfahren veranschaulicht das Zuordnen von Datentypen auf das Projekt, Datenbank oder Objektebene:  
  
**Zuordnen von Datentypen**  
  
1.  Datentypzuordnung für das gesamte Projekt anpassen möchten, öffnen Sie die **Projekteinstellungen** (Dialogfeld):  
  
    1.  Auf der **Tools** klicken Sie im Menü **Projekteinstellungen**.  
  
    2.  Wählen Sie im linken Bereich **Type Mapping**.  
  
        Der Typ Zuordnung Diagramm und Schaltflächen werden im rechten Bereich angezeigt.  
  
    Oder zum Anpassen von Datentyp Zuordnung an die Datenbank, Tabelle, Sicht oder gespeicherte Prozedur auf, wählen Sie Datenbank, des Objektkategorie oder des Objekts in DB2-Metadaten-Explorer:  
  
    1.  Wählen Sie im DB2-Metadaten-Explorer den Ordner oder das Objekt, um anzupassen.  
  
    2.  Klicken Sie im rechten Bereich auf die **Type Mapping** Registerkarte.  
  
2.  Wenn eine neue Zuordnung hinzufügen möchten, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen den DB2-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** Feld und die maximale Datenlänge in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Um eine datentypzuordnung zu ändern, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie auf **Bearbeiten**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen den DB2-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** Feld und die maximale Datenlänge in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld, und klicken Sie dann [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  Um eine benutzerdefinierte datentypzuordnung zu entfernen, führen Sie folgende Schritte aus:  
  
    1.  Wählen Sie die Zeile, in der Liste ' datentypzuordnung ', die die datentypzuordnung enthält, die Sie entfernen möchten.  
  
    2.  Klicken Sie auf **Entfernen**.  
  
        Geerbte Zuordnungen kann nicht entfernt werden. Allerdings werden geerbte Zuordnungen von benutzerdefinierten Zuordnungen auf einem bestimmten Objekt bzw. die Objektkategorie überschrieben.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt des Migrationsvorgangs besteht entweder [Bewertungsbericht &#40;DB2ToSQL&#41; ](../../ssma/db2/assessment-report-db2tosql.md) oder [DB2-Schemas konvertieren &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md). Wenn Sie einen Assessment-Bericht erstellen, werden die DB2-Objekte automatisch während der Bewertung konvertiert.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Datenbanken zu SQLServer &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
