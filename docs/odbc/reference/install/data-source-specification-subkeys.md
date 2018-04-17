---
title: Datenquellen-Spezifikation Unterschlüssel | Microsoft Docs
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
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f3080d85b2c01491d94ecb75b956d6c67bc061b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="data-source-specification-subkeys"></a>Data Source-Spezifikation Unterschlüssel
Jede Datenquelle, die in der ODBC-Datenquellen-Unterschlüssel aufgeführt verfügt über einen Unterschlüssel selbst. Dieser Unterschlüssel verfügt über den gleichen Namen wie der entsprechende Wert unter dem Unterschlüssel ODBC-Datenquellen. Die Werte unter dieser Unterschlüssel müssen die Treiber-DLL auflisten und listet möglicherweise eine Beschreibung der Datenquelle. Wenn der Treiber Konvertierer unterstützt, kann der Name von einem Standard-Konvertierer, das Standard-Konvertierungs-DLL und die Standardoption für die Übersetzung Werteliste. Die Werteliste möglicherweise auch andere Informationen, die vom Treiber bei der Herstellung einer Verbindung mit der Datenquelle erforderlich sind. Der Treiber möglicherweise z. B. einen Servernamen, Datenbanknamen oder Schemaname.  
  
 Die Formate der Werte sind wie in der folgenden Tabelle gezeigt. Nur der Treiber-Wert ist erforderlich.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|Description|REG_SZ|*description*|  
|Treiber|REG_SZ|*Treiber-DLL-Pfad*|  
|TranslationDLL|REG_SZ|*Konvertierer-DLL-Pfad*|  
|TranslationName|REG_SZ|*Konvertierer-name*|  
|TranslationOption|REG_SZ|*Translation-option*|  
|*OPT-Wert-name*|*OPT-Werttyp*|*OPT-Wertdaten*|  
  
 Nehmen wir beispielsweise an, der SQL Server-Treiber benötigt den Servernamen und ein Flag für OEM-ANSI-Konvertierung und die Server und OEMTOANSI Werte für diese definiert. Angenommen Sie auch, dass die Datenquelle für die Inventur der Microsoft® Code Seite Translator verwendet, um zwischen dem Windows®-Latin 1 (1250) und Codepages Mehrsprachig (850) übersetzt. Die Werte unter dem Unterschlüssel Inventur könnte folgendermaßen aussehen:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
