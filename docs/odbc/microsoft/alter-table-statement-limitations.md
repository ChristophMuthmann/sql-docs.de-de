---
title: ALTER Tabelle Anweisung Einschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06af545611da90d51ad0fc82136a4cb1ecc3984c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-table-statement-limitations"></a>ALTER Tabelle Anweisung Einschränkungen
Wann wird die dBASE- oder Paradox-Treiber verwendet, um, sobald ein Index erstellt wurde und ein neuer Datensatz hinzugefügt, die Struktur der Tabelle durch die ALTER TABLE-Anweisung geändert werden kann, es sei denn, der Index gelöscht wird und der Inhalt der Tabelle gelöscht werden.  
  
 ALTER TABLE-Anweisungen werden für die Treiber für Microsoft Excel- oder Textdateien nicht unterstützt.  
  
> [!NOTE]  
>  Wenn Sie den Paradox-Treiber verwenden, ohne das Datenbankmodul Borland implementieren, sind ALTER TABLE-Anweisungen nicht unterstützt. nur lesen und Anfügen-Anweisungen sind zulässig.
