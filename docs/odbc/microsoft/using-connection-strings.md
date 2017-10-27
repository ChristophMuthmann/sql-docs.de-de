---
title: Verwenden von Verbindungszeichenfolgen | Microsoft Docs
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
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f95e0a2ed1b93e89254e5e357cc3889dc5817554
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-connection-strings"></a>Verwenden von Verbindungszeichenfolgen
Sie können eine Verbindungszeichenfolge für die Verbindung mit einer Visual FoxPro-Datenquelle verwenden.  
  
 Um eine Verbindung herzustellen, auf die Datenquelle TasTrade und überschreiben die aktuelle Einstellung der exklusive mit der Datenquelle zugeordnet ist, verwenden Sie z. B. die Zeichenfolge:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Eine Liste der Attribut-Schlüsselwörter und der Werte, die Sie in der Verbindungszeichenfolge enthalten können, finden Sie unter [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Eine vollständige Erläuterung der Syntax für Verbindungszeichenfolgen finden Sie unter [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) in der *ODBC Programmer's Reference*.

