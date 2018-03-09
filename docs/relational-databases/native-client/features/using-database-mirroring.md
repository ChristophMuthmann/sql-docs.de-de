---
title: Die Verwendung der Datenbankspiegelung | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63e362b186725b5e9adf15721fcfd4154be3148d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="using-database-mirroring"></a>Verwenden der Datenbankspiegelung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]Verwendung [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] stattdessen.  
  
 Die in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] eingeführte Datenbankspiegelung ist eine Lösung zum Erhöhen der Datenbankverfügbarkeit und Datenredundanz. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client beinhaltet eine implizite Unterstützung für die datenbankspiegelung, sodass der Entwickler nicht notwendigerweise Code schreiben oder andere Aktionen ausführen, nachdem es für die Datenbank konfiguriert wurde.  
  
 Datenbankspiegelung, die für eine Datenbanken einzeln implementiert wird, befindet sich eine Kopie einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Produktionsdatenbank auf einem Standbyserver. Bei dem Server handelt es sich je nach Konfiguration und Status der Datenbankspiegelungs-Sitzung um einen unmittelbar betriebsbereiten oder einfach betriebsbereiten Standbyserver. Ein unmittelbar betriebsbereiter Standbyserver unterstützt schnelles Failover ohne Verlust von Transaktionen mit ausgeführtem Commit, und ein betriebsbereiter Standbyserver unterstützt das Erzwingen eines Diensts (bei möglichem Datenverlust).  
  
 Die Produktionsdatenbank wird aufgerufen, die *Prinzipaldatenbank*, und die Standbykopie wird aufgerufen, die *Spiegeldatenbank*. Die Prinzipaldatenbank und Spiegeldatenbank müssen, befinden sich auf separaten Instanzen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Serverinstanzen), und sie sollten auf unterschiedlichen Computern befinden, wenn möglich.  
  
 Die produktionsserverinstanz wird aufgerufen, die *Prinzipalserver*, kommuniziert mit der standbyserverinstanz wird aufgerufen, die *Spiegelserver*. Prinzipal-und Spiegelserver fungieren als Partner in einer datenbankspiegelungs- *Sitzung*. Wenn der Prinzipalserver ausfällt, kann der Spiegelserver seine Datenbank vornehmen, in der Prinzipaldatenbank mithilfe des so genannten *Failover*. Beispiel: Partner_A und Partner_B sind zwei Partnerserver. Die Prinzipaldatenbank befindet sich anfänglich auf dem Prinzipalserver Partner_A und die Spiegeldatenbank auf dem Spiegelserver Partner_B. Wenn Partner_A offline geht, kann die Datenbank auf Partner_B ein Failover ausführen, um zur aktuellen Prinzipaldatenbank zu werden. Sobald Partner_A wieder mit der Sitzung verbunden ist, übernimmt er wieder die Rolle des Spiegelservers und seine Datenbank wird zur Spiegeldatenbank.  
  
 Alternative Konfigurationen für die Datenbankspiegelung bieten unterschiedliche Leistungs- und Datensicherheitsstufen und unterstützen unterschiedliche Formen des Failover. Weitere Informationen finden Sie unter [Datenbankspiegelung &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 Beim Angeben des Spiegeldatenbanknamens ist es möglich, einen Alias zu verwenden.  
  
> [!NOTE]  
>  Informationen zu ersten Verbindungsversuche und Versuche der erneuten Herstellen einer Verbindung mit einer gespiegelten Datenbank finden Sie unter [Verbinden von Clients mit einer Datenbank-Spiegelungssitzung &#40; SQLServer &#41; ](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>Überlegungen zur Programmierung  
 Wenn auf dem Prinzipaldatenbankserver ein Fehler auftritt, empfängt die Clientanwendung als Antwort auf API-Aufrufe Fehlermeldungen. Dadurch wird angezeigt, dass die Verbindung zur Datenbank unterbrochen ist. Wenn dieser Fall eintritt, gehen alle Datenbankänderungen, für die kein Commit ausgeführt wurde, verloren und für die aktuelle Transaktion wird ein Rollback durchgeführt. Dann sollte die Anwendung die Verbindung beenden (oder das Datenquellobjekt freigeben) und erneut herstellen. Die Verbindung wird transparent zur Spiegeldatenbank umgeleitet, die jetzt als Prinzipalserver fungiert.  
  
 Wenn eine Verbindung hergestellt wurde, teilt der Prinzipalserver die Identität seines Failoverpartners, der bei einem Failover einspringt, dem Client mit. Wenn eine Anwendung versucht, nach dem Failover des Prinzipalservers eine Verbindung aufzubauen, kennt der Client die Identität des Failoverpartners nicht. Um Clients die Möglichkeit zu geben, in dieser Situation Abhilfe zu schaffen, können sie die Identität des Failoverpartners mithilfe einer Initialisierungseigenschaft und eines zugeordneten Schlüsselworts für die Verbindungszeichenfolge selbst angeben. Das Clientattribut wird nur in dieser Situation verwendet; wenn der Prinzipalserver verfügbar ist, wird es nicht verwendet. Wenn der vom Client angegebene Failoverpartnerserver nicht auf einen Server verweist, der als Failoverpartner fungiert, wird die Verbindung vom Server abgewiesen. Um es Anwendungen zu ermöglichen, sich an Konfigurationsänderungen anzupassen, kann die Identität des tatsächlichen Failoverpartners durch Überprüfung des Attributs nach dem Verbindungsaufbau bestimmt werden. Sie sollten die Partnerinformationen zwischenspeichern, um die Verbindungszeichenfolge zu aktualisieren, oder eine Wiederholungsstrategie für den Fall entwerfen, dass der erste Versuch des Verbindungsaufbaus fehlschlägt.  
  
> [!NOTE]  
>  Sie müssen die von einer Verbindung zu verwendende Datenbank explizit angeben, wenn Sie diese Funktion in einem DSN, einer Verbindungszeichenfolge oder einer/m Verbindungseigenschaft/-attribut verwenden möchten. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client versucht sonst nicht, bei einem Fehler zur Partnerdatenbank zu wechseln.  
>   
>  Die Spiegelung ist eine Funktion der Datenbank. Anwendungen, die mehrere Datenbanken verwenden, sind möglicherweise nicht in der Lage, diese Funktion zu nutzen.  
>   
>  Außerdem erfolgt bei den Servernamen keine Unterscheidung nach Groß-/Kleinschreibung, bei Datenbanknamen jedoch schon. Sie müssen daher auf die Übereinstimmung der Groß-/Kleinschreibung in DSNs und Verbindungszeichenfolgen achten.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt die datenbankspiegelung durch Verbindungen und Verbindungszeichenfolgen-Attribute. Die SSPROP_INIT_FAILOVERPARTNER-Eigenschaft wurde dem DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz hinzugefügt wurde und die **FailoverPartner** -Schlüsselwort ist ein neues Verbindungszeichenfolgen-Attribut für DBPROP_INIT_PROVIDERSTRING. Weitere Informationen finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Der failovercache wird beibehalten, solange der Anbieter, also geladen wird bis **CoUninitialize** wird so lange wie die Anwendung einen Verweis auf ein Objekt, das von verwaltet hat oder aufgerufen der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, wie z. B. ein Datenquellenobjekt.  
  
 Weitere Informationen zu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützten datenbankspiegelung finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt die datenbankspiegelung durch Verbindungen und Verbindungszeichenfolgen-Attribute. Insbesondere das SQL_COPT_SS_FAILOVER_PARTNER-Attribut wurde für die Verwendung mit der [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) und [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) Funktionen; und die **von Failover_Partner** Schlüsselwort wurde als ein neues Verbindungszeichenfolgen-Attribut hinzugefügt.  
  
 Der Failovercache wird beibehalten, solange der Anwendung mindestens ein Umgebungshandle zugeordnet ist. Umgekehrt geht er verloren, wenn die Zuordnung des letzten Umgebungshandles aufgehoben wird.  
  
> [!NOTE]  
>  Der ODBC-Treiber-Manager wurde verbessert, um die Spezifikation des Failoverservernamens zu unterstützen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Funktionen](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Verbinden von Clients mit einer Datenbank-Spiegelungssitzung (SQL Server)](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
