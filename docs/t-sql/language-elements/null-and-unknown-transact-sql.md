---
title: NULL und UNKNOWN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdac1899707b3caa4f4c515324511a47830f2722
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="null-and-unknown-transact-sql"></a>NULL und UNKNOWN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL gibt an, dass der Wert unbekannt ist. Ein null-Wert unterscheidet sich von einem leeren Wert oder NULL-Wert. NULL-Werte sind niemals identisch. Vergleiche zwischen zwei null-Werte, oder ein null-Wert und ein anderer Wert zurückgeben unbekannt, da der Wert jedes NULL unbekannt ist.  
  
 NULL-Werte in der Regel Daten hin, die ist unbekannt oder nicht zutreffend, oder zu einem späteren Zeitpunkt hinzugefügt werden. Beispielsweise ist es möglich, dass der Anfangsbuchstabe des zweiten Vornamens eines Kunden noch nicht bekannt ist, wenn der Kunde eine Bestellung aufgibt.  
  
 Beachten Sie Folgendes im Zusammenhang mit null-Werte aus:  
  
-   Um das Vorhandensein von NULL-Werten in einer Abfrage zu testen, verwenden Sie IS NULL oder IS NOT NULL in der WHERE-Klausel.  
  
-   NULL-Werte können in eine Spalte eingefügt werden, indem NULL explizit in einer INSERT- oder UPDATE-Anweisung, oder indem Sie eine Spalte aus einer INSERT-Anweisung zu verlassen.  
  
-   NULL-Werte können nicht als Informationen verwendet werden, die erforderlich sind, um eine Zeile in einer Tabelle von einer anderen Zeile in einer Tabelle, z. B. Primärschlüssel, oder Informationen, die zum Verteilen von Zeilen, z. B. Verteilung Schlüssel verwendet zu unterscheiden.  
  
 Sind NULL-Werte in den Daten vorhanden, ist es möglich, dass logische Operatoren und Vergleichsoperatoren nicht nur TRUE oder FALSE zurückgeben, sondern ein drittes Ergebnis: UNKNOWN. Diese Notwendigkeit einer dreiwertigen Logik ist die Ursache für zahlreiche Anwendungsfehler. In den folgenden Tabellen wird dargestellt, welche Auswirkungen die Einführung von Vergleichen zwischen NULL-Werten haben kann.  
  
 Die folgende Tabelle zeigt die Ergebnisse des Anwendens eines AND-Operators auf zwei boolesche Operanden, in denen ein Operand gibt NULL zurück.  
  
|Operand 1|Der Operand 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|NULL|FALSE|  
|NULL|NULL|FALSE|  
|FALSE|NULL|FALSE|  
  
 Die folgende Tabelle zeigt die Ergebnisse des Anwendens eines OR-Operators auf zwei boolesche Operanden, in denen ein Operand gibt NULL zurück.  
  
|Operand 1|Der Operand 2|Ergebnis|  
|---------------|---------------|------------|  
|TRUE|NULL|TRUE|  
|NULL|NULL|UNKNOWN|  
|FALSE|NULL|UNKNOWN|  
  
## <a name="see-also"></a>Siehe auch  
 [UND &#40; Transact-SQL &#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [ODER &#40; Transact-SQL &#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NICHT &#40; Transact-SQL &#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IST NULL &#40; Transact-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
