---
title: Treibermanager-Verbindungspooling | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd838afbe2391e679c58537bc9547b7d4138e07c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="driver-manager-connection-pooling"></a>Treibermanager-Verbindungspooling
Verbindungspooling ermöglicht einer Anwendung eine Verbindung aus einem Pool von Verbindungen verwendet werden, die nicht für jede Verwendung neu eingerichtet werden müssen. Sobald eine Verbindung erstellt und in einem Pool platziert wurde, kann eine Anwendung diese Verbindung wiederverwenden, ohne die vollständige Verbindungsprozess auszuführen.  
  
 Eine gepoolte Verbindung können sich deutliche Leistungssteigerungen ergeben, da den Aufwand beim Herstellen einer Verbindung von Anwendungen gespeichert werden können. Dies kann besonders wichtige für Anwendungen der mittleren Ebene, die über ein Netzwerk verbunden oder für Anwendungen, die wiederholt eine Verbindung herstellen und trennen möchten, z. B. Internetanwendungen sein.  
  
 Zusätzlich zu den Leistungssteigerungen ermöglicht der Verbindungspooling-Architektur eine Umgebung und die zugeordneten Verbindungen von mehreren Komponenten in einem einzelnen Prozess verwendet werden. Dies bedeutet, dass es sich bei eigenständigen Komponenten in demselben Prozess miteinander interagieren können, ohne Berücksichtigung der jeweils anderen. Eine Verbindung in einem Verbindungspool kann wiederholt von mehreren Komponenten verwendet werden.  
  
> [!NOTE]  
>  Verbindungspooling kann von einer ODBC-Anwendung ODBC 2. Fehler verwendet werden. *x* Verhalten, solange die Anwendung aufrufen kann *SQLSetEnvAttr*. Wenn Verbindungspooling verwenden, muss die Anwendung nicht SQL-Anweisungen, die die Datenbank oder im Kontext der Datenbank, z. B. veränderte ändern ausgeführt der \< *Datenbank ** Namen*>, welche Änderungen des Katalogs, in eine die Datenquelle.  
  
 Ein ODBC-Treiber muss vollständig threadsicheren und Verbindungen dürfen keine Threadaffinität um Verbindungspooling zu unterstützen. Dies bedeutet, dass der Treiber ist in der Lage, einen Aufruf für jeden Thread zu einem beliebigen Zeitpunkt zu behandeln und Herstellen einer Verbindung in einem Thread, um die Verbindung in einem anderen Thread verwendet und um auf ein dritter Thread zu trennen.  
  
 Der Verbindungspool wird vom Treiber-Manager verwaltet. Verbindungen werden aus dem Pool entnommen, wenn die Anwendung aufruft, **SQLConnect** oder **SQLDriverConnect** und an den Pool zurückgegeben, wenn die Anwendung aufruft **SQLDisconnect**. Die Größe des Pools wird dynamisch basierend auf die angeforderte Ressource Zuordnungen. Verkleinert wird basierend auf das Timeout bei Inaktivität: Wenn eine Verbindung für eine bestimmte Zeitspanne inaktiv ist (es ist nicht im verwendet wurde eine Verbindung) aus dem Pool entfernt. Die Größe des Pools wird nur durch Arbeitsspeicher Einschränkungen und auf dem Server beschränkt.  
  
 Der Treiber-Manager bestimmt, ob eine bestimmte Verbindung in einem Pool soll, entsprechend die übergebenen Argumente verwendet werden **SQLConnect** oder **SQLDriverConnect**, und gemäß der Verbindungsattribute festgelegt, nachdem die Verbindung zugewiesen wurde.  
  
 Beim pooling von Verbindungen wird der Treiber-Manager muss es in der Lage, um festzustellen, ob eine Verbindung vor der Übergabe, die Verbindung weiterhin ausgeführt wird. Andernfalls bleibt der Treiber-Manager auf Ausgabe die inaktiven Verbindung mit der Anwendung nach einem vorübergehenden Netzwerkausfall. Ein neues Verbindungsattribut definiert wurde, in ODBC 3.*.x*: SQL_ATTR_CONNECTION_DEAD. Dies ist eine schreibgeschützte Verbindung-Attribut, das SQL_CD_TRUE oder SQL_CD_FALSE zurückgibt. Der Wert SQL_CD_TRUE bedeutet, dass die Verbindung unterbrochen, wurde während der Wert SQL_CD_FALSE bedeutet, dass die Verbindung noch aktiv ist. (Entsprechen, das mit früheren Versionen der ODBC-Treiber können auch das Attribut unterstützt.)  
  
 Ein Treiber muss diese Option implementieren, effizient oder es ist das Verbindungspooling-Leistung beeinträchtigt. Insbesondere sollte ein Aufruf zum Abrufen dieses Verbindungsattribut keinen Roundtrip zum Server verursachen. Stattdessen sollte ein Treiber nur den letzten bekannten Status der Verbindung zurück. Die Verbindung ist inaktiv, wenn die letzte Reiseroute an den Server fehlgeschlagen ist und nicht inaktiv, wenn die letzte Reiseroute erfolgreich war.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Verbindung verloren geht (über SQL_ATTR_CONNECTION_DEAD gemeldet), zerstört der ODBC-Treiber-Manager diese Verbindung durch Aufrufen von SQLDisconnect im Treiber. Neue verbindungsanforderungen können eine verwendbare Verbindung im Pool nicht gefunden werden. Schließlich kann der Treiber-Manager, eine neue Verbindung, vorausgesetzt, dass der Pool leer ist.  
  
 Um einem Verbindungspool zu verwenden, führt eine Anwendung die folgenden Schritte aus:  
  
