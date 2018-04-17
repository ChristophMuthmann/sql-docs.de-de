---
title: Prozeduren | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC]
- stored procedures [ODBC], about ODBC stored procedures
- ODBC applications, statements
- statements [ODBC], stored procedures
- ODBC applications, stored procedures
ms.assetid: c64d5f3a-376b-48ef-84f3-b6148ac8600a
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: daa872f40a8b7d5bcbde813ea1c473fd055bcf6e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="procedures"></a>Vorgehensweisen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Eine gespeicherte Prozedur ist ein vorkompiliertes ausführbares Objekt, das eine oder mehrere [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen enthält. Gespeicherte Prozeduren können Ein- und Ausgabeparameter enthalten und auch einen ganzzahligen Rückgabecode ausgeben. Eine Anwendung kann kann mithilfe von Katalogfunktionen verfügbare gespeicherte Prozeduren auflisten.  
  
 ODBC-Anwendungen für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sollten gespeicherte Prozeduren nur mithilfe der direkten Ausführung aufrufen. Beim Verbinden mit früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber implementiert [SQLPrepare-Funktion](http://go.microsoft.com/fwlink/?LinkId=59360) erstellen Sie eine temporäre gespeicherte Prozedur, die dann heißt auf **SQLExecute**. Er fügt mehr Aufwand **SQLPrepare** erstellen Sie eine temporäre gespeicherte Prozedur, die ausschließlich Ruft die gespeicherte Zielprozedur direkt Prozedur das Ziel auszuführen gespeicherte. Selbst bei einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] muss der Aufruf eines zusätzlichen Roundtrips durch das Netzwerk vorbereitet und ein Ausführungsplan, mit dem nur der Ausführungsplan der gespeicherten Prozedur aufgerufen wird, erstellt werden.  
  
 Beim Ausführen einer gespeicherten Prozedur sollten ODBC-Anwendungen die ODBC CALL-Syntax verwenden. Der Treiber ist für die Verwendung eines Remoteprozeduraufrufsmechanismus zum Aufrufen der Prozedur optimiert, sofern die ODBC CALL-Syntax verwendet wird. Dies ist effizienter als der Mechanismus, der verwendet wird, um eine [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE-Anweisung an den Server zu senden.  
  
 Weitere Informationen finden Sie unter [Ausführen von gespeicherten Prozeduren](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Anweisungen & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
