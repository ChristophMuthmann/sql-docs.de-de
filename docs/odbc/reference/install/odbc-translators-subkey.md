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
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a6c59901d3e784f1ab845da595c84a4e74a0129
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
