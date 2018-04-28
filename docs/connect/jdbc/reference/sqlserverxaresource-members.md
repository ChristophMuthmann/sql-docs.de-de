---
title: SQLServerXAResource-Elemente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b4d0dd8ffe48528b439447a59e2540950c34527d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource-Elemente
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  In den folgenden Tabellen enthalten die Elemente, die verfügbar gemacht werden, indem Sie die [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Klasse.  
  
## <a name="constructors"></a>Konstruktoren  
 Keine.  
  
## <a name="fields"></a>Felder  
  
|Name|Description|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|Hierdurch werden eng verkoppelte XA-Transaktionen ermöglicht, die unterschiedliche XA-Verzweigungstransaktions-IDs (XIDs) aber dieselbe globale Transaktions-ID (GTRID) aufweisen.|  
  
## <a name="inherited-fields"></a>Geerbte Felder  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN, TMFAIL, TMJOIN, TMNOFLAGS, TMONEPHASE, TMRESUME, TMSTARTRSCAN, TMSUCCESS, TMSUSPEND, XA_OK, XA_RDONLY|  
  
## <a name="methods"></a>Methoden  
  
|Name|Description|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|Führt einen Commit für die globale Transaktion vom angegebenen Xid-Objekt.|  
|[Ende](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|Beendet die für einen Transaktionszweig durchgeführte Arbeit.|  
|[vergessen](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|Teilt dem Ressourcen-Manager mit, dass eine heuristisch abgeschlossene Transaktionsverzweigung ignoriert (vergessen) werden kann.|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|Ruft den aktuellen Transaktionstimeoutwert für diesen [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt.|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|Bestimmt, ob das Zielobjekt dargestellte Ressourcen-Manager-Instanz identisch mit der Ressourcen-Manager-Instanz vom angegebenen XAResource-Objekt dargestellt wird.|  
|[Vorbereiten](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|Fordert an, dass der Ressourcen-Manager für einen Commit der Transaktion der Transaktion, durch das angegebene Objekt der Xid vorzubereiten.|  
|[Wiederherstellen](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|Ruft eine Liste vorbereiteter Transaktionszweige von einem Ressourcen-Manager ab.|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|Fordert an, dass der Ressourcen-Manager für die für den Transaktionszweig durchgeführte Arbeit ein Rollback ausführt.|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|Legt den aktuellen Transaktionstimeoutwert für diesen [SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) Objekt.|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Startet die Arbeit für einen transaktionszweig angegeben, in dem Xid-Objekt.|  
  
## <a name="inherited-methods"></a>Geerbte Methoden  
  
|Klasse geerbt von:|Methoden|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLServerXAResource-Klasse](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
