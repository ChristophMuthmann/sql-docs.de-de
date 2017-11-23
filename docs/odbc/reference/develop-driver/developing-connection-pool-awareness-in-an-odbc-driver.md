---
title: Entwickeln von Verbindungspool wissen in eine ODBC-Treiber | Microsoft Docs
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
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 678d44bb439804246b84a7f8d60f59be45a6dce0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Entwickeln von Verbindungspool wissen in eine ODBC-Treiber
In diesem Artikel werden die Details der Entwicklung von eines ODBC-Treibers, der enthält Informationen darüber, wie der Treiber Connection pooling-Dienste bieten sollte.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling aktivieren  
 Ein Treiber, muss die folgenden Funktionen von ODBC Service Provider Interface (SPI) implementieren:  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Finden Sie unter [ODBC Service Provider Interface (SPI) Verweis](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) für Weitere Informationen.  
  
 Ein Treiber muss auch die folgenden vorhandenen Funktionen implementieren, sodass die treiberfähiges Verbindungspooling aktiviert werden kann:  
  
|Funktion|Zusätzliche Funktionalität|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Unterstützung für die neue Handle: SQL_HANDLE_DBC_INFO_TOKEN (siehe Beschreibung unten).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Unterstützung der neuen Gruppe nur Verbindungsattribut: SQL_ATTR_DBC_INFO_TOKEN für das Zurücksetzen der Verbindung (siehe Beschreibung unten).|  
  
> [!NOTE]  
>  Veraltete Funktionen wie z. B. **SQLError** und **SQLSetConnectOption** werden für treiberfähiges Verbindungspooling nicht unterstützt.  
  
