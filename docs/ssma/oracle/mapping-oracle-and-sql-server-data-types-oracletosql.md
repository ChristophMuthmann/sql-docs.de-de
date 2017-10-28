---
title: Zuordnen von Oracle und SQL Server-Datentypen (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 400ed2a28e622ffb9493af7462e06f551a214a51
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Zuordnen von Oracle und SQL Server-Datentypen (OracleToSQL)
Oracle-Datenbank-Datentypen unterscheiden sich von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank-Datentypen. Bei der Konvertierung von Oracle-Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte aufweist, müssen Sie angeben, Zuordnen von Datentypen aus Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können die standardmäßigen datentypzuordnungen übernehmen, oder die Zuordnungen können angepasst werden, wie in den folgenden Abschnitten gezeigt.  
  
## <a name="default-mappings"></a>Standardzuordnungen  
SSMA ist einen Standardsatz von datentypzuordnungen. Die Liste der standardzuordnungen finden Sie [Projekteinstellungen &#40; Typzuordnung &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
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
  
    Oder zum Anpassen von Datentyp Zuordnung an die Datenbank, Tabelle, Sicht oder gespeicherte Prozedur auf, wählen Sie Datenbank, des Objektkategorie oder des Objekts in Oracle-Metadaten-Explorer:  
  
    1.  Wählen Sie in der Oracle-Metadaten-Explorer den Ordner oder das Objekt, um anzupassen.  
  
    2.  Klicken Sie im rechten Bereich auf die **Type Mapping** Registerkarte.  
  
2.  Wenn eine neue Zuordnung hinzufügen möchten, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie auf **Hinzufügen**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen Sie den Oracle-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** Feld und die maximale Datenlänge in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Um eine datentypzuordnung zu ändern, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie auf **Bearbeiten**.  
  
    2.  Klicken Sie unter **Datenquellentyp**, wählen Sie den Oracle-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Länge erfordert, geben Sie die minimale Datenlänge für die Zuordnung in der **aus** Feld und die maximale Datenlänge in der **zu** Feld.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzt** Feld, und klicken Sie dann[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
4.  Um eine benutzerdefinierte datentypzuordnung zu entfernen, führen Sie folgende Schritte aus:  
  
    1.  Wählen Sie die Zeile, in der Liste ' datentypzuordnung ', die die datentypzuordnung enthält, die Sie entfernen möchten.  
  
    2.  Klicken Sie auf **Entfernen**.  
  
        Geerbte Zuordnungen kann nicht entfernt werden. Allerdings werden geerbte Zuordnungen von benutzerdefinierten Zuordnungen auf einem bestimmten Objekt bzw. die Objektkategorie überschrieben.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt des Migrationsvorgangs besteht entweder [Erstellen eines Berichts Assessment](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) oder [Objekte der Oracle-Datenbank in SQL Server-Syntax konvertieren](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272). Wenn Sie einen Assessment-Bericht erstellen, werden Oracle-Objekten während der Bewertung automatisch konvertiert.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

