---
title: Verwenden von Verschlüsselung ohne Überprüfung | Microsoft Docs
description: Verwenden von Verschlüsselung ohne Überprüfung
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], encryption
- cryptography [OLE DB Driver for SQL Server]
- MSOLEDBSQL, encryption
- encryption [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, encryption
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be4885de83c5d189b1772c6fe04eff1a744cafef
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="using-encryption-without-validation"></a>Verwenden von Verschlüsselung ohne Überprüfung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verschlüsselt stets Netzwerkpakete, die mit der Anmeldung verbunden sind. Wenn auf dem Server beim Start kein Zertifikat bereitgestellt wird, erstellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ein selbstsigniertes Zertifikat, mit dem Anmeldungspakete verschlüsselt werden.  

Selbstsignierte Zertifikate garantieren Sicherheit nicht. Der verschlüsselte Handshake basiert auf NT LAN Manager (NTLM). Es wird dringend empfohlen, dass Sie ein überprüfbares Zertifikat auf SQL Server für sichere Verbindungen bereitstellen. Sicherheit TLS (Transport Layer) können nur mit Überprüfung des Serverzertifikats sichere vorgenommen werden.

Anwendungen erfordern möglicherweise auch die Verschlüsselung des gesamten Netzwerkdatenverkehrs mit Verbindungszeichenfolgenschlüsselwörtern oder Verbindungseigenschaften. Die Schlüsselwörter lauten "Encrypt", für OLE DB, wenn eine Anbieterzeichenfolge mit **IDBInitialize:: Initialize**, oder "Use Encryption for Data" für ADO und OLE DB, wenn eine Initialisierungszeichenfolge mit **IDataInitialize**. Dies kann auch konfigurieren, indem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager verwenden die **Protokollverschlüsselung** aus, und durch Konfigurieren des Clients zum Anfordern verschlüsselter Verbindungen. Standardmäßig ist für die Verschlüsselung des Netzwerkverkehrs für eine Verbindung die Bereitstellung eines Zertifikats auf dem Server erforderlich. Durch Festlegen des Clients das Zertifikat auf dem Server als vertrauenswürdig einstufen, könnte Sie anfällig für Man-in-the-Middle-Angriffe. Wenn Sie ein überprüfbares Zertifikat auf dem Server bereitstellen, stellen Sie sicher, dass Sie die Clienteinstellungen zu dem Zertifikat vertrauen auf "false" ändern.

Informationen zu verbindungszeichenfolgeschlüsselwörtern finden Sie unter [Schlüsselwörtern für Verbindungszeichenfolgen mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md ).  
  
 Zum Aktivieren der Verschlüsselung verwendet werden, wenn ein Zertifikat auf dem Server nicht bereitgestellt wurde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager verwendet werden können, zum Festlegen der **Protokollverschlüsselung** und **Serverzertifikat vertrauen**  Optionen. In diesem Fall wird bei der Verschlüsselung ein selbstsigniertes Serverzertifikat ohne Überprüfung verwendet, wenn kein überprüfbares Zertifikat auf dem Server bereitgestellt wurde.  
  
 Anwendungen können auch das Schlüsselwort "TrustServerCertificate" oder das zugeordnete Verbindungsattribut verwenden, um sicherzustellen, dass eine Verschlüsselung durchgeführt wird. Anwendungseinstellungen senken nicht die vom [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client-Konfigurations-Manager festgelegte Sicherheitsstufe, vielmehr stärken sie sie. Z. B. wenn **Protokollverschlüsselung** nicht festgelegt ist für den Client kann eine Anwendung die Verschlüsselung selbst anfordern. Um die Verschlüsselung sicherzustellen, selbst wenn kein Serverzertifikat bereitgestellt wurde, kann eine Anwendung die Verschlüsselung und "TrustServerCertificate" anfordern. Wenn "TrustServerCertificate" nicht in der Clientkonfiguration aktiviert ist, ist dennoch die Bereitstellung eines Serverzertifikats erforderlich. In der folgenden Tabelle werden alle Fälle beschrieben:  
  
|Protokollverschlüsselung erzwingen - Clienteinstellung|Dem Serverzertifikat vertrauen|Verbindungszeichenfolge-/Verbindungsattribut 'Verschlüsseln/Verschlüsselung für Daten verwenden'|Verbindungszeichenfolge/Verbindungsattribut 'Dem Serverzertifikat vertrauen'|Ergebnis|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|nein|–|Nein (Standard)|Wird ignoriert.|Keine Verschlüsselung.|  
|nein|–|ja|Nein (Standard)|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|nein|–|ja|ja|Verschlüsselung wird immer durchgeführt, es wird jedoch z. B. ein selbstsigniertes Serverzertifikat verwendet.|  
|ja|nein|Wird ignoriert.|Wird ignoriert.|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|ja|ja|Nein (Standard)|Wird ignoriert.|Verschlüsselung wird immer durchgeführt, es wird jedoch z. B. ein selbstsigniertes Serverzertifikat verwendet.|  
|ja|ja|ja|Nein (Standard)|Eine Verschlüsselung findet nur statt, wenn ein überprüfbares Serverzertifikat vorliegt, anderenfalls schlägt der Verbindungsversuch fehl.|  
|ja|ja|ja|ja|Verschlüsselung vielleicht immer tritt auf, aber ein selbst signiertes Serverzertifikat.|  
||||||

> [!CAUTION]
> Die obigen Tabelle bietet eine Orientierungshilfe nur auf das Systemverhalten unter unterschiedlichen Konfigurationen. Sichere Verbindungen stellen Sie sicher, dass dem Client und Server-Verschlüsselung. Stellen Sie außerdem sicher, dass der Server ein überprüfbares Zertifikat, und dass die **"TrustServerCertificate"** Einstellung auf dem Client auf "false" festgelegt ist.

## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer 
 Der OLE DB-Treiber für SQL Server unterstützt die Verschlüsselung ohne Überprüfung durch das Hinzufügen der SSPROP_INIT_TRUST_SERVER_CERTIFICATE Initialisierungseigenschaft-Datenquellen, die in der Eigenschaftengruppe DBPROPSET_SQLSERVERDBINIT implementiert wird. Darüber hinaus ein neues Verbindungszeichenfolgen-Schlüsselwort "TrustServerCertificate", hinzugefügt wurden. Er akzeptiert Ja oder Nein-Werte; Nein ist die Standardeinstellung. Wenn Dienstkomponenten verwendet werden, sind die Werte "true" und "false" gültig, wobei "false" die Standardeinstellung ist.  
  
 Weitere Informationen zu Verbesserungen am DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  

  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