## <a name="the-pool-id"></a>Die Anwendungspool-ID  
 Die Anwendungspool-ID ist eine Länge Zeiger-treiberspezifische-ID eine bestimmte Gruppe von Verbindungen dargestellt, das Synonym verwendet werden kann. Wenn eine Reihe von Verbindungsinformationen, sollten ein Treiber schnell die entsprechenden Pool-ID hergeleitet werden können  
  
 Die Anwendungspool-ID sollte z. B. die Serverinformationen für Namen und die Anmeldeinformationen codieren. Der Datenbankname ist jedoch nicht erforderlich, da ein Treiber möglicherweise wiederverwenden einer Verbindung, und ändern Sie die Datenbank in weniger Zeit als eine neue Verbindung herstellen können.  
  
 Ein Treiber sollten einen Satz von Schlüsselattributen, definieren die Pool-ID umfassen Der Wert dieser Schlüssel Attribute kann aus Verbindungsattribute, Verbindungszeichenfolge und DSN stammen. Für den Fall, dass alle Konflikte, die in diesen Quellen vorhanden sind, sollte die vorhandene, treiberspezifische zur konfliktlösung für Abwärtskompatibilität verwendet werden.  
  
 Der Treiber-Manager verwendet einen anderen Pool für die anderen Pool IDs. Alle Verbindungen im gleichen Pool können wiederverwendet werden. Der Treiber-Manager wird eine Verbindung mit einem anderen Pool-ID nie wiederverwendet werden.  
  
 Treiber sollte daher eine eindeutigen Anwendungspool-ID für jede Gruppe von Verbindungen mit dem gleichen Wert in ihren definierten Schlüsselattribute zuweisen. Wenn ein Treiber die gleichen Pool-ID für zwei Verbindungen mit verschiedenen Werten in den wichtigsten Attributen verwendet, wird der Treiber-Manager weiterhin den gleichen Pool Einsatzort (der Treiber-Manager hat keinerlei wissen über die treiberspezifischen Schlüsselattribute). Dies bedeutet, dass der Treiber an den Treiber-Manager zu melden, die eine Verbindung mit einem anderen Satz von Schlüsselattributen nicht innerhalb von wiederverwendbaren [SQLRateConnection Funktion](../../../odbc/reference/syntax/sqlrateconnection-function.md). Dies kann die Leistung reduzieren, und dies wird nicht empfohlen.  
  
 Der Treiber-Manager wird eine Verbindung aus einem anderen Treiber Umgebung zugeordnet werden, auch wenn alle Verbindungsinformationen entspricht nicht wiederverwendet werden. Der Treiber-Manager verwenden einen anderen Pool für andere Umgebung ab, auch wenn Verbindungen die gleiche Pool-ID Aus diesem Grund ist die Pool-ID für ihre Umgebung Treiber lokal.  
  
 Die Funktion zum Abrufen der Anwendungspool-ID aus dem Treiber ist [SQLGetPoolID Funktion](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>Die Bewertung der Verbindung  
 Im Vergleich zum Herstellen einer neuen Verbindung erhalten eine bessere Leistung Sie durch einige Verbindungsinformationen (z. B.-Datenbank) in eine gepoolte Verbindung zurücksetzen. Daher sollten Sie nicht den Datenbanknamen in der Menge von Schlüsselattributen sein. Andernfalls können Sie einen separaten Pool für jede Datenbank, die möglicherweise nicht gut in Mid-Tier-Anwendungen, lassen, an denen Kunden verschiedene verschiedene Verbindungszeichenfolgen verwenden.  
  
 Wenn Sie eine Verbindung, die einige übereinstimmende Attribut verfügt wiederzuverwenden, sollten Sie die nicht übereinstimmende Attribute basierend auf der neuen anwendungsanforderung zurücksetzen, so, dass die zurückgegebene Verbindung identisch mit der anwendungsanforderung (siehe die Erläuterung des Attributs SQL_ATTR _DBC_INFO_TOKEN in [Funktion SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=59368)). Zurücksetzen dieser Attribute kann jedoch die Leistung verringern. Zurücksetzen einer Datenbank erfordert z. B. einen Netzwerkaufruf an Server. Aus diesem Grund Wiederverwenden einer Verbindungs, die vollkommen verglichen wird, sofern verfügbar.  
  
 Eine Bewertung-Funktion in der Treiber kann eine vorhandene Verbindung mit einer neuen verbindungsanforderung auswerten. Beispielsweise kann der Treiber-Bewertung-Funktion ermitteln:  
  
-   Wenn die vorhandene Verbindung mit der Anforderung perfekt verglichen wird.  
  
-   Wenn nur einige bedeutungslose Konflikte, z. B. Verbindungstimeout, die keine Kommunikation mit dem Server auftreten zurückgesetzt benötigen.  
  
-   Wenn es einige nicht übereinstimmende Attribute, die erforderlich ist eine Kommunikation mit dem Server gibt zurückgesetzt, aber würde weiterhin eine bessere Leistung als eine neue Verbindung herzustellen.  
  
-   Wenn der nicht übereinstimmenden für ein Attribut, die sehr zeitaufwändig aufgetreten zurückgesetzt wird (der Entwickler des Treibers möglicherweise empfiehlt es sich durch Hinzufügen dieses Attributs in den Satz von Schlüsselattributen, die verwendet wird, um die Pool-ID zu generieren).  
  
 Eine Bewertung zwischen 0 und 100 ist möglich, wobei 0 bedeutet, dass nicht wieder verwendet werden können und 100 bedeutet, dass perfekt abgeglichen. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) ist die Funktion für die Bewertung einer Verbindungs.  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>Neue Handle der ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Unterstützung von treiberfähiges Verbindungspooling, benötigt der Treiber Verbindungsinformationen, um die Pool-ID zu berechnen. Der Treiber benötigt auch Informationen zu Verbindungen mit neuen verbindungsanforderungen mit Verbindungen im Pool zu vergleichen.  Wenn keine Verbindung im Pool wiederverwendet werden kann, wurde der Treiber zum Herstellen einer neuen Verbindungs, die Verbindungsinformationen-masterdatenbankzugriff erforderlich ist.  
  
 Da Verbindungsinformationen aus mehreren Quellen (Verbindungszeichenfolge Verbindungsattribute und DSN) stammen kann, müssen der Treiber möglicherweise analysieren die Verbindungszeichenfolge und lösen Sie den Konflikt zwischen diesen Quellen in jeder der obigen Funktionsaufruf.  
  
 Aus diesem Grund wird ein neues Handle der ODBC-eingeführt: SQL_HANDLE_DBC_INFO_TOKEN. Mit SQL_HANDLE_DBC_INFO_TOKEN muss ein Treiber nicht zum Analysieren der Verbindungszeichenfolge und mehr als einmal Lösen von Konflikten in Verbindungsinformationen. Da dies eine treiberspezifische Datenstruktur ist, der Treiber Daten wie Verbindungsinformationen speichern und Anwendungspool-ID  
  
 Dieses Handle ist nur als eine Schnittstelle zwischen der Treiber-Manager und Treiber verwendet. Eine Anwendung kann dieses Handle nicht direkt zuordnen.  
  
 Das Handle des übergeordneten dieses Handle ist vom Typ SQL_HANDLE_ENV auf, was bedeutet, dass der Treiber die Umgebungsinformationen aus dem HENV Handle während der Auflösung von Verbindung Informationen abrufen kann.  
  
 Wenn sie eine neue verbindungsanforderung empfängt, wird der Treiber-Manager ein Handle vom Typ SQL_HANDLE_DBC_INFO_TOKEN zuweisen, zum Speichern von Verbindungsinformationen, nachdem bestätigt, dass der Treiber Verbindungspool Awareness unterstützt. Wenn Sie fertig sind, mit dem Handle (jedoch vor der Rückgabe wird einige Rückgabecodes als SQL_STILL_EXECUTING aus [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) oder [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), der Treiber-Manager wird das Handle freigegeben. Das Handle ist daher nach dem Aufruf der SQLAllocHandle erstellt und nach dem Aufruf der SQLFreeHandle zerstört. Der Treiber-Manager wird sichergestellt, das Handle vor dem Freigeben von seiner zugeordnete HENV freigegeben wird (Wenn [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) oder [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) gibt einen Fehler zurück).  
  
 Der Treiber sollte die folgenden Funktionen, um den neuen Handletyp SQL_HANDLE_DBC_INFO_TOKEN akzeptieren ändern:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 Der Treiber-Manager wird sichergestellt, dass mehrere Threads dasselbe Handle SQL_HANDLE_DBC_INFO_TOKEN nicht gleichzeitig verwendet werden. Daher kann die Synchronisierungsmodell dieser Anforderung innerhalb des Treibers sehr einfach sein. Der Treiber-Manager nimmt eine Sperre für die Umgebung vor dem zuordnen und befreien SQL_HANDLE_DBC_INFO_TOKEN.  
  
 Der Treiber-Manager **SQLAllocHandle** und **SQLFreeHandle** dieser neuen Handletyp nicht akzeptiert.  
  
 SQL_HANDLE_DBC_INFO_TOKEN enthalten möglicherweise vertrauliche Informationen wie Anmeldeinformationen. Aus diesem Grund sollten ein Treiber sicher Speicherpuffers deaktivieren (mit [SecureZeroMemory](http://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)), enthält die vertrauliche Informationen vor dem Freigeben von diesem Handle mit **SQLFreeHandle**. Wenn eine Anwendung Umgebungshandle geschlossen wird, werden alle zugehörigen Verbindungspools geschlossen.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Treiber-Manager-Verbindungspool Bewertung Algorithmus  
 Dieser Abschnitt beschreibt den Algorithmus Bewertung für Treibermanager-Verbindungspooling. Entwickler können den gleichen Algorithmus für die Abwärtskompatibilität implementieren. Dieser Algorithmus möglicherweise nicht das beste aus. Sie sollten dies verfeinern Algorithmus Basis Ihrer Implementierung (andernfalls, es besteht kein Grund, um diese Funktion zu implementieren).  
  
 Der Treiber-Manager wird eine ganzzahlige Bewertung zwischen 0 und 100, die für jede Verbindung aus dem Pool zurückgegeben. 0 bedeutet, dass die Verbindung kann nicht wiederverwendet werden, und 100 an eine perfekte Übereinstimmung. Angenommen Sie, die verbindungsanforderung hRequest ist und die vorhandene Verbindung aus dem Pool als hCandidate benannt ist. Wenn eine der folgenden Bedingungen auf "false" festgelegt ist, kann die poolverbindung hCandidate für hRequest wiederverwendet werden (der Treiber-Manager weist eine Bewertung von 0).  
  
-   hCandidate und hRequest stammen aus UNICODE-API (z. B. sqldriverconnectw durchzuführen) oder ANSI-API (z. B. sqldriverconnecta durchzuführen). (Unicode-Treiber können ein anderes Verhalten angegebenen ANSI-API und UNICODE-API (Siehe das Verbindungsattribut SQL_ATTR_ANSI_APP).)  
  
-   hCandidate und hRequest werden von der gleichen Funktion erstellt. SQLDriverConnect oder SQLConnect.  
  
-   Die Verbindungszeichenfolge verwendet, um hCandidate öffnen sollten hRequest, identisch sein, wenn SQLDriverConnect verwendet wird.  
  
-   Der ServerName oder DSN, Benutzername und Kennwort verwendet, um hCandidate öffnen sollte identisch mit dem hRequest geöffnet, wenn SQLConnect verwendet wird.  
  
-   Die Sicherheits-ID (SID) des aktuellen Threads sollte identisch sein, wie die SID verwendet, um hCandidate zu öffnen.  
  
-   Für Treiber ist teuer, eintragen und austragen (siehe die Erläuterung der SQL_DTC_TRANSITION_COST in [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), Wiederverwenden von *hRequest* eine zusätzliche Eintragung oder Unenlistment nicht erforderlich.  
  
 Die folgende Tabelle zeigt die Bewertung Zuweisung für verschiedene Szenarien.  
  
|Vergleich auf Verbindungsattribute zwischen gepoolte Verbindung und die Anforderung|Keine Eintragung / Unenlistment|Erfordert zusätzliche Eintragung / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Katalog (SQL_ATTR_CURRENT_CATALOG) unterscheidet.|60|50|  
|Einige Verbindungsattribute voneinander abweichen, aber Katalog ist gleich|90|70|  
|Alle Verbindungsattribute perfekt abgeglichen.|100|80|  
  
## <a name="sequence-diagram"></a>Sequenzdiagramm  
 Diese Sequenzdiagramm zeigt die grundlegenden pooling Mechanismus, der in diesem Thema beschrieben. Zeigt nur die Verwendung von [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) aber die [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) Fall ähnelt.  
  
 ![Sequenzieren Diagramm](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "Odbc_seq_dia")  
  
## <a name="state-diagram"></a>Zustandsdiagramm  
 Status Abbildung zeigt die Info token Verbindungsobjekt können in diesem Thema beschrieben. Zeigt das Diagramm nur [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) aber die [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) Fall ähnelt. Der Treiber-Manager können aufrufen, da der Treiber-Manager möglicherweise zur Fehlerbehandlung zu einem beliebigen Zeitpunkt [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) für sämtliche Staaten.  
  
 ![Status Diagramm](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "Odbc_state_diagram")  
  
## <a name="see-also"></a>Siehe auch  
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC-Dienstanbieterschnittstelle (Service Provider Interface, SPI) – Referenz](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
