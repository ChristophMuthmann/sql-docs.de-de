---
title: "ODBC-Konvertierer Unterschlüssel | Microsoft Docs"
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
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dfc34daa6236fa7187c27a204ee16cc47a0de7b0
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

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
