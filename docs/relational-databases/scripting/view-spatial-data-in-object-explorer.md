---
title: Anzeigen räumlicher Daten im Objekt-Explorer | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4172a48b28cf2b38a9da335caf18c5a60dd21876
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-spatial-data-in-object-explorer"></a>Anzeigen räumlicher Daten im Objekt-Explorer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Im Fenster **Räumliche Ergebnisse** des Abfrage-Editors werden visuelle Zuordnungstools bereitgestellt, mit denen Sie zusätzlich zu den im Fenster **Ergebnisse** im Rasterformat angezeigten Daten Ergebnisse für räumliche Daten anzeigen können. Zum Anzeigen räumlicher Daten im Fenster **Räumliche Ergebnisse** müssen die Abfrageergebnisse mindestens eine Spalte für räumliche Daten mit Geometrie- oder Geografiedaten enthalten.  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>So zeigen Sie räumliche Daten im Fenster "Räumliche Ergebnisse" an  
  
1.  Klicken Sie im Abfrage-Editor auf die Registerkarte **Räumliche Ergebnisse** .  
  
    > [!NOTE]  
    >  Dieses Fenster ist nicht verfügbar, wenn die Abfrageergebnisse keine räumlichen Daten enthalten oder Sie angeben, dass die Ergebnisse als Text zurückgegeben werden.  
  
2.  Wählen Sie die anzuzeigende Spalte in der Liste **Räumliche Spalte auswählen** aus. Wenn in der Tabelle nur eine räumliche Spalte enthalten ist, bildet diese Spalte die Standardoption in der Liste.  
  
3.  Wählen Sie in der Liste **Bezeichnungsspalte auswählen** die nicht räumliche Spalte aus, die Sie für Datenbezeichnungen verwenden möchten.  
  
4.  Wählen Sie in der Liste **Projektion auswählen** die Projektion aus, die Sie für Geografiedaten verwenden möchten. Die Standardprojektion ist Equirectangular. Andere verfügbare Projektionen sind Mercator, Robinson und Bonne.  
  
    > [!NOTE]  
    >  **Projektion auswählen** ist nicht verfügbar, wenn die räumliche Spalte Geometriedaten enthält.  
  
5.  Stellen Sie den Schieberegler **Zoom** ein, um zugeordnete Elemente visuell zu vergrößern. Bei polygonalen Formen ist die Bezeichnung nur sichtbar, wenn die Form groß genug ist, um den Bezeichnungstext aufzunehmen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Fenster "Räumliche Ergebnisse"](../../relational-databases/scripting/spatial-results-window.md)   
 [Abfrage-Editor des Datenbankmoduls &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [Abfrage- und Text-Editoren &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
