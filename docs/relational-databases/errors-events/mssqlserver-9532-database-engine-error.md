---
title: MSSQLSERVER_9532 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c83d81e219f3b308caf9550c48622ffd116fbbe4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9532|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Meldungstext|Konvertierungsfehler während des Abfrage-/DML-Vorgangs mit dem Spaltensatz '%.*ls' beim Versuch, den '%ls'-Datentyp für die '%.\*ls'-Spalte in den '%ls'-Datentyp zu konvertieren.|  
  
## <a name="explanation"></a>Erklärung  
Bei einem Spaltensatz handelt es sich um eine nicht typisierte XML-Darstellung, die einige Tabellenspalten mit geringer Dichte in einer strukturierten Ausgabe kombiniert. Wenn Sie Sparsespalten mit dem XML-Spaltensatz einfügen bzw. aktualisieren, werden die Werte, die in die zugrunde liegenden Sparsespalten eingefügt werden, vom **xml**-Datentyp implizit konvertiert. Es wurde ein Wert angegeben, der nicht in den Datentyp der Spalte konvertiert werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
Da der bereitgestellte Wert nicht implizit konvertiert werden konnte, könnte es sich um einen ungültigen Eintrag handeln. Beheben Sie den Fehler, und versuchen Sie es erneut. Wenn der Wert korrekt ist, bearbeiten Sie die Anweisung so, dass die einzelnen Spalten anstelle des gesamten Spaltensatzes verwendet werden. Dadurch können Sie den Wert explizit in den richtigen Datentyp umwandeln.  
  