1.  Ermöglicht es, Verbindungspooling durch Aufrufen von **SQLSetEnvAttr** Attributs Umgebung SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER oder SQL_CP_ONE_PER_HENV festlegen. Dieser Aufruf muss erfolgen, bevor die Anwendung die freigegebene Umgebung weist pooling ist für die Verbindung aktiviert werden. Das Umgebungshandle im Aufruf **SQLSetEnvAttr** sollte auf Null, wodurch SQL_ATTR_CONNECTION_POOLING auf Prozessebene-Attribut festgelegt werden. Wenn das Attribut auf SQL_CP_ONE_PER_DRIVER festgelegt ist, wird eine einzelne Verbindungspools für jeden Treiber unterstützt. Wenn eine Anwendung mit vielen Treiber und einige Umgebungen funktioniert, dies effizienter möglicherweise weniger Vergleiche erforderlich sein können. Wenn der Satz an SQL_CP_ONE_PER_HENV, einem einzelnen Verbindungspool für jede Umgebung unterstützt wird. Wenn eine Anwendung mit vielen Umgebungen und einige Treiber funktioniert, dies effizienter möglicherweise weniger Vergleiche erforderlich sein können. Verbindungspooling ist deaktiviert, indem SQL_ATTR_CONNECTION_POOLING auf SQL_CP_OFF festlegen.  
  
2.  Ordnet eine Umgebung durch den Aufruf **SQLAllocHandle** mit der *HandleType* -Argument auf SQL_HANDLE_ENV festgelegt. Eine implizite freigegebenen Umgebung kann von die Umgebung, die durch diesen Aufruf zugeordnet ist, werden, weil Verbindungspooling aktiviert wurde. Die Umgebung verwendet werden, ist nicht festgelegt, jedoch erst **SQLAllocHandle** mit einem *HandleType* SQL_HANDLE_DBC auf, die für diese Umgebung aufgerufen wird.  
  
3.  Ordnet eine Verbindung durch Aufrufen von **SQLAllocHandle** mit *InputHandle* auf SQL_HANDLE_DBC auf, festgelegt und die *InputHandle* festlegen, um das Umgebungshandle zugeordnet Verbindungspooling. Der Treiber-Manager versucht, eine vorhandene Umgebung finden, die die Umgebung Attribute, die von der Anwendung festgelegten entspricht. Wenn keine solche Umgebung vorhanden ist, wird eine mit einer Verweisanzahl von 1 (werden vom Treiber-Manager) erstellt. Wenn eine übereinstimmende freigegebene Umgebung gefunden wird, die Umgebung an die Anwendung zurückgegeben, und dessen Verweiszähler erhöht. (Die tatsächliche Verbindung zu verwendende richtet sich nicht auf die vom Treiber-Manager bis **SQLConnect** oder **SQLDriverConnect** aufgerufen wird.)  
  
4.  Aufrufe **SQLConnect** oder **SQLDriverConnect** zum Herstellen die Verbindung. Der Treiber-Manager verwendet die Verbindungsoptionen im Aufruf **SQLConnect** (oder die Schlüsselwörter im Aufruf **SQLDriverConnect**) und die Verbindungsattribute festlegen, nach der Zuordnung der Verbindung zu Ermitteln Sie, welche Verbindung im Pool verwendet werden soll.  
  
    > [!NOTE]  
    >  Wie eine angeforderte Verbindung eine gepoolte Verbindung zugeordnet ist, wird vom Attribut SQL_ATTR_CP_MATCH Umgebung bestimmt. Weitere Informationen finden Sie unter [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     ODBC-Anwendungen mithilfe von Verbindungspooling sollten Aufrufen [CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307) während der anwendungsinitialisierung und [CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310) beim Schließen der Anwendung.  
  
5.  Aufrufe **SQLDisconnect** Wenn die Verbindung nicht mehr benötigen. Die Verbindung an den Verbindungspool zurückgegeben, und für die Wiederverwendung verfügbar.  
  
 Eine ausführliche Erläuterung finden Sie unter [in der Microsoft Data Access Components Pooling](http://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Überlegungen für Verbindungspooling  
 Eine der folgenden Aktionen mithilfe eines SQL-Befehls (und nicht über die ODBC-API) ausführen und beeinflussen kann, der Zustand der Verbindung zu unerwarteten Problemen kommen, wenn Verbindungspooling aktiviert ist:  
  
-   Öffnen einer Verbindung, und ändern die Standarddatenbank.  
  
-   Mithilfe der SET-Anweisung keine konfigurierbaren Optionen (einschließlich SET ROWCOUNT, ANSI_NULL IMPLICIT_TRANSACTIONS, SHOWPLAN, Statistiken, TEXTSIZE und DateFormat-Einstellung) ändern.  
  
-   Erstellen von temporären Tabellen und gespeicherten Prozeduren.  
  
 Wenn eine dieser Aktionen außerhalb der ODBC-API ausgeführt werden, erben die nächste Person, die die Verbindung verwendet automatisch die vorherigen Einstellungen, Tabellen oder Prozeduren.  
  
> [!NOTE]  
>  Erwarten Sie keine bestimmte Einstellungen in den Zustand der Verbindung vorhanden sein. Sollten Sie immer den Verbindungsstatus in Ihrer Anwendung festgelegt werden und stellen Sie sicher, dass die Anwendung alle nicht verwendeten Verbindungs-pooling Einstellungen entfernt.  
  
## <a name="driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling  
 Ab Windows 8 kann ein ODBC-Treiber Verbindungen im Pool effizienter verwenden. Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Herstellen einer Verbindung mit einer Quelle oder Treiber](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [In der Microsoft Data Access Components Pooling](http://go.microsoft.com/fwlink/?LinkId=120776)
