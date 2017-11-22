---
title: "Verwenden von Verschlüsselung ohne Überprüfung | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d29061f3c43735b9a3855cee0dd635face3db00
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-encryption-without-validation"></a>Verwenden von Verschlüsselung ohne Überprüfung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verschlüsselt stets Netzwerkpakete, die mit der Anmeldung verbunden sind. Wenn auf dem Server beim Start kein Zertifikat bereitgestellt wird, erstellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ein selbstsigniertes Zertifikat, mit dem Anmeldungspakete verschlüsselt werden.  
  
 Anwendungen erfordern möglicherweise auch die Verschlüsselung des gesamten Netzwerkdatenverkehrs mit Verbindungszeichenfolgenschlüsselwörtern oder Verbindungseigenschaften. Die Schlüsselwörter lauten "Encrypt", für ODBC und OLE DB, wenn eine Anbieterzeichenfolge mit **IDBInitialize:: Initialize**, oder "Use Encryption for Data" für ADO und OLE DB, wenn eine Initialisierungszeichenfolge mit **IDataInitialize** . Dies kann auch konfigurieren, indem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager verwenden die **Protokollverschlüsselung** Option. Standardmäßig ist für die Verschlüsselung des Netzwerkverkehrs für eine Verbindung die Bereitstellung eines Zertifikats auf dem Server erforderlich.  
  
 Informationen zu verbindungszeichenfolgeschlüsselwörtern finden Sie unter [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Zum Aktivieren der Verschlüsselung verwendet werden, wenn ein Zertifikat auf dem Server nicht bereitgestellt wurde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager verwendet werden können, zum Festlegen der **Protokollverschlüsselung** und **Serverzertifikat vertrauen**  Optionen. In diesem Fall wird bei der Verschlüsselung ein selbstsigniertes Serverzertifikat ohne Überprüfung verwendet, wenn kein überprüfbares Zertifikat auf dem Server bereitgestellt wurde.  
  
 Anwendungen können auch das Schlüsselwort "TrustServerCertificate" oder das zugeordnete Verbindungsattribut verwenden, um sicherzustellen, dass eine Verschlüsselung durchgeführt wird. Anwendungseinstellungen senken nicht die vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client-Konfigurations-Manager festgelegte Sicherheitsstufe, vielmehr stärken sie sie. Z. B. wenn **Protokollverschlüsselung** nicht festgelegt ist für den Client kann eine Anwendung die Verschlüsselung selbst anfordern. Um die Verschlüsselung sicherzustellen, selbst wenn kein Serverzertifikat bereitgestellt wurde, kann eine Anwendung die Verschlüsselung und "TrustServerCertificate" anfordern. Wenn "TrustServerCertificate" nicht in der Clientkonfiguration aktiviert ist, ist dennoch die Bereitstellung eines Serverzertifikats erforderlich. In der folgenden Tabelle werden alle Fälle beschrieben:  
  
|Protokollverschlüsselung erzwingen - Clienteinstellung|Dem Serverzertifikat vertrauen|Verbindungszeichenfolge-/Verbindungsattribut 'Verschlüsseln/Verschlüsselung für Daten verwenden'|Verbindungszeichenfolge/Verbindungsattribut 'Dem Serverzertifikat vertrauen'|Ergebnis|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|Nein|–|Nein (Standard)|Wird ignoriert.|Keine Verschlüsselung.|  
|Nein|–|ja|Nein (Standard)|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|Nein|–|ja|ja|Verschlüsselung wird immer durchgeführt, es wird jedoch z. B. ein selbstsigniertes Serverzertifikat verwendet.|  
|ja|Nein|Wird ignoriert.|Wird ignoriert.|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|ja|ja|Nein (Standard)|Wird ignoriert.|Verschlüsselung wird immer durchgeführt, es wird jedoch z. B. ein selbstsigniertes Serverzertifikat verwendet.|  
|ja|ja|ja|Nein (Standard)|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|ja|ja|ja|ja|Verschlüsselung vielleicht immer tritt auf, aber ein selbst signiertes Serverzertifikat.|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB-Anbieter  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter unterstützt die Verschlüsselung ohne Überprüfung durch das Hinzufügen der SSPROP_INIT_TRUST_SERVER_CERTIFICATE Initialisierungseigenschaft-Datenquellen, die in der Eigenschaft DBPROPSET_SQLSERVERDBINIT implementiert wird festgelegt. Darüber hinaus ein neues Verbindungszeichenfolgen-Schlüsselwort "TrustServerCertificate", hinzugefügt wurden. Er akzeptiert Ja oder Nein-Werte; Nein ist die Standardeinstellung. Wenn Dienstkomponenten verwendet werden, sind die Werte "true" und "false" gültig, wobei "false" die Standardeinstellung ist.  
  
 Weitere Informationen zu Verbesserungen am DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>ODBC-Treiber für SQL Server Native Client  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber unterstützt die Verschlüsselung ohne Überprüfung durch Hinzufügungen zu den [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) und [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) Funktionen. SQL_COPT_SS_TRUST_SERVER_CERTIFICATE wurde hinzugefügt, um entweder SQL_TRUST_SERVER_CERTIFICATE_YES oder SQL_TRUST_SERVER_CERTIFICATE_NO anzunehmen, wobei SQL_TRUST_SERVER_CERTIFICATE_NO die Standardeinstellung ist. Darüber hinaus wurde ein neues Verbindungszeichenfolgeschlüsselwort, "TrustServerCertificate", hinzugefügt. Gültig sind die Werte "Ja" oder "Nein", wobei "Nein" die Standardeinstellung ist.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client-Features](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
