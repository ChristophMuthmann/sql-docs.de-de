---
title: Beschränkungen in Word reserviert | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac61a7aa818ef3593fddc630d5027fbf7e4aa211
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keyword-limitations"></a>Reserviertes Schlüsselwort Einschränkungen

Vermeiden Sie die Verwendung der reservierten ODBC-Schlüsselwörter als Bezeichner in der SQL-Tabellen oder verbundenen Objekte. Wenn eine ungerade Groß-/Kleinschreibung tritt auf, wobei ein reserviertes Schlüsselwort als Bezeichner verwendet werden muss, müssen Sie den Bezeichner umschließen, mit ein Paar von *Backticks* ('). Einen anderen Namen für *Hochkomma als Escapezeichen* ist *Anführungszeichen Sichern*.

Reserviertes Schlüsselwort Einschränkung gilt auch für alle Kurzform der reservierten Schlüsselwörter.

Eine Liste der reservierten ODBC-Schlüsselwörter finden Sie unter:

- [Reservierte ODBC-Schlüsselwörter](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- In der *ODBC Programmer's Reference Guide*, finden Sie unter [Anhang C: SQL-Grammatik](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

