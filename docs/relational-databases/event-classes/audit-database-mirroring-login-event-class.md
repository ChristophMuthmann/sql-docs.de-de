---
title: Audit Database Mirroring Login (Ereignisklasse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- Audit Database Mirroring Login event class
- database mirroring [SQL Server], event notifications
ms.assetid: d0bd436d-aade-4208-a7e5-75cf3b5d0ce9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e224b60ca56dab7ce2c46d6bf3a554690bc3b0c
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="audit-database-mirroring-login-event-class"></a>Audit Database Mirroring Login (Ereignisklasse)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt ein **Audit Database Mirroring Login** -Ereignis, um Überwachungsmeldungen im Zusammenhang mit der Datenbankspiegelungs-Transportsicherheit zu melden.  
  
## <a name="audit-database-mirroring-login-event-class-data-columns"></a>Datenspalten der Audit Database Mirroring Login-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Wird in dieser Ereignisklasse nicht verwendet.|10|ja|  
|**ClientProcessID**|**int**|Wird in dieser Ereignisklasse nicht verwendet.|9|ja|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Lautet für **Audit Database Mirroring Login** immer **154**.|27|nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|nein|  
|**EventSubClass**|**int**|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse liefert. In der folgenden Tabelle sind die Ereignisunterklassen-Werte für dieses Ereignis aufgeführt.|21|ja|  
|**FileName**|**nvarchar**|Unterstützte Authentifizierungsmethode, konfiguriert am Endpunkt für die Remotedatenbank-Spiegelung. Wenn mehr als eine Methode zur Verfügung steht, bestimmt der annehmende Endpunkt (Zielendpunkt), welche Methode zuerst versucht wird. Folgende Werte sind möglich:<br /><br /> <br /><br /> **Keiner**. Es wird keine Authentifizierungsmethode konfiguriert.<br /><br /> **NTLM**. Erfordert die NTLM-Authentifizierung.<br /><br /> **KERBEROS**. Erfordert die Kerberos-Authentifizierung.<br /><br /> **NEGOTIATE**. Windows verhandelt die Authentifizierungsmethode.<br /><br /> **CERTIFICATE**. Erfordert das Zertifikat, das für den in der **master** -Datenbank gespeicherten Endpunkt konfiguriert wurde.<br /><br /> **NTLM, CERTIFICATE**. Nimmt NTLM oder das Endpunktzertifikat für die Authentifizierung an.<br /><br /> **KERBEROS, CERTIFICATE**. Nimmt Kerberos oder das Endpunktzertifikat für die Authentifizierung an.<br /><br /> **NEGOTIATE, CERTIFICATE**. Windows verhandelt die Authentifizierungsmethode, oder es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden.<br /><br /> **CERTIFICATE, NTLM**. Nimmt ein Endpunktzertifikat oder NTLM für die Authentifizierung an.<br /><br /> **CERTIFICATE, KERBEROS**. Nimmt ein Endpunktzertifikat oder Kerberos für die Authentifizierung an.<br /><br /> **CERTIFICATE, NEGOTIATE**. Nimmt ein Endpunktzertifikat für die Authentifizierung an, oder Windows verhandelt die Authentifizierungsmethode.|36|nein|  
|**HostName**|**nvarchar**|Wird in dieser Ereignisklasse nicht verwendet.|8|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ObjectName**|**nvarchar**|Die für diese Verbindung verwendete Verbindungszeichenfolge.|34|nein|  
|**OwnerName**|**nvarchar**|Unterstützte Authentifizierungsmethode, konfiguriert am Endpunkt für die lokale Datenbankspiegelung. Wenn mehr als eine Methode zur Verfügung steht, bestimmt der annehmende Endpunkt (Zielendpunkt), welche Methode zuerst versucht wird. Folgende Werte sind möglich:<br /><br /> <br /><br /> **Keiner**. Es wird keine Authentifizierungsmethode konfiguriert.<br /><br /> **NTLM**. Erfordert die NTLM-Authentifizierung.<br /><br /> **KERBEROS**. Erfordert die Kerberos-Authentifizierung.<br /><br /> **NEGOTIATE**. Windows verhandelt die Authentifizierungsmethode.<br /><br /> **CERTIFICATE**. Erfordert das Zertifikat, das für den in der **master** -Datenbank gespeicherten Endpunkt konfiguriert wurde.<br /><br /> **NTLM, CERTIFICATE**. Nimmt NTLM oder das Endpunktzertifikat für die Authentifizierung an.<br /><br /> **KERBEROS, CERTIFICATE**. Nimmt Kerberos oder das Endpunktzertifikat für die Authentifizierung an.<br /><br /> **NEGOTIATE, CERTIFICATE**. Windows verhandelt die Authentifizierungsmethode, oder es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden.<br /><br /> **CERTIFICATE, NTLM**. Nimmt ein Endpunktzertifikat oder NTLM für die Authentifizierung an.<br /><br /> **CERTIFICATE, KERBEROS**. Nimmt ein Endpunktzertifikat oder Kerberos für die Authentifizierung an.<br /><br /> **CERTIFICATE, NEGOTIATE**. Nimmt ein Endpunktzertifikat für die Authentifizierung an, oder Windows verhandelt die Authentifizierungsmethode.|37|nein|  
|**ProviderName**|**nvarchar**|Die für diese Verbindung verwendete Authentifizierungsmethode.|46|nein|  
|**RoleName**|**nvarchar**|Die Rolle der Verbindung. Dabei handelt es sich um **initiator** oder **target**.|38|nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|**SPID**|**int**|Die Serverprozess-ID, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dem Prozess zugewiesen wurde, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**Status**|**int**|Gibt den Standort im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Quellcode an, der das Ereignis erstellt hat. Jeder Ort, von dem aus dieses Ereignis ggf. erstellt werden kann, besitzt einen anderen Statuscode. Der Microsoft Software Service kann mithilfe dieses Statuscodes herausfinden, wo das Ereignis generiert wurde.|30|nein|  
|**TargetUserName**|**nvarchar**|Anmeldestatus. Folgende Angaben sind möglich:<br /><br /> **INITIAL**<br /><br /> **WAIT LOGIN NEGOTIATE**<br /><br /> **ONE ISC**<br /><br /> **ONE ASC**<br /><br /> **TWO ISC**<br /><br /> **TWO ASC**<br /><br /> **WAIT ISC Confirm**<br /><br /> **WAIT ASC Confirm**<br /><br /> **WAIT REJECT**<br /><br /> **WAIT PRE-MASTER SECRET**<br /><br /> **WAIT VALIDATION**<br /><br /> **WAIT ARBITRATION**<br /><br /> **ONLINE**<br /><br /> **ERROR**<br /><br /> <br /><br /> Hinweis: ISC = Sicherheitskontext initiieren. ASC = Accept Security Context.|39|nein|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|nein|  
  
 In der folgenden Tabelle sind die Unterklassenwerte für diese Ereignisklasse aufgelistet.  
  
|ID|Unterklasse|Description|  
|--------|--------------|-----------------|  
|1|Login Success|Ein Login Success-Ereignis meldet, dass der letzte Datenbankspiegelungs-Anmeldeprozess erfolgreich abgeschlossen wurde.|  
|2|Login Protocol Error|Ein Login Protocol Error-Ereignis meldet, dass die Datenbankspiegelungs-Anmeldung eine Meldung erhält, die zwar wohlgeformt, jedoch für den aktuellen Status des Anmeldeprozesses ungültig ist. Die Meldung ging eventuell verloren oder wurde außer der Reihe versendet.|  
|3|Message Format Error|Ein Message Format Error-Ereignis meldet, dass die Datenbankspiegelungs-Anmeldung eine Meldung erhalten hat, die dem erwarteten Format nicht entspricht. Die Meldung war möglicherweise beschädigt, oder ein anderes Programm als [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sendet eventuell Meldungen an den Port, der zur Datenbankspiegelung verwendet wird.|  
|4|Negotiate Failure|Ein Negotiate Failure-Ereignis meldet, dass der lokale Datenbankspiegelungs-Endpunkt und der Remotedatenbank-Spiegelungsendpunkt gegenseitig ausschließende Authentifizierungsebenen unterstützen.|  
|5|Authentication Failure|Ein Authentication Failure-Ereignis meldet, dass ein Datenbankspiegelungs-Endpunkt aufgrund eines Fehlers keine Authentifizierung für die Verbindung durchführen kann. Für die Windows-Authentifizierung meldet dieses Ereignis, dass der Datenbankspiegelungs-Endpunkt keine Windows-Authentifizierung verwenden kann. Für eine zertifikatbasierte Authentifizierung meldet dieses Ereignis, dass der Datenbankspiegelungs-Endpunkt nicht auf das Zertifikat zugreifen kann.|  
|6|Authorization Failure|Ein Authorization Failure-Ereignis meldet, dass ein Datenbankspiegelungs-Endpunkt die Autorisierung für die Verbindung verweigert hat. Bei der Windows-Authentifizierung meldet dieser Bericht, dass die Sicherheits-ID für die Verbindung mit keinem Datenbankbenutzer übereinstimmt. Für eine zertifikatbasierte Authentifizierung meldet dieses Ereignis, dass der in der Meldung zugestellte öffentliche Schlüssel nicht mit einem Zertifikat in der **master** -Datenbank übereinstimmt.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
