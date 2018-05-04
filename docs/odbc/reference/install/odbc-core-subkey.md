---
title: ODBC Core Unterschlüssel | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8e143a8d5d329fe3eb68185a3ebdf8f7f6cd6b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
