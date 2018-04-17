---
title: ODBC-Konvertierer Unterschlüssel | Microsoft Docs
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
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ede16122078aa53d3eeb0799678537746e3fcf12
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-translators-subkey"></a>ODBC-Konvertierer Unterschlüssel
Die Werte unter dem Unterschlüssel ODBC Konvertierer Liste der installierten Übersetzer. Das Format dieser Werte wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|*Konvertierer-"DESC"*|REG_SZ|**Installiert**|  
  
 Die *Konvertierer Desc* Name vom Entwickler Konvertierer definiert ist.  
  
 Nehmen Sie beispielsweise an, dass ein Benutzer das Microsoft® Code Seite Konvertierungsprogramm und eine benutzerdefinierte ASCII zu EBCDIC-Konvertierer installiert sind. Die Werte unter dem Unterschlüssel ODBC Konvertierer könnte folgendermaßen aussehen:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
