---
title: SQLSTATE (ODBC-Fehlercodes) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 40ead7f1822e63f7445669cedcd47f0ef90f988b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC-Fehlercodes)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSTATE stellt ausführliche Informationen über die Ursache einer Warnung oder eines Fehlers bereit. Für Fehler, die in der Datenquelle auftreten erkannt und zurückgegeben werden, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ordnet die zurückgegebene systemeigene Fehlernummer dem entsprechenden SQLSTATE. Wenn eine systemeigene Fehlernummer keine ODBC-Fehlercode zum zuweisen, werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt SQLSTATE 42000 ("Syntaxfehler oder zugriffsverletzung"). Für Fehler, die vom Treiber erkannt werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber generiert die entsprechenden SQLSTATE-Code.  
  
 Weitere Informationen über Statusfehlercodes finden Sie unter folgenden Themen:  
  
-   [Anhang A: ODBC-Fehlercodes](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE-Zuordnungen](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Siehe auch  
 [Behandlung von Fehlern und Meldungen](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
