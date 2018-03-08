---
title: "Treiberfähiges Verbindungspooling im ODBC-Treiber für SQLServer | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67cb0f520c9e75606c7e1ffcae42d20d87a3d9fb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>Treiberfähiges Verbindungspooling im ODBC-Treiber für SQL Server.
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützt [Treiberfähiges Verbindungspooling](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). Dieses Thema beschreibt die Erweiterungen treiberfähiges Verbindungspooling im Microsoft ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unter Windows:  
  
-   Unabhängig von den Verbindungseigenschaften Verbindungen, bei denen `SQLDriverConnect` wechseln in einen separaten Pool von Verbindungen, verwenden Sie `SQLConnect`.
- Bei Verwendung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Authentifizierung und treiberfähiges Verbindungspooling, verwendet der Treiber nicht die Windows-Benutzer-Sicherheitskontext für den aktuellen Thread um Verbindungen im Pool zu trennen. Das bedeutet, wenn Verbindungen in ihren Parametern für Identitätswechsel-Szenarien unter Windows mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Authentifizierung äquivalent sind und die gleichen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] -Anmeldeinformationen zur Verbindung mit dem Back-End verwenden, können andere Windows-Benutzer möglicherweise den gleichen Pool aus Verbindungen verwenden. Bei Verwendung der Windows-Authentifizierung und des treiberfähigen Verbindungspoolings verwendet der Treiber den aktuellen Sicherheitkontext des Windows-Benutzers für den aktuellen Thread, um Verbindungen im Pool zu trennen. D. h. für Windows-Identitätswechsel-Szenarios teilen sich verschiedene Windows-Benutzer keine Verbindungen, auch wenn die Verbindungen dieselben Parameter verwenden.
- Bei Verwendung von Azure Active Directory und treiberfähiges Verbindungspooling verwendet der Treiber den Wert für die Serverauthentifizierung auch die Mitgliedschaft in einem Verbindungspool zu bestimmen.
  
-   Treiberfähiges Verbindungspooling verhindert, dass eine fehlerhafte Verbindung aus dem Pool zurückgegeben wird.  
  
-   Treiberfähiges Verbindungspooling erkennt treiberspezifische Verbindungsattribute. Wenn eine Verbindung verwendet also `SQL_COPT_SS_APPLICATION_INTENT` auf schreibgeschützt festgelegt ist, ruft diese Verbindung ihren eigenen Verbindungspool.
-   Festlegen der `SQL_COPT_SS_ACCESS_TOKEN` Attribut bewirkt, dass eine Verbindung getrennt "zusammengelegt" werden 
  
Wenn eine der folgenden Verbindungsattribut-IDs oder eines der Schlüsselwörter für Verbindungszeichenfolgen zwischen Ihrer Verbindungszeichenfolge und der in einem Pool zusammengefassten Verbindungszeichenfolge abweicht, verwendet der Treiber eine gepoolte Verbindung. Allerdings ist die Leistung besser, wenn alle Verbindungsattribut-IDs oder Schlüsselwörter für Verbindungszeichenfolgen übereinstimmen. (Um eine Übereinstimmung einer Verbindung im Pool herzustellen, setzt der Treiber das Attribut zurück. Die Leistung wird beeinträchtigt, da ein zusätzlicher Netzwerkaufruf notwendig ist, um die folgenden Parameter zurückzusetzen.)  
  
-    Wenn sich zwei oder mehr der folgenden Verbindungsattribute oder Verbindungsschlüsselwörter unterscheiden, wird keine gepoolte Verbindung verwendet.  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   Gibt es einen Unterschied in einem der folgenden Verbindungsschlüsselwörter zwischen Ihrer Verbindungszeichenfolge und einer gepoolten Verbindungszeichenfolge, wird keine gepoolte Verbindung verwendet.  
  
    |Schlüsselwort|ODBC-Treiber 13|ODBC-Treiber 11|
    |-|-|-|
    |`Address`|ja|ja|
    |`AnsiNPW`|ja|ja|
    |`App`|ja|ja|
    |`ApplicationIntent`|ja|ja|  
    |`Authentication`|ja|Nein|
    |`ColumnEncryption`|Ja|Nein|
    |`Database`|Ja|ja|
    |`Encrypt`|ja|ja|  
    |`Failover_Partner`|ja|ja|
    |`FailoverPartnerSPN`|ja|ja|
    |`MARS_Connection`|ja|ja|
    |`Network`|ja|ja|
    |`PWD`|ja|ja|
    |`Server`|ja|ja|
    |`ServerSPN`|ja|ja|
    |`TransparentNetworkIPResolution`|ja|ja|
    |`Trusted_Connection`|ja|ja|
    |`TrustServerCertificate`|ja|ja|
    |`UID`|ja|ja|
    |`WSID`|ja|ja|
    
