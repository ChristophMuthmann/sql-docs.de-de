---
title: SQLRemoveDefaultDataSource Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed4db21dce5cf5da5234f4906116c93f9a4ea735
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0, veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.0 die **SQLRemoveDefaultDataSource** Funktion wurde durch einen Aufruf von ersetzt [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) mit einer *häufigsten* ODBC_REMOVE_DEFAULT_DSN Argument. Wenn eine ODBC 2.*.x* Installationsprogramm ruft diese Funktion, die ODBC-Installationsprogramm ordnen sie Sie die folgenden **SQLConfigDataSource** aufrufen:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
