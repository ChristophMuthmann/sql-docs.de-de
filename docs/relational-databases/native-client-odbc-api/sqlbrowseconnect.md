---
title: SQLBrowseConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 400097362ec6364d7a7b0d6f13cd3e62bb4d6b87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBrowseConnect** Schlüsselwörter, die kategorisiert werden können in drei Ebenen von Verbindungsinformationen verwendet. In der folgenden Tabelle wird für jedes Schlüsselwort angegeben, ob eine Liste gültiger Werte zurückgegeben wird und ob das Schlüsselwort optional ist.  
  
## <a name="level-1"></a>Ebene 1  
  
|Schlüsselwort|Liste zurückgegeben?|Optional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|DSN|–|Nein|Name der Datenquelle zurückgegebene **SQLDataSources**. Das DSN-Schlüsselwort kann nicht verwendet werden, wenn das DRIVER-Schlüsselwort verwendet wird.|  
|DRIVER|–|Nein|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treibername ist {[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11}. Das DRIVER-Schlüsselwort kann nicht verwendet werden, wenn das DSN-Schlüsselwort verwendet wird.|  
  
## <a name="level-2"></a>Ebene 2  
  
|Schlüsselwort|Liste zurückgegeben?|Optional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|ja|Nein|Name des Servers in dem Netzwerk, auf dem die Datenquelle gespeichert ist. Für den Server kann der Begriff "(local)" eingegeben werden. In diesem Fall kann eine lokale Kopie von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden, auch wenn dies keine vernetzte Version ist.|  
|UID|Nein|ja|Benutzeranmelde-ID.|  
|PWD|Nein|Ja (vom Benutzer abhängig)|Vom Benutzer angegebenes Kennwort.|  
|APP|Nein|ja|Name der aufrufenden Anwendung **SQLBrowseConnect**.|  
|WSID|Nein|ja|Workstation-ID. Dies ist normalerweise der Netzwerkname des Computers, auf dem die Anwendung ausgeführt wird.|  
  
## <a name="level-3"></a>Ebene 3  
  
|Schlüsselwort|Liste zurückgegeben?|Optional?|Description|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|ja|ja|Name der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank.|  
|LANGUAGE|ja|ja|Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendete Landessprache.|  
  
 **SQLBrowseConnect** ignoriert die Werte der Schlüsselwörter DATABASE und LANGUAGE, die in den ODBC-Datenquellendefinitionen gespeichert. Wenn die Datenbank oder in der Verbindungszeichenfolge angegebene Sprache übergeben **SQLBrowseConnect** ist ungültig, **SQLBrowseConnect** gibt SQL_NEED_DATA sowie die Verbindungsattribute der Ebene 3.  
  
 Die folgenden Attribute, die festgelegt werden, durch den Aufruf [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), bestimmen Sie das zurückgegebene Resultset **SQLBrowseConnect**.  
  
|Attribut|Description|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|Wenn diese Option auf SQL_MORE_INFO_YES festgelegt wird **SQLBrowseConnect** eine erweiterte Zeichenfolge mit Servereigenschaften zurück.<br /><br /> Folgender Ausdruck ist ein Beispiel für eine erweiterte Zeichenfolge zurückgegebenes **SQLBrowseConnect**:<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> In dieser Zeichenfolge werden verschiedene durch Semikolons getrennte Informationen zum Server aufgeführt. Informationen zu verschiedenen Serverinstanzen werden durch Kommas getrennt.|  
|SQL_COPT_SS_BROWSE_SERVER|Wenn ein Servername angegeben wird, **SQLBrowseConnect** Informationen für den angegebenen Server zurück. Wenn SQL_COPT_SS_BROWSE_SERVER NULL festgelegt ist **SQLBrowseConnect** Informationen für alle Server in der Domäne zurückgegeben.<br /><br /> <br /><br /> Beachten Sie, dass aufgrund von Netzwerkproblemen **SQLBrowseConnect** möglicherweise nicht rechtzeitige eine Antwort von allen Servern empfängt. Daher kann die Liste der zurückgegebenen Server bei jeder Anforderung unterschiedlich sein.|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|Wenn die Pufferlänge nicht groß genug ist, um das Ergebnis aufzunehmen, können Sie das Attribut SQL_COPT_SS_BROWSE_CACHE_DATA auf SQL_CACHE_DATA_YES festlegen und Daten in Abschnitten abrufen. Diese Länge ist im Argument Pufferlänge SQLBrowseConnect angegeben.<br /><br /> Wenn weitere Daten verfügbar sind, wird SQL_NEED_DATA zurückgegeben. Wenn keine weiteren Daten abrufbar sind, wird SQL_SUCCESS zurückgegeben.<br /><br /> Der Standardwert ist SQL_CACHE_DATA_NO.|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>SQLBrowseConnect-Unterstützung für hohe Verfügbarkeit, Wiederherstellung im Notfall  
 Weitere Informationen zur Verwendung von **SQLBrowseConnect** zur Verbindung mit einer [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cluster, finden Sie unter [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>SQLBrowseConnect-Unterstützung für Dienstprinzipalnamen (Service Principal Names, SPNs)  
 Wenn eine Verbindung hergestellt wird, legt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client für SQL_COPT_SS_MUTUALLY_AUTHENTICATED und SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD die für das Herstellen der Verbindung zu verwendende Authentifizierungsmethode fest.  
  
 Weitere Informationen zu SPNs finden Sie unter [Dienstprinzipalnamen & #40; Dienstprinzipalnamen & #41; in Clientverbindungen & #40; ODBC & #41; ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="change-history"></a>Änderungsverlauf  
  
|Aktualisierter Inhalt|  
|---------------------|  
|Dokumentierte SQL_COPT_SS_BROWSE_CACHE_DATA.|  
  
## <a name="see-also"></a>Siehe auch  
 [SQLBrowseConnect-Funktion](http://go.microsoft.com/fwlink/?LinkId=59329)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
