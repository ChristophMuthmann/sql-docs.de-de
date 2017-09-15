---
title: "ODBC-Treiber-Unterschlüssel | Microsoft Docs"
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 21b151256f93d77cd0efecedfa8eef2ddcd6482b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-drivers-subkey"></a>ODBC-Treiber-Unterschlüssel
Die Werte unter der ODBC-Treiber-Unterschlüssel Auflisten der installierten Treiber. Das Format dieser Werte wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|*Treiber-Beschreibung*|REG_SZ|**Installiert**|  
  
 Die *treiberbeschreibung* Name wird vom Treiber Entwickler definiert. Normalerweise ist der Name des DBMS an, mit dem Treiber verknüpft sind.  
  
 Nehmen Sie z. B. an, dass Treiber für formatierte Textdateien und SQL Server installiert wurden. Die Werte unter dem Unterschlüssel ODBC-Treibern möglicherweise:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
