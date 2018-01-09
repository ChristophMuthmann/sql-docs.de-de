---
title: SQLSTATE (ODBC-Fehlercodes) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- ODBC error handling, cause information
- messages [ODBC], cause information
- SQLSTATEs
- errors [ODBC], cause information
ms.assetid: 84cce528-edb0-473f-a85f-3eb87fbe2cf3
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fa0f6a84463aa331c2650ed106e322c6a15fdf9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC-Fehlercodes)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  SQLSTATE stellt ausführliche Informationen über die Ursache einer Warnung oder eines Fehlers bereit. Für Fehler, die in der Datenquelle auftreten erkannt und zurückgegeben werden, indem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber ordnet die zurückgegebene systemeigene Fehlernummer dem entsprechenden SQLSTATE. Wenn eine systemeigene Fehlernummer keine ODBC-Fehlercode zum zuweisen, werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt SQLSTATE 42000 ("Syntaxfehler oder zugriffsverletzung"). Für Fehler, die vom Treiber erkannt werden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber generiert die entsprechenden SQLSTATE-Code.  
  
 Weitere Informationen über Statusfehlercodes finden Sie unter folgenden Themen:  
  
-   [Anhang A: ODBC-Fehlercodes](http://go.microsoft.com/fwlink/?LinkId=89356)  
  
-   [SQLSTATE-Zuordnungen](http://go.microsoft.com/fwlink/?LinkId=89355)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Behandlung von Fehlern und Meldungen](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
