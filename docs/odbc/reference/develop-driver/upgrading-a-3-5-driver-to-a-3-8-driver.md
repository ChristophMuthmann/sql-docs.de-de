---
title: Aktualisieren eines 3.5 Treibers einem 3.8 Treiberpaket | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5dc39bf1203a06d571bf188e17e7066e53167415
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>Aktualisieren eines 3.5 Treibers 3.8-Treiber
Dieses Thema enthält Richtlinien und Überlegungen zum Upgrade von eines ODBC 3.5-Treibers auf ODBC 3.8-Treiber.  
  
##### <a name="version-numbers"></a>Versionsnummern  
 Die folgenden Richtlinien beziehen sich auf Versionsnummern:  
  
-   Ein Treiber sollten SQL_OV_ODBC3_80 für SQL_ATTR_ODBC_VERSION, Rückgabe von SQL_ERROR für andere Werte als SQL_OV_ODBC2 SQL_OV_ODBC3 und SQL_OV_ODBC3_80 unterstützen. Zukünftige Versionen der Treiber-Manager werden davon ausgegangen, dass ein Treiber eine ODBC-Kompatibilitätsstufe unterstützt, wenn der Treiber gibt SQL_SUCCESS aus zurück [SQLSetEnvAttr-Funktion](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
-   Ein Version 3.8 Treiber sollte 03.80 aus zurückgeben **SQLGetInfo** Wenn SQL_DRIVER_ODBC_VER an übergeben *Infotyp*. Jedoch ältere Treiber-Manager, darunter auch in früheren Versionen von Microsoft Windows enthalten sind, behandelt den Treiber als Treiber Version 3.5, und eine Warnung ausgeben.  
  
     In Windows 7 ist der Treiber-Manager-Version 03.80. In Windows 8 ist die Treiber-Manager-Version über die SQLGetInfo SQL_DM_VER 03.81 (*Infotyp* Parameter). SQL_ODBC_VER meldet die Version als 03.80 in Windows 7 und Windows 8.  
  
##### <a name="driver-specific-c-data-types"></a>Treiber-spezifischen C-Datentypen  
 Ein Treiber kann C-Datentypen angepasst haben, wenn es mit einer Version 3.8-ODBC-Anwendung funktioniert. (Weitere Informationen finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) Allerdings besteht keine Notwendigkeit für einen 3.8 Treiber implementiert alle treiberspezifischen C-Typen zur Verfügung. Aber der Treiber sollte noch die bereichsüberprüfung C-Typen ausführen. der Treiber-Manager wird nicht für 3.8 Treiber nachholen. Um Treiberentwicklung zu erleichtern, kann der Wert der Treiber bestimmte, C-Datentyp im folgenden Format definiert werden:  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnose Typen und Attribute  
 Wenn Sie einen neuen Treiber zu entwickeln, sollten Sie den treiberspezifischen Bereich für Datentypen, Deskriptor Typen Informationstypen, Diagnose Typen und Attribute verwenden. Treiberspezifische Bereiche und deren Basistyp Werte werden im erläutert [Treiber-spezifische Datentypen, Deskriptor Typen Informationstypen, Diagnosetypen und Attribute](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
##### <a name="connection-pooling"></a>Verbindungspooling  
 Für eine bessere Verwaltung des Verbindungspoolings ODBC 3.8 führt das Verbindungsattribut SQL_ATTR_RESET_CONNECTION in **SQLSetConnectAttr**. SQL_RESET_CONNECTION_YES ist der einzige gültige Wert für dieses Attribut. SQL_ATTR_RESET_CONNECTION wird festgelegt werden, kurz bevor der Treiber-Manager eine Verbindung im Verbindungspool, ermöglichen die Treiber setzt zu den weiteren Verbindungsattributen auf ihre Standardwerte zurückgesetzt.  
  
 Um unnötige Kommunikation mit dem Server zu vermeiden, kann ein Treiber verzögern, das Verbindungsattribut, bis der nächsten Kommunikation mit dem Remoteserver zurückgesetzt wird, nachdem die Verbindung aus dem Pool wiederverwendet wird.  
  
 Beachten Sie, dass SQL_ATTR_RESET_CONNECTION nur bei der Kommunikation zwischen der Treiber-Manager und einen Treiber verwendet wird. Dieses Attribut kann nicht direkt eine Anwendung festgelegt werden. Alle Treiber der Version 3.8 sollte dieses Verbindungsattribut implementieren.  
  
##### <a name="streamed-output-parameters"></a>Gestreamte Output-Parameter  
 ODBC 3.8-Version führt gestreamte Output-Parameter, eine stärker skalierbare Möglichkeit zum Abrufen der Output-Parameter. (Weitere Informationen finden Sie unter [Abrufen von Ausgabeparametern mit SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) Um dieses Feature zu unterstützen, ein Treiber sollte festgelegt SQL_GD_OUTPUT_PARAMS im Rückgabewert bei SQL_GETDATA_EXTENSIONS ist die *Infotyp* in einer **SQLGetInfo** aufrufen. Unterstützung für SQL-Typ mit gestreamte Output-Parameter muss in der Treiber implementiert werden. Der Treiber-Manager generiert keinen Fehler für eine ungültige SQL-Typ. Die SQL-Typen, gestreamte Output-Parameter unterstützen, in der Treiber definiert ist.  
  
 Ein Treiber sollte SQL_ERROR zurück, wenn die Anwendung verwendet **SQLGetData** um einen Parameter abzurufen, die nicht den Parameter zurückgegebenes identisch ist **SQLParamData**.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>Asynchrone Ausführung für Verbindungsvorgänge (Abrufmethode)  
 Ein Treiber kann asynchrone Unterstützung für verschiedene Verbindungsvorgänge aktivieren.  
  
 Ab Windows 7, ODBC unterstützt der Abrufmethode (Weitere Informationen finden Sie unter [asynchrone Ausführung (Methode abrufen)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md). Es ist nicht erforderlich für einen ODBC-Treiber Version 3.8 zum Implementieren asynchroner Vorgänge auf Verbindungshandles. Auch wenn ein Treiber asynchroner Vorgänge auf Verbindungshandles nicht implementiert wird, sollte der Treiber noch die SQL_ASYNC_DBC_FUNCTIONS implementieren *Infotyp* inventurüberprüfung **SQL_ASYNC_DBC_NOT_CAPABLE**.  
  
 Wenn Vorgänge asynchron-Verbindung aktiviert sind, wird die Ausführungszeit eines Vorgangs für die Verbindung die Gesamtzeit für alle wiederholte Aufrufe. Wenn die letzte Aufruf erfolgt wiederholt, nachdem die gesamte Zeit den Wert festlegen, indem das Verbindungsattribut SQL_ATTR_CONNECTION_TIMEOUT überschritten und der Vorgang nicht beendet hat wurde, wird der Treiber gibt SQL_ERROR zurück, und einen Diagnosedatensatz mit SQLState HYT01 protokolliert und die Meldung "Verbindungstimeout abgelaufen". Es wurde kein Timeout auf, wenn der Vorgang abgeschlossen.  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle-Funktion  
 Unterstützt ODBC 3.8 [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md), der verwendet wird, sowohl Verbindungs- und -Vorgänge "Abbrechen". Ein Treiber, der unterstützt **SQLCancelHandle** müssen die Funktion exportieren. Ein Treiber sollte nicht abgebrochen werden, synchrone oder asynchrone Verbindungsfunktion, die ausgeführt wird, wenn die Anwendung aufruft, **SQLCancel** oder **SQLCancelHandle** für ein Anweisungshandle. Auf ähnliche Weise ein Treiber sollte nicht abgebrochen werden, jede Anweisung für den synchronen bzw. asynchronen-Funktion, die ausgeführt wird, wenn eine Anwendung ruft **SQLCancelHandle** auf dem Verbindungshandle. Darüber hinaus sollte ein Treiber nicht den browsing Vorgang abbrechen (**SQLBrowseConnect** wird SQL_NEED_DATA zurückgegeben.) Wenn die Anwendung aufruft, **SQLCancelHandle** auf dem Verbindungshandle. In diesen Fällen sollte ein Treiber HY010 "Funktionsreihenfolge" zurückgeben.  
  
 Es ist nicht notwendig, beide unterstützen das **SQLCancelHandle** und asynchronverbindung Vorgänge zur gleichen Zeit. Ein Treiber kann asynchrone Verbindungsvorgänge unterstützen, aber nicht **SQLCancelHandle**, oder umgekehrt.  
  
##### <a name="suspended-connections"></a>Unterbrochene Verbindungen  
 Der ODBC 3.8-Treiber-Manager kann eine Verbindung in Zustand "angehalten" versetzt. Eine Anwendung ruft **SQLDisconnect** der Verbindung zugeordnete Ressourcen freizugeben. In diesem Fall sollten ein Treiber so viele Ressourcen wie möglich freizugeben, ohne die Überprüfung des Status der Verbindung. Weitere Informationen zum Zustand "angehalten" finden Sie unter [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
##### <a name="driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling  
 ODBC in Windows 8 ermöglicht, dass Treiber Pool Verbindungsverhalten angepasst wird. Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
##### <a name="asynchronous-execution-notification-method"></a>Asynchrone Ausführung (Benachrichtigungsmethode)  
 ODBC 3.8 unterstützt die Benachrichtigungsmethode für asynchrone Vorgänge, verfügbar unter Windows 8 ab. Weitere Informationen finden Sie unter [asynchrone Ausführung (Benachrichtigungsmethode)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft gelieferten ODBC-Treiber](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [What's New in ODBC 3.8 (Neues in ODBX 3.8)](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
