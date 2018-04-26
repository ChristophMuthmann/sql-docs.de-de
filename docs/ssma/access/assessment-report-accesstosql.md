---
title: Bewertungsbericht (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
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
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 903fcc1d14d7976e39603bf925595594b0b88170
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="assessment-report-accesstosql"></a>Bewertungsbericht (AccessToSQL)
Assessment Berichtfenster zeigt die Ergebnisse der Konvertierung von Datenbankobjekten zu [!INCLUDE[tsql](../../includes/tsql_md.md)] Syntax, und kann ebenfalls dazu beitragen, die Sie schätzen, die Komplexität und Kosten der Migrationsprojekte.  
  
So erstellen Sie einen Assessment-Bericht ausgewählten Objekten, die für die Konvertierung in der Quelle Metadaten-Explorer Maustaste **Datenbanken**, und wählen Sie dann **Bericht erstellen**. Sie können in diesem Bericht auch automatisch angezeigt, nachdem Sie Schemas konvertieren. Allerdings wird der Berichtsname Konvertierungsbericht sein. Weitere Informationen finden Sie unter [Projekt Einstellungen (GUI) (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>enthalten  
**Explorer-Bereich**  
Enthält eine Hierarchie von Objekten in den Bewertungsbericht. Erweitern Sie die Ordner, um die einzelnen Objekte und Unterkomponenten anzeigen. Wenn Sie eine Kategorie oder ein Objekt klicken, werden die Konvertierungsstatistiken für diese Kategorie oder ein Objekt im Detailbereich angezeigt.  
  
**Detailbereich**  
Zeigt die Konvertierung Statistiken oder Fehler- und warnungsstatusmeldungen Nachrichten für das ausgewählte Objekt. Beispielsweise wenn der Ordner "Tabellen" ausgewählt ist, wird im Detailbereich angezeigt, die Nummern der Fremdschlüssel, Indizes, Primärschlüssel und Tabellen, die konvertiert wurden.  
  
**Meldungsbereich**  
Zeigt die Fehler, Warnungen und informationsmeldungen, die generiert wurden, wenn der Assessment-Bericht erstellt wurde. Nachrichten werden nach Anzahl gruppiert.  
  
Klicken Sie zum Anzeigen von Nachrichtendetails auf **Fehler**, **Warnungen**, oder **Nachrichten**, und erweitern Sie dann eine Nachricht. SSMA wird die Liste der Objekte angezeigt, die diesem Fehler aufweisen. Klicken Sie auf ein Objekt, um alle Konvertierungsdetails für das Objekt anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
[Benutzer-Schnittstelle Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