- Gibt es einen Unterschied in einem der folgenden Verbindungsattribute zwischen Ihrer Verbindungszeichenfolge und einer gepoolten Verbindungszeichenfolge, wird keine gepoolte Verbindung verwendet.  
  
    |Attribut|ODBC-Treiber 13|ODBC-Treiber 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|ja|ja|
    |`SQL_ATTR_PACKET_SIZE`|ja|ja|
    |`SQL_COPT_SS_ANSI_NPW`|ja|ja|
    |`SQL_COPT_SS_ACCESS_TOKEN`|ja|Nein|
    |`SQL_COPT_SS_AUTHENTICATION`|Ja|Nein|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|Ja|ja|
    |`SQL_COPT_SS_BCP`|ja|ja|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|ja|Nein|
    |`SQL_COPT_SS_CONCAT_NULL`|Ja|ja|
    |`SQL_COPT_SS_ENCRYPT`|ja|ja|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|ja|ja|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|ja|ja|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|ja|ja|
    |`SQL_COPT_SS_MARS_ENABLED`|ja|ja|
    |`SQL_COPT_SS_OLDPWD`|ja|ja|
    |`SQL_COPT_SS_SERVER_SPN`|ja|ja|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|ja|ja|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|ja|ja|
    |`SQL_COPT_SS_TNIR`|ja|Nein|
 
-   Der Treiber kann die folgenden Verbindungsschlüsselwörter und Attribute zurücksetzen und anpassen, ohne einen zusätzlichen Netzwerkaufruf durchzuführen. Der Treiber setzt diese Parameter zurück, um sicherzustellen, dass die Verbindung keine falschen Informationen enthält.  
  
     Diese Schlüsselwörter werden nicht berücksichtigt, wenn der Treiber-Manager versucht, eine Übereinstimmung zwischen Ihrer Verbindung und einer Verbindung im Pool zu erzielen. (Auch wenn Sie einen dieser Parameter ändern, kann eine vorhandene Verbindung wiederverwendet werden. Der Treiber wird je nach Bedarf die Optionen zurücksetzen.) Diese Attribute können clientseitig ohne einen zusätzliche Netzwerkaufruf zurückgesetzt werden.  
  
    |Schlüsselwort|ODBC-Treiber 13|ODBC-Treiber 11|  
    |-|-|-|  
    |`AutoTranslate`|ja|ja|
    |`Description`|ja|ja|
    |`MultisubnetFailover`|ja|ja|  
    |`QueryLog_On`|ja|ja|
    |`QueryLogFile`|ja|ja|
    |`QueryLogTime`|ja|ja|
    |`Regional`|ja|ja|
    |`StatsLog_On`|ja|ja|
    |`StatsLogFile`|  ja|ja|
  
     Wenn Sie eine der folgenden Verbindungsattribute ändern, kann eine vorhandene Verbindung wiederverwendet werden.  Der Treiber wird je nach Bedarf den Wert zurücksetzen. Der Treiber kann diese Attribute clientseitig ohne einen zusätzliche Netzwerkaufruf zurücksetzen  
  
    |Attribut|ODBC-Treiber 13|ODBC-Treiber 11|  
    |-|-|-|  
    |Alle Anweisungsattribute|ja|ja|
    |`SQL_ATTR_AUTOCOMMIT`|ja|ja|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  ja|ja|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|ja|ja|
    |`SQL_ATTR_LOGIN_TIMEOUT`|ja|ja|
    |`SQL_ATTR_ODBC_CURSORS`|  ja|ja|
    |`SQL_COPT_SS_PERF_DATA`|ja|ja|
    |`SQL_COPT_SS_PERF_DATA_LOG`|ja|ja|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| ja|ja| 
    |`SQL_COPT_SS_PERF_QUERY`|ja|ja|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|ja|ja|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  ja|ja|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|ja|ja|
    |`SQL_COPT_SS_TRANSLATE`|ja|ja|
    |`SQL_COPT_SS_USER_DATA`|  ja|ja|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|ja|ja|  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
