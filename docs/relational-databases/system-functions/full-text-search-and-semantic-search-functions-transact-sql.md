---
title: Volltextsuche und semantische Suche Funktionen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 70e9351761332d534f612cfe77d20c301a9423cb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>Funktionen für Volltextsuche und semantische Suche (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die Systemfunktionen für die Volltextsuche und die semantische Suche beschrieben.  
  
## <a name="full-text-search-functions"></a>Funktionen für die Volltextsuche  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für jene Spalten zurück, die präzise oder weniger präzise (fuzzy) Übereinstimmungen mit einzelnen Wörtern bzw. Ausdrücken aufweisen, die den Abstand von Wörtern oder gewichtete Treffer enthalten.  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 Gibt eine Tabelle mit 0 (null), einer oder mehreren Zeilen für alle Spalten mit Werten, die die Bedeutung und nicht nur mit dem genauen Wortlaut des Texts in der angegebenen entsprechen *Freetext_string*.  
  
## <a name="semantic-search-functions"></a>Funktionen für die semantische Suche  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für die Schlüsselausdrücke zurück, die in der angegebenen Tabelle Spalten zugeordnet sind.  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 Gibt eine Tabelle mit 0 (null), einer oder mehreren Zeilen von Schlüsselausdrücken allgemeine in zwei Dokumenten (einem Quelldokument und einem verglichenen Dokument), deren Inhalt semantisch ähnlich ist.  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 Gibt eine Tabelle mit keiner, einer oder mehreren Zeilen für die Spalten zurück, deren Inhalt einem angegebenen Dokument semantisch ähnlich ist.  
  
  
