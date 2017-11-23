---
title: "ODBC Core Unterschlüssel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85c4e842ef48f412696c4a0c851480915f5d9b27
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-core-subkey"></a>ODBC Core Unterschlüssel
Der Wert unter dem Unterschlüssel ODBC Core bietet der Verwendungszähler für die Kernkomponenten (Treiber-Manager, Cursorbibliothek, Installer DLL usw.). Das Format dieses Werts wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD-WERT|*count*|  
  
 Nehmen Sie beispielsweise an, dass durch die Setupprogramme für drei verschiedenen Anwendungen und zwei verschiedenen Treiber die ODBC-Kernkomponenten installiert wurden. Der Wert unter dem Unterschlüssel ODBC Core würde folgendermaßen lauten:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
