---
title: Bezeichner in Anführungszeichen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e74c39ad73357e50c1040e8a90029c0bf65f7b6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="quoted-identifiers"></a>Bezeichner in Anführungszeichen
In einer SQL­Anweisung müssen von Bezeichnern, die Sonderzeichen oder Übereinstimmung Schlüsselwörter in eingeschlossen werden *Anführungszeichen Bezeichner*; Bezeichner eingeschlossen in solche Zeichen werden als bezeichnet *Bezeichnern*(auch bekannt als *Begrenzungsbezeichner* in SQL-92). Beispielsweise wird der "Accounts Payable" Bezeichner in Anführungszeichen in der folgenden **wählen** Anweisung:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Der Grund für Bezeichner ist, die Anweisung analysiert. Wenn "Accounts Payable" nicht in der vorherigen Anweisung in Anführungszeichen gesetzt wurde, würde der Parser z. B. wird davon ausgegangen, dass zwei Tabellen, Konten und Payable, wurden und ein Syntaxfehler, den nicht durch ein Komma getrennt zurückzugeben. Der Bezeichner Anführungszeichen treiberspezifische und wird abgerufen, mit der Option SQL_IDENTIFIER_QUOTE_CHAR **SQLGetInfo**. Die Listen von Sonderzeichen und Schlüsselwörter werden abgerufen, mit den Optionen SQL_SPECIAL_CHARACTERS und SQL_KEYWORDS in **SQLGetInfo**.  
  
 Um sicher zu sein, Angebot interoperable Anwendungen häufig alle Bezeichner mit Ausnahme derjenigen für Pseudospalten, z. B. den Spalte ROWID in Oracle. **SQLSpecialColumns** gibt eine Liste der Pseudospalten zurück. Darüber hinaus treten anwendungsspezifische Beschränkungen, wobei Sonderzeichen in Objektnamen angezeigt werden können, ist es am besten für interoperablen Anwendungen nicht, für die Verwendung von Sonderzeichen in diese Positionen.
