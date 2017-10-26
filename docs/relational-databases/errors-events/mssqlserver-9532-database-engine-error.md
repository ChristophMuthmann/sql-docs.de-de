---
title: MSSQLSERVER_9532 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c88ac3f700fa2f91a868f7a7fb1590d4119d0cc
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|9532|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Meldungstext|Konvertierungsfehler während des Abfrage-/DML-Vorgangs mit dem Spaltensatz '%.*ls' beim Versuch, den '%ls'-Datentyp für die '%.\*ls'-Spalte in den '%ls'-Datentyp zu konvertieren.|  
  
## <a name="explanation"></a>Erklärung  
Bei einem Spaltensatz handelt es sich um eine nicht typisierte XML-Darstellung, die einige Tabellenspalten mit geringer Dichte in einer strukturierten Ausgabe kombiniert. Wenn Sie Spalten mit geringer Dichte mit dem XML-Spaltensatz einfügen bzw. aktualisieren, werden die Werte, die in die zugrunde liegenden Spalten mit geringer Dichte eingefügt werden, vom **xml**-Datentyp implizit konvertiert. Es wurde ein Wert angegeben, der nicht in den Datentyp der Spalte konvertiert werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
Da der bereitgestellte Wert nicht implizit konvertiert werden konnte, könnte es sich um einen ungültigen Eintrag handeln. Beheben Sie den Fehler, und versuchen Sie es erneut. Wenn der Wert korrekt ist, bearbeiten Sie die Anweisung so, dass die einzelnen Spalten anstelle des gesamten Spaltensatzes verwendet werden. Dadurch können Sie den Wert explizit in den richtigen Datentyp umwandeln.  
  

