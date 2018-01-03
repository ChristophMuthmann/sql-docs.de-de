---
title: "Argumente für externe Tools | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments [SQL Server Management Studio]
- external tools [SQL Server Management Studio]
ms.assetid: 3991c13a-f23f-450b-a2ba-19391c399735
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07a73ebeb158d520db011f979bfd2e21c543c22f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="arguments-for-external-tools"></a>Arguments for External Tools
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Argumente sind Variablen, für die die SQL Server Management Studio-Umgebung Werte bereitstellt, wenn ein externes Tool aus dem Menü **Extras** gestartet wird. Externe Tools, z. B. Editor, lassen sich mit dem Dialogfeld **Externe Tools** zum Menü **Extras** hinzufügen.  
  
In der folgenden Tabelle sind die Argumente für externe Tools aufgeführt.  
  
|Name|Argument|Description|  
|--------|------------|---------------|  
|**Elementpfad**|$(ItemPath)|Der vollständige Dateiname der aktuellen Quelle (definiert als Laufwerk + Pfad + Dateiname); leer, wenn ein Fenster aktiv ist, das nicht zur Quelle gehört.|  
|**Elementverzeichnis**|$(ItemDir)|Das Verzeichnis der aktuellen Quelle (definiert als Laufwerk + Pfad); leer, wenn ein Fenster aktiv ist, das nicht zur Quelle gehört.|  
|**Elementdateiname**|$(ItemFilename)|Der Dateiname der aktuellen Quelle (definiert als Dateiname); leer, wenn ein Fenster aktiv ist, das nicht zur Quelle gehört.|  
|**Elementerweiterung**|$(ItemExt)|Die Dateinamenerweiterung der aktuellen Quelle.|  
|**Aktuelle Zeile***|$(CurLine)|Die aktuelle Zeilenposition des Cursors im Editor.|  
|**Aktuelle Spalte***|$(CurCol)|Die aktuelle Spaltenposition des Cursors im Editor.|  
|**Aktueller Text***|$(CurText)|Der aktuelle Text (das Wort unter der aktuellen Cursorposition oder eine einzeilige Auswahl, sofern vorhanden).|  
|**Zielpfad**|$(TargetPath)|Der vollständige Dateiname des Ziels (definiert als Laufwerk + Pfad + Dateiname).|  
|**Zielverzeichnis**|$(TargetDir)|Das Verzeichnis des Ziels.|  
|**Zielname**|$(TargetName)|Der Dateiname des Ziels.|  
|**Zielerweiterung**|$(TargetExt)|Die Dateinamenerweiterung des Ziels.|  
|**Projektverzeichnis**|$(ProjDir)|Das Verzeichnis des aktuellen Projekts (definiert als Laufwerk + Pfad).|  
|**Projektdateiname**|$(ProjFileName)|Der Dateiname des aktuellen Projekts (definiert als Laufwerk + Pfad + Dateiname).|  
|**Projektmappenverzeichnis**|$(SolutionDir)|Das Verzeichnis der aktuellen Projektmappe (definiert als Laufwerk + Pfad).|  
|**Projektmappen-Dateiname**|$(SolutionFileName)|Der Dateiname der aktuellen Projektmappe (definiert als Laufwerk + Pfad + Dateiname).|  
  
* Die aktuelle Zeile oder Spalte bzw. der aktuelle Text hängt von der Position des Cursors im Text-Editor ab, wie in der Statusleiste dargestellt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Externe Tools (Dialogfeld)](../ssms/external-tools-dialog-box.md)  
[Allgemeine Benutzeroberflächenelemente](../ssms/general-user-interface-elements.md)  
  
