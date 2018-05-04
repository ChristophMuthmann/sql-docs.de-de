---
title: SQLRemoveDefaultDataSource Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 072f599ad63e7b624478e66030356367d944fd17
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0, veraltet  
  
 **Zusammenfassung**  
 In ODBC 3.0 die **SQLRemoveDefaultDataSource** Funktion wurde durch einen Aufruf von ersetzt [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) mit einer *häufigsten* ODBC_REMOVE_DEFAULT_DSN Argument. Wenn eine ODBC 2.*.x* Installationsprogramm ruft diese Funktion, die ODBC-Installationsprogramm ordnen sie Sie die folgenden **SQLConfigDataSource** aufrufen:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
