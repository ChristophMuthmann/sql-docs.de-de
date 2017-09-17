---
title: "ALTER Tabelle Anweisung Einschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c50ea6550e9dfb255c87886e4e0375240bcd2ae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="alter-table-statement-limitations"></a>ALTER Tabelle Anweisung Einschränkungen
Wann wird die dBASE- oder Paradox-Treiber verwendet, um, sobald ein Index erstellt wurde und ein neuer Datensatz hinzugefügt, die Struktur der Tabelle durch die ALTER TABLE-Anweisung geändert werden kann, es sei denn, der Index gelöscht wird und der Inhalt der Tabelle gelöscht werden.  
  
 ALTER TABLE-Anweisungen werden für die Treiber für Microsoft Excel- oder Textdateien nicht unterstützt.  
  
> [!NOTE]  
>  Wenn Sie den Paradox-Treiber verwenden, ohne das Datenbankmodul Borland implementieren, sind ALTER TABLE-Anweisungen nicht unterstützt. nur lesen und Anfügen-Anweisungen sind zulässig.
