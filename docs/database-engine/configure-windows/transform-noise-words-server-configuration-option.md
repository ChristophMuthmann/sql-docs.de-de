---
title: "Füllwörtertransformation (Serverkonfigurationsoption) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: beb60bb5bc681c45ed465b9b75e7f5834cd39a0f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="transform-noise-words-server-configuration-option"></a>Füllwörtertransformation (Serverkonfigurationsoption)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Verwenden Sie Serverkonfigurationsoption **Füllwörtertransformation** (Transform Noise Words), um eine Fehlermeldung zu unterdrücken, wenn durch Füllwörter, bei denen es sich um [Stoppwörter](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)handelt, verursacht wird, dass ein boolescher Vorgang für eine Volltextabfrage 0 Zeilen zurückgibt. Diese Option ist für Volltextabfragen nützlich, bei denen das CONTAINS-Prädikat verwendet wird, in dem boolesche oder NEAR-Operationen Füllwörter enthalten. Eine Beschreibung der möglichen Werte finden Sie in der folgenden Tabelle:  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|0|Füllwörter (oder Stoppwörter) werden nicht umgewandelt. Wenn eine Volltextabfrage Füllwörter enthält, gibt die Abfrage 0 Zeilen zurück und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] löst eine Warnung aus. Dies ist das Standardverhalten.<br /><br /> Hinweis: Bei der Warnung handelt es sich um eine Laufzeitwarnung. Die Warnung wird daher nicht ausgegeben, wenn die Volltextklausel in der Abfrage nicht ausgeführt wird. Bei lokalen Abfragen wird auch bei mehreren Volltextabfrageklauseln immer nur eine einzige Warnung ausgegeben. Bei Remoteabfragen übermittelt der Verbindungsserver u. U. den Fehler nicht, und die Warnung wird daher möglicherweise nicht ausgegeben.|  
|1|Füllwörter (oder Stoppwörter) werden umgewandelt. Sie werden ignoriert, und der Rest der Abfrage wird ausgewertet.<br /><br /> Wenn Füllwörter in einem NEAR-Begriff angegeben werden, werden sie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt. Das Füllwort `is` wird beispielsweise aus `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`entfernt, und die Suchabfrage wird in `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`umgewandelt. Beachten Sie, dass `CONTAINS(<column_name>, 'NEAR(hello,is)')` einfach in `CONTAINS(<column_name>, hello)` umgewandelt werden würde, da es nur einen gültigen Suchbegriff gibt.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Auswirkungen der Einstellung von „Füllwörtertransformation“  
 In diesem Abschnitt wird das Verhalten von Abfragen, die das Füllwort „`the`“ enthalten, unter den alternativen Einstellungen von **Füllwörtertransformation**dargestellt.  Für die Beispielzeichenfolgen für Volltextabfragen wird angenommen, dass sie in einer Tabellenzeile mit den folgenden Daten ausgeführt werden: `[1, "The black cat"]`.  
  
> [!NOTE]  
>  Alle derartigen Szenarien können eine Füllwortwarnung generieren.  
  
-   Mit „Füllwörtertransformation“ auf „0“ festgelegt:  
  
    |Abfragezeichenfolge|Ergebnis|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Keine Ergebnisse (das Verhalten ist für "`the`" AND "`cat`" genau gleich.)|  
    |"`cat`" NEAR "`the`"|Keine Ergebnisse (das Verhalten ist für "`the`" NEAR "`cat`" genau gleich.)|  
    |"`the`" AND NOT "`black`"|Keine Ergebnisse|  
    |"`black`" AND NOT "`the`"|Keine Ergebnisse|  
  
-   Mit „Füllwörtertransformation“ auf „1“ festgelegt:  
  
    |Abfragezeichenfolge|Ergebnis|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Treffer für Zeile mit ID 1|  
    |"`cat`" NEAR "`the`"|Treffer für Zeile mit ID 1|  
    |"`the`" AND NOT "`black`"|Keine Ergebnisse|  
    |"`black`" AND NOT "`the`"|Treffer für Zeile mit ID 1|  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird **Füllwörtertransformation** auf `1`festgelegt.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
  
