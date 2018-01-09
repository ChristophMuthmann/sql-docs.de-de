---
title: Dienstprinzipalnamen (SPN) in Clientverbindungen (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e212010e-a5b6-4ad1-a3c0-575327d3ffd3
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2f4140619a98798e057c8e4ae85c1e99c58e68a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="service-principal-names-spns-in-client-connections-ole-db"></a>Dienstprinzipalnamen (SPN) in Clientverbindungen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In diesem Thema werden OLE DB-Eigenschaften und Memberfunktionen beschrieben, die Dienstprinzipalnamen (SPN) in Clientanwendungen unterstützen. Weitere Informationen zu SPNs in Clientanwendungen finden Sie unter [Service Principal Name &#40; Dienstprinzipalnamen &#41; Unterstützung in Clientverbindungen](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md). Ein Beispiel finden Sie unter [integrierte Kerberos-Authentifizierung &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-how-to/integrated-kerberos-authentication-ole-db.md).  
  
## <a name="provider-initialization-string-keywords"></a>Schlüsselwörter für Anbieter-Initialisierungszeichenfolgen  
 Die folgenden Schlüsselwörter für Anbieter-Initialisierungszeichenfolgen unterstützen SPNs in OLE DB-Anwendungen. In der folgenden Tabelle werden die Werte aus der schlüsselwortspalte für die Anbieterzeichenfolge der IDBInitialize:: Initialize verwendet. Beim Herstellen einer Verbindung mit ADO oder IDataInitialize:: GetDatasource, werden die Werte aus der Beschreibungsspalte in Initialisierungszeichenfolgen verwendet.  
  
|Schlüsselwort|Description|value|  
|-------------|-----------------|-----------|  
|ServerSPN|Server-SPN|Der SPN für den Server. Der Standardwert ist eine leere Zeichenfolge ist, wodurch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN.|  
|FailoverPartnerSPN|Failoverpartner-SPN|Der SPN für den Failoverpartner. Der Standardwert ist eine leere Zeichenfolge ist, wodurch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN.|  
  
## <a name="data-source-initialization-properties"></a>Eigenschaften zur Datenquelleninitialisierung  
 Die folgenden Eigenschaften in der **DBPROPSET_SQLSERVERDBINIT** -Eigenschaftengruppe ermöglichen es Anwendungen, SPNs anzugeben.  
  
|Name|Typ|Verwendung|  
|----------|----------|-----------|  
|SSPROP_INIT_SERVERSPN|VT_BSTR, Lese-/Schreibzugriff|Gibt den SPN für den Server an. Der Standardwert ist eine leere Zeichenfolge ist, wodurch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN.|  
|SSPROP_INIT_FAILOVERPARTNERSPN|VT_BSTR, Lese-/Schreibzugriff|Gibt den SPN für den Failoverpartner an. Der Standardwert ist eine leere Zeichenfolge ist, wodurch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client den vorgegebenen, vom Anbieter generierten SPN.|  
  
## <a name="data-source-properties"></a>Datenquelleneigenschaften  
 Die folgenden Eigenschaften in der **DBPROPSET_SQLSERVERDATASOURCEINFO** -Eigenschaftengruppe ermöglichen es Anwendungen, die Authentifizierungsmethode zu ermitteln.  
  
|Name|Typ|Verwendung|  
|----------|----------|-----------|  
|SSPROP_INTEGRATEDAUTHENTICATIONMETHOD|VT_BSTR, schreibgeschützt|Gibt die für die aktuelle Verbindung verwendete Authentifizierungsmethode zurück. Der zurückgegebene Wert für die Anwendung ist der Wert, der an Windows zurückgibt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Folgende Werte sind möglich: <br />"NTLM" wird zurückgegeben, wenn eine Verbindung mit der NTLM-Authentifizierung geöffnet wird.<br />"Kerberos" wird zurückgegeben, wenn eine Verbindung mit der Kerberos-Authentifizierung geöffnet wird.<br /><br /> Wenn eine Verbindung geöffnet wurde und die Authentifizierungsmethode nicht bestimmt werden kann, wird "VT_EMPTY" zurückgegeben.<br /><br /> Diese Eigenschaft kann nur gelesen werden, wenn eine Datenquelle initialisiert wurde. Wenn Sie versuchen, die Eigenschaft zu lesen, bevor eine Datenquelle initialisiert wurde, IDBProperties::GetProperies zurück DB_S_ERRORSOCCURRED oder DB_E_ERRORSOCCURRED, nach Bedarf, und DBPROPSTATUS_NOTSUPPORTED wird in DBPROPSET_PROPERTIESINERROR festgelegt für diese Eigenschaft. Dieses Verhalten entspricht der OLE DB-Kernspezifikation.|  
|SSPROP_MUTUALLYAUTHENICATED|VT_BOOL, schreibgeschützt|Gibt VARIANT_TRUE zurück, wenn die Server in der Verbindung gegenseitig authentifiziert wurden; andernfalls wird VARIANT_FALSE zurückgegeben.<br /><br /> Diese Eigenschaft kann nur gelesen werden, wenn eine Datenquelle initialisiert wurde. Ist ein Versuch, die Eigenschaft zu lesen, bevor eine Datenquelle initialisiert wurde, IDBProperties::GetProperies zurück DB_S_ERRORSOCCURRED oder DB_E_ERRORSOCCURRED, nach Bedarf, und DBPROPSTATUS_NOTSUPPORTED wird in DBPROPSET_ festgelegt PROPERTIESINERROR für diese Eigenschaft. Dieses Verhalten entspricht der OLE DB-Kernspezifikation.<br /><br /> Wenn dieses Attribut für eine Verbindung abgefragt wird, für die keine Windows-Authentifizierung verwendet wurde, wird VARIANT_FALSE zurückgegeben.|  
  
## <a name="ole-db-api-support-for-spns"></a>OLE DB-API-Unterstützung für SPNs  
 In der folgenden Tabelle werden die OLE DB-Memberfunktionen beschrieben, die SPNs in Clientverbindungen unterstützen:  
  
|Memberfunktion|Description|  
|---------------------|-----------------|  
|IDataInitialize::GetDataSource|*pwszInitializationString* kann die neuen Schlüsselwörter **ServerSPN** und **FailoverPartnerSPN**enthalten.|  
|IDataInitialize::GetInitializationString|Wenn SSPROP_INIT_SERVERSPN und SSPROP_INIT_FAILOVERPARTNERSPN Nichtstandardwerte aufweisen, werden sie durch *ppwszInitString* als Schlüsselwortwerte für **ServerSPN** und **FailoverPartnerSPN**in die Initialisierungszeichenfolge aufgenommen. Andernfalls sind diese Schlüsselwörter nicht in der Initialisierungszeichenfolge enthalten.|  
|IDBInitialize::Initialize|Sind durch die Einstellung von DBPROP_INIT_PROMPT in den Eigenschaften zur Datenquelleninitialisierung Aufforderungen aktiviert, wird das OLE DB-Anmeldedialogfeld angezeigt. Damit können SPNs sowohl für den Prinzipalserver als auch für seinen Failoverpartner eingegeben werden.<br /><br /> Sofern festgelegt, erkennt die Anbieterzeichenfolge in DPPROP_INIT_PROVIDERSTRING die neuen Schlüsselwörter **ServerSPN** und **FailoverPartnerSPN** und verwendet ihre Werte (sofern vorhanden) zur Initialisierung von SSPROP_INIT_SERVER_SPN und SSPROP_INIT_FAILOVER_PARTNER_SPN.<br /><br /> IDBProperties:: SetProperties kann aufgerufen werden, um die Eigenschaften SSPROP_INIT_SERVER_SPN und SSPROP_INIT_FAILOVER_PARTNER_SPN festzulegen, bevor IDBInitialize:: Initialize aufgerufen wird. Dies ist eine Alternative zum Verwenden einer Anbieterzeichenfolge.<br /><br /> Wird eine Eigenschaft mehrfach festgelegt, hat ein programmgesteuert festgelegter Wert Vorrang vor einem in der Anbieterzeichenfolge festgelegten Wert. Ein in einer Initialisierungszeichenfolge festgelegter Wert hat Vorrang vor einem in einem Anmeldedialogfeld festgelegten Wert.<br /><br /> Kommt ein Schlüsselwort mehrfach in der Anbieterzeichenfolge vor, hat der an erster Stelle stehende Wert Vorrang.|  
|IDBProperties::GetProperties|IDBProperties::GetProperties kann aufgerufen werden, um die Werte der neuen Eigenschaften zur datenquelleninitialisierung SSPROP_INIT_SERVERSPN und SSPROP_INIT_FAILOVERPARTNERSPN und die neuen Datenquelleneigenschaften SSPROP_AUTHENTICATIONMETHOD und SSPROP_ zu erhalten. MUTUALLYAUTHENTICATED.|  
|IdbProperties::GetPropertyInfo|GetPropertyInfo schließt die neuen Eigenschaften zur datenquelleninitialisierung SSPROP_INIT_SERVERSPN und SSPROP_INIT_FAILOVERPARTNERSPN oder die neuen Datenquelleneigenschaften SSPROP_AUTHENTICATION_METHOD und SSPROP_MUTUALLYAUTHENTICATED.|  
|IDBProperties::SetProperties|IDBProperties:: SetProperties kann aufgerufen werden, um die Werte der neuen Datenquelle Eigenschaften zur datenquelleninitialisierung SSPROP_INITSERVERSPN und SSPROP_INIT_FAILOVERPARTNERSPN festzulegen.<br /><br /> Diese Eigenschaften können zu einem beliebigen Zeitpunkt festgelegt werden. Ist die Datenquelle jedoch bereits geöffnet, wird der folgende Fehler zurückgegeben: DB_E_ERRORSOCCURRED, "Fehler bei einem aus mehreren Schritten bestehenden OLE DB-Vorgang. Prüfen Sie die einzelnen OLE DB-Statuswerte, falls vorhanden. Daten wurden nicht verarbeitet."|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
