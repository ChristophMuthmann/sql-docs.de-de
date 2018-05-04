---
title: Konvertierer Spezifikation Unterschlüssel | Microsoft Docs
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
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 163add6fac863912f05378f2e799596f3ad41533
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="translator-specification-subkeys"></a>Konvertierer Spezifikation Unterschlüssel
Jede Konvertierer im ODBC-Konvertierer-Unterschlüssel aufgeführt verfügt über einen Unterschlüssel selbst. Dieser Unterschlüssel verfügt über den gleichen Namen wie der entsprechende Wert unter dem Unterschlüssel ODBC Übersetzer. Die Werte unter dieser Unterschlüssel auflisten, die vollständigen Pfade der Übersetzer und Translator-Setup-DLLs und die Verwendungsanzahl der. Die Formate der Werte sind wie in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|Translator|REG_SZ|*Konvertierer-DLL-Pfad*|  
|Setup|REG_SZ|*Setup-DLL-Pfad*|  
|UsageCount|REG_DWORD-WERT|*count*|  
  
 Informationen zu Verwendungszähler finden Sie unter [zählen Verbrauch](../../../odbc/reference/install/usage-counting.md) weiter oben in diesem Abschnitt.  
  
 Anwendungen sollten die Verwendungsanzahl nicht festlegen. ODBC wird dieser Zähler zu verwalten.  
  
 Nehmen wir beispielsweise an das Microsoft Code Seite Konvertierungsprogramm verfügt, eine Übersetzung DLL mit dem Namen Mscpxl32.dll, die in der gleichen DLL, die Funktionen des Konvertierungsprogramms Setup sind und dass das Konvertierungsprogramm drei Mal installiert wurde. Die Werte unter dem Unterschlüssel Microsoft Code Seite Translator könnte folgendermaßen aussehen:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
