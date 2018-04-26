---
title: Zuordnen von MySQL und SQL Server-Datentypen (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
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
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67a23e286e6d3a7c125d37e5f5cb68f01751fba0
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Zuordnen von MySQL und SQL Server-Datentypen (MySQLToSQL)
MySQL-Datenbank-Datentypen unterscheiden sich von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank-Datentypen. Bei der Konvertierung von MySQL-Datenbankobjekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte, müssen Sie angeben, Zuordnen von Datentypen von MySQL zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können die standardmäßigen datentypzuordnungen übernehmen, oder die Zuordnungen können angepasst werden, wie in den folgenden Verfahren gezeigt.  
  
## <a name="default-mappings"></a>Standardzuordnungen  
SSMA ist einen Standardsatz von datentypzuordnungen. Die Liste der standardzuordnungen finden Sie [Projekteinstellungen &#40;Type Mapping&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Vererbung des Typmappings  
Sie können Zuordnungen auf Projektebene, Objekt Category-Ebene (z. B. alle gespeicherten Prozeduren) oder Objektebene anpassen. Einstellungen werden von der höheren Ebene geerbt, es sei denn, sie auf einer niedrigeren Ebene überschrieben werden. Angenommen, Sie ordnen **"smallint"** auf **Int** auf Projektebene, werden alle Objekte im Projekt verwenden Sie diese Zuordnung, es sei denn, Sie anpassen, dass die Zuordnung auf der Ebene Objekt oder Kategorie.  
  
Beim Anzeigen der **Type Mapping** Registerkarte im Hintergrund SSMA ist farbcodiert, um anzuzeigen, welche Typmappings geerbt werden. Der Hintergrund einer Zuordnung ist gelb alle geerbten Typzuordnung und weiß für eine beliebige Zuordnung, die auf der aktuellen Ebene angegeben ist.  
  
## <a name="customizing-data-type-mappings"></a>Anpassen von Datentypzuordnungen  
  
-   **Zuordnen von Datentypen**  
  
    Die folgenden Verfahren wird das Zuordnen von Datentypen auf Projekt, Datenbank- oder Objektebene Datenbank gezeigt:  
  
    1.  Datentypzuordnung für das gesamte Projekt anpassen möchten, öffnen Sie die **Projekteinstellungen** (Dialogfeld). Wählen Sie im Menü Extras **Projekteinstellungen**.  
  
        Wählen Sie im linken Bereich **Type Mapping**. Der Typ Zuordnung Diagramm und Schaltflächen werden im rechten Bereich angezeigt.  
  
    2.  Wählen Sie die Datenbank oder Tabelle in der MySQL-Metadaten-Explorer aus, um datentypzuordnungen Ebene der Datenbank oder Tabelle anzupassen. Wählen Sie in der MySQL-Metadaten-Explorer den Ordner oder das Objekt, um anzupassen.  
  
        Klicken Sie im rechten Bereich auf **Type Mapping**.  
  
-   **Wenn eine neue Zuordnung hinzufügen möchten, führen Sie folgende Schritte aus:**  
  
    1.  Klicken Sie im Bereich Type Mapping auf **hinzufügen** .  
  
    2.  Geben Sie der neuen Zuordnung (Dialogfeld), unter **Datenquellentyp**, wählen Sie die MySQL-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Längenangabe erfordert, geben Sie die minimalen und maximalen Länge für die Zuordnung durch Auswahl der **aus** und **auf** Kontrollkästchen, und klicken Sie dann die Werte eingeben.  
  
    4.  Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen. Klicken Sie unter **Zieltyp**, wählen Sie die SQL-Zielserver oder SQL Azure-Datentyp.  
  
        1.  Einige Typen erfordern eine Ziel-Datentyplänge. Falls erforderlich, geben Sie die neue Datenlänge in der **ersetzen durch** Feld, und klicken Sie dann auf **OK**.  
  
        2.  Einige Datentypen erfordern den Zieldatentyp **Genauigkeit** und **Skalierung**. Falls erforderlich, geben Sie die neue Genauigkeit und Skalierung der **ersetzen durch** Feld, und klicken Sie dann auf **OK**.  
  
-   **Führen Sie folgende Schritte aus, um eine Zuordnung zu bearbeiten:**  
  
    1.  Klicken Sie im Bereich Type Mapping auf **bearbeiten**.  
  
    2.  In der Zuordnung Liste im Dialogfeld unter **Datenquellentyp**, wählen Sie die MySQL-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Längenangabe erfordert, geben Sie die minimalen und maximalen Länge für die Zuordnung durch Auswahl der **aus** und **auf** Kontrollkästchen, und klicken Sie dann die Werte eingeben.  
  
    Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen. Klicken Sie unter **Zieltyp**, wählen Sie die SQL-Zielserver oder SQL Azure-Datentyp.  
  
    1.  Einige Typen erfordern eine Ziel-Datentyplänge. Falls erforderlich, geben Sie die neue Datenlänge in der **ersetzen durch** Feld, und klicken Sie dann auf **OK**.  
  
    2.  Einige Datentypen erfordern den Zieldatentyp **Genauigkeit** und **Skalierung** . Falls erforderlich, geben Sie die neue Genauigkeit und Skalierung der **ersetzen durch** Feld, und klicken Sie dann auf **OK** .  
  
-   **Um eine datentypzuordnung zu entfernen, führen Sie folgende Schritte aus:**  
  
    1.  Wählen Sie die Zeile in der Liste ' datentypzuordnung ', die die datentypzuordnung enthält, die Sie entfernen möchten, klicken Sie im Bereich "Zuordnung".  
  
    2.  Klicken Sie auf **Entfernen**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht entweder [Erstellen eines Berichts Assessment](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) oder [konvertieren MySQL-Datenbankobjekte in SQL Server- bzw. SQL Azure-Syntax](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7). Wenn Sie einen Bericht erstellen, werden die MySQL-Objekte während der Bewertung automatisch konvertiert.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
