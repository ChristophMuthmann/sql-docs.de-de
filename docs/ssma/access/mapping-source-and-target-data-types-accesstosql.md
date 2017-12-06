---
title: Zuordnen von Quelle und Ziel-Datentypen (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
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
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
caps.latest.revision: "14"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58d908af3ce4c8ee9e04d9499367949e27d9ca3e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>Zuordnen von Quelle und Ziel-Datentypen (AccessToSQL)
Access-Datenbank-Datentypen unterscheiden sich von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank-Datentypen. Wenn Sie den Zugriff auf Datenbankobjekte zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objekte aufweist, müssen Sie angeben, Zuordnen von Datentypen aus den Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können die standardmäßigen datentypzuordnungen übernehmen, oder die Zuordnungen können angepasst werden, wie in den folgenden Verfahren gezeigt.  
  
## <a name="default-mappings"></a>Standardzuordnungen  
SSMA ist einen Standardsatz von datentypzuordnungen. Die Liste der standardzuordnungen finden Sie [Projekteinstellungen (Type-Mapping)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
## <a name="customizing-data-type-mappings"></a>Anpassen von Datentypzuordnungen  
Mithilfe der **Projekteinstellungen** (Dialogfeld), können Sie anpassen, wie Typen für alle Datenbanken und Datenbankobjekte in einem Projekt zugeordnet werden. Die datentypzuordnungen für ein Projekt gelten für alle Datenbanken und Datenbankobjekte, die keine benutzerdefinierte Typmappings.  
  
Sie können auch die datentypzuordnung Ebene der Datenbank oder Tabelle anpassen.  
  
Das folgende Verfahren veranschaulicht das Zuordnen von Datentypen auf Projekt, Datenbank- oder Datenbankebene-Objekt.  
  
**Zuordnen von Datentypen**  
  
1.  Datentypzuordnung für das gesamte Projekt anpassen möchten, öffnen Sie die **Projekteinstellungen** (Dialogfeld):  
  
    1.  Auf der **Tools** klicken Sie im Menü **Projekteinstellungen**.  
  
    2.  Wählen Sie im linken Bereich **Type Mapping**.  
  
        Der Typ Zuordnung Diagramm und Schaltflächen werden im rechten Bereich angezeigt.  
  
    Oder zum datentypzuordnung Ebene der Datenbank oder Tabelle anpassen, wählen Sie die Datenbank oder Tabelle in der Access-Metadaten-Explorer-Bereich:  
  
    1.  Erweitern Sie im Metadaten-Explorer Zugriff **Zugriff Metabasis**, und erweitern Sie dann **Datenbanken**.  
  
    2.  Wählen Sie die Datenbank oder Tabelle, für die Sie die datentypzuordnung anpassen möchten.  
  
    3.  Klicken Sie im rechten Bereich auf **Type Mapping**.  
  
2.  Wenn eine neue Zuordnung hinzufügen möchten, führen Sie folgende Schritte aus:  
  
    1.  Klicken Sie im Bereich Type Mapping auf **hinzufügen**.  
  
    2.  In der **neue Type Mapping** Dialogfeld unter **Datenquellentyp**, wählen Sie die Access-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Längenangabe erfordert, geben Sie die minimalen und maximalen Länge für die Zuordnung durch Auswahl der **aus** und **auf** Kontrollkästchen, und klicken Sie dann die Werte eingeben.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzen durch** Feld, und klicken Sie dann auf **OK**.  
  
3.  Führen Sie folgende Schritte aus, um eine datentypzuordnung zu bearbeiten:  
  
    1.  Klicken Sie im Bereich Type Mapping auf **bearbeiten**.  
  
    2.  In der **Typliste Zuordnung** Dialogfeld unter **Datenquellentyp**, wählen Sie die Access-Datentyp zugeordnet.  
  
    3.  Wenn der Typ eine Längenangabe erfordert, geben Sie die minimalen und maximalen Länge für die Zuordnung durch Auswahl der **aus** und **auf** Kontrollkästchen, und klicken Sie dann die Werte eingeben.  
  
        Dies ermöglicht Ihnen das Anpassen von der datenzuordnung für kleinere und größere Werte denselben Datentyp aufweisen.  
  
    4.  Klicken Sie unter **Zieltyp**, wählen Sie das Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentyp.  
  
        Einige Typen erfordern eine Ziel-Datentyplänge. Wenn dies erforderlich ist, geben Sie die neue Datenlänge in der **ersetzen durch** Feld, und klicken Sie dann auf **OK**.  
  
4.  Um eine datentypzuordnung zu entfernen, führen Sie folgende Schritte aus:  
  
    1.  Wählen Sie die Zeile in der Liste ' datentypzuordnung ', die die datentypzuordnung enthält, die Sie entfernen möchten, klicken Sie im Bereich "Zuordnung".  
  
    2.  Klicken Sie auf **Entfernen**.  
  
## <a name="next-steps"></a>Nächste Schritte  
Der nächste Schritt des Migrationsvorgangs besteht [den Zugriff auf Datenbankobjekte in SQL Server-Objekte zu konvertieren.](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
