---
title: Fehlermeldungen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
caps.latest.revision: 34
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7f4e2f850e7671af448af6fc6467f9b5886c3ee8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="error-messages"></a>Fehlermeldungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Der Text der Fehlermeldungen von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber befindet sich der *MessageText* Parameter **SQLGetDiagRec**. Die Quelle eines Fehlers wird im Header der Meldung angegeben:  
  
 [Microsoft][ODBC-Treiber-Manager]  
 Diese Fehler werden vom ODBC-Treiber-Manager ausgelöst.  
  
 [Microsoft][ODBC-Cursorbibliothek]  
 Diese Fehler werden von der ODBC-Cursorbibliothek ausgelöst.  
  
 [Microsoft][SQL Server Native Client]  
 Diese Fehler werden ausgelöst, durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber. Wenn keine anderen Knoten entweder mit den Namen einer Netzwerkbibliothek oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vorhanden sind, trat der Fehler im Treiber auf.  
  
 [Microsoft] [SQL Server Native Client] [*Net-Transportname*]  
 Diese Fehler werden ausgelöst, durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Netzwerkbibliothek, in denen *Net-Transportname* ist der Anzeigename des eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client-Netzwerktransports (z. B. Named Pipes, Shared Memory, TCP/IP-Sockets oder VIA). Die restliche Fehlermeldung enthält die aufgerufene Netzwerkbibliotheksfunktion und die von der TDS-Funktion in der zugrunde liegenden Netzwerk-API aufgerufene Funktion. Die *PfNative* mit diesen Fehlern zurückgegebene Fehlercode ist der Fehlercode aus der zugrunde liegenden Netzwerkprotokollstapel.  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 Diese Fehler werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgelöst. Die übrige Fehlermeldung entspricht dem Text der Fehlermeldung aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die *PfNative* mit diesen Fehlern zurückgegebene Code ist die Fehlernummer aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen über eine Liste mit Fehlermeldungen (und ihren Nummern), die von zurückgegeben werden kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter der Beschreibung und den Fehlerspalten Spalten von der **Sysmessages** -Systemtabelle in der **master** Datenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Behandlung von Fehlern und Meldungen](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
