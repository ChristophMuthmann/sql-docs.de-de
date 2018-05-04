---
title: Beschränkungen in Word reserviert | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 010546fe5d0d987443fb4deebc4409cb5e867085
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keyword-limitations"></a>Reserviertes Schlüsselwort Einschränkungen

Vermeiden Sie die Verwendung der reservierten ODBC-Schlüsselwörter als Bezeichner in der SQL-Tabellen oder verbundenen Objekte. Wenn eine ungerade Groß-/Kleinschreibung tritt auf, wobei ein reserviertes Schlüsselwort als Bezeichner verwendet werden muss, müssen Sie den Bezeichner umschließen, mit ein Paar von *Backticks* ('). Einen anderen Namen für *Hochkomma als Escapezeichen* ist *Anführungszeichen Sichern*.

Reserviertes Schlüsselwort Einschränkung gilt auch für alle Kurzform der reservierten Schlüsselwörter.

Eine Liste der reservierten ODBC-Schlüsselwörter finden Sie unter:

- [Reservierte ODBC-Schlüsselwörter](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords).

- In der *ODBC Programmer's Reference Guide*, finden Sie unter [Anhang C: SQL-Grammatik](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar).

