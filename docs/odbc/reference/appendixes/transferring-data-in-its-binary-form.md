---
title: Übertragen von Daten in seiner binären Form | Microsoft Docs
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
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 489ce7115a312a8f2d171d839393b9ead695ef48
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="transferring-data-in-its-binary-form"></a>Übertragen von Daten in seiner binären Form
Eine Anwendung kann problemlos Daten (in der internen Form, die von einem angegebenen DBMS verwendet) zwischen zwei Datenquellen übertragen, die das gleiche DBMS und die Hardwareplattform verwenden. Für einen bestimmten Daten müssen die SQL-Datentypen in den Quell- und Datenquellen identisch sein. Die C-Datentyp ist SQL_C_BINARY.  
  
 Wenn die Anwendung aufruft, **SQLFetch**, **SQLFetchScroll**, oder **SQLGetData** zum Abrufen der Daten aus der Datenquelle für die Quelle ruft der Treiber die Daten aus den Daten ab Datenquelle aus, und überträgt, ohne Konvertierung zu einem Speicherort vom Typ SQL_C_BINARY. Wenn die Anwendung aufruft, **SQLBulkOperations**, **SQLExecute**, **SQLExecDirect**, **SQLPutData oder SQLSetPos** zum Senden von Daten Die Zieldatenquelle der Treiber Ruft die Daten aus den Speicherort ab und überträgt, ohne Konvertierung auf die Zieldatenquelle.  
  
> [!NOTE]  
>  Anwendungen, die für die Übertragung von Daten (mit Ausnahme der binären Daten) auf diese Weise sind nicht interoperabel zwischen DBMS.  
  
 **SQLCopyDesc** kann zum Kopieren von zeilenbindungen von Quell-DBMS Parameter-Bindungen in der Ziel-DBMS verwendet werden.
