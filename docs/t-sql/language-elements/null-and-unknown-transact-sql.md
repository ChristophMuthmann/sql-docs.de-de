---
title: NULL und UNKNOWN (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ff35786ca071881f25922ed955301fc8e38af2bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="null-and-unknown-transact-sql"></a>NULL und UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL weist darauf hin, dass der Wert unbekannt ist. Ein NULL-Wert unterscheidet sich von einem leeren Wert oder dem Wert Null (0). NULL-Werte sind niemals identisch. Vergleiche zwischen zwei NULL-Werten oder zwischen einem NULL-Wert und einem anderen Wert geben ein nicht definiertes Ergebnis zurück, da der Wert jedes NULL-Werts unbekannt ist.  
  
 Durch NULL-Werte werden grundsätzlich unbekannte, nicht anwendbare oder solche Daten angegeben, die später hinzugefügt werden. Beispielsweise ist es möglich, dass der Anfangsbuchstabe des zweiten Vornamens eines Kunden noch nicht bekannt ist, wenn der Kunde eine Bestellung aufgibt.  
  
 Beachten Sie folgende Hinweise zu NULL-Werten:  
  
-   Um das Vorhandensein von NULL-Werten in einer Abfrage zu testen, verwenden Sie IS NULL oder IS NOT NULL in der WHERE-Klausel.  
  
-   NULL-Werte können in eine Spalte eingefügt werden, indem NULL explizit in einer INSERT- oder UPDATE-Anweisung angegeben oder indem eine Spalte aus einer INSERT-Anweisung weggelassen wird.  
  
-   NULL-Werte können nicht für Informationen verwendet werden, die für die Unterscheidung einer Zeile in einer Tabelle von einer anderen Zeile in einer Tabelle erforderlich sind, beispielsweise Primärschlüssel, oder für Informationen, mit denen Zeilen verteilt werden, wie etwa Verteilungsschlüssel.  
  
 Sind NULL-Werte in den Daten vorhanden, ist es möglich, dass logische Operatoren und Vergleichsoperatoren nicht nur TRUE oder FALSE zurückgeben, sondern ein drittes Ergebnis: UNKNOWN. Diese Notwendigkeit einer dreiwertigen Logik ist die Ursache für zahlreiche Anwendungsfehler. Logische Operatoren in einem booleschen Ausdruck, der UNKNOWN-Elemente enthält, geben UNKNOWN zurück, es sei denn, das Ergebnis des Operators hängt nicht vom UNKNOWN-Ausdruck ab. Die folgenden Tabellen enthalten Beispiele für dieses Verhalten.  
  
 Die folgende Tabelle zeigt die Ergebnisse der Anwendung eines AND-Operators auf zwei boolesche Ausdrücke, in denen ein Ausdruck UNKNOWN zurückgibt.  
  
|Ausdruck 1|Ausdruck 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 Die folgende Tabelle zeigt die Ergebnisse der Anwendung eines OR-Operators auf zwei boolesche Ausdrücke, in denen ein Ausdruck UNKNOWN zurückgibt.  
  
|Ausdruck 1|Ausdruck 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [AND &#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR &#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT &#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
