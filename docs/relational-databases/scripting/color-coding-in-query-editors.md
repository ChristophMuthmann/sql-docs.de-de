---
title: Farbcodierung in Abfrage-Editoren | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], color coding
- color coding [Query Editor]
ms.assetid: 802882dc-c997-4e3f-8a01-994bb43169ae
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b51afacfd047298f5f498bf956e9a70443ad71c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="color-coding-in-query-editors"></a>Farbcodierung im Abfrage-Editor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Der in die Code-Editoren eingegebene Text wird einer Kategorie zugeordnet, die jeweils durch durch Farben identifiziert werden. Mithilfe der Farben können Sie Text im Code schnell finden. Kommentare sind z. B. dunkelgrün. In der folgenden Tabelle werden die gängigsten Farben aufgelistet. Rufen Sie im Menü **Extras**die Option **Optionen** auf, in dem Sie die vollständige Liste der Farben und ihrer Kategorien anzeigen und ein benutzerdefiniertes Farbschema konfigurieren können. Weitere Informationen zum Ändern der Standardfarben finden Sie unter [Change Font Color, Size, and Style](../../relational-databases/scripting/change-font-color-size-and-style.md).  
  
## <a name="default-code-colors"></a>Standardfarben für Code  
  
|Farbe|Kategorie|  
|-----------|--------------|  
|Red|SQL-Zeichenfolge|  
|Dunkelgrün|Anmerkung|  
|Schwarz auf silberfarbenem Hintergrund|SQLCMD-Befehl|  
|Magenta|Systemfunktionen|  
|Green|Systemtabelle, Sicht oder Tabellenwertfunktion. Außerdem die Systemschemas sys und INFORMATION_SCHEMA.|  
|Blue|Schlüsselwort|  
|Blaugrün|Zeilennummern oder Vorlagenparameter|  
|Kastanienbraun|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )|  
|Dunkelgrau|Operatoren|  
  
## <a name="status-bar"></a>Statusleiste  
 Sie können registrierte Server oder [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Server im Objekt-Explorer konfigurieren, damit sie in der Statusleiste des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors andere Farben aufweisen. Damit können Sie identifizieren, zu welchem Server die einzelnen Editor-Fenster gehören, wenn viele Fenster gleichzeitig geöffnet sind. Weitere Informationen zum Festlegen der Statusleistenfarben finden Sie unter [Statusleiste &#40;Abfrage-Editor des Datenbankmoduls&#41;](../../relational-databases/scripting/status-bar-database-engine-query-editor.md).  
  
 In manchen Editor-Typen wird die Statusleiste nicht angezeigt, oder es werden keine verschiedenen Farben unterstützt.  
  
  
