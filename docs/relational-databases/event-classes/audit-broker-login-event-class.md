---
title: Audit Broker Login-Ereignisklasse | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: event-classes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Audit Broker Login event class
ms.assetid: af9b1153-2791-40ef-a95c-50923cd0cc97
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 630bfd54a62522f9b6d53141f2f8de2aa2833992
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="audit-broker-login-event-class"></a>Audit Broker Login-Ereignisklasse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erstellt **Audit Broker Login** -Ereignisse, um Überwachungsmeldungen in Bezug auf die Transportsicherheit von Service Broker zu melden.  
  
## <a name="audit-broker-login-event-class-data-columns"></a>Datenspalten der Audit Broker Login-Ereignisklasse  
  
|Datenspalte|Typ|Description|Spaltennummer|Filterbar|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Wird in dieser Ereignisklasse nicht verwendet.|10|ja|  
|**ClientProcessID**|**int**|Wird in dieser Ereignisklasse nicht verwendet.|9|ja|  
|**DatabaseID**|**int**|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] zeigt den Namen der Datenbank an, wenn die **ServerName** -Datenspalte in der Ablaufverfolgung aufgezeichnet wird und der Server verfügbar ist. Der Wert für eine Datenbank kann mithilfe der DB_ID-Funktion ermittelt werden.|3|ja|  
|**EventClass**|**int**|Der Typ der aufgezeichneten Ereignisklasse. Für **Audit Broker Login** ist der Typ immer **159**.|27|nein|  
|**EventSequence**|**int**|Die Sequenznummer für dieses Ereignis.|51|nein|  
|**EventSubClass**|**int**|Der Typ der Ereignisunterklasse, der weitere Informationen zu jeder Ereignisklasse liefert. In der folgenden Tabelle sind die Ereignisunterklassen-Werte für dieses Ereignis aufgeführt.|21|ja|  
|**FileName**|**nvarchar**|Authentifizierungsebene des Remote-Brokers. Die unterstützte Authentifizierungsmethode wird auf dem Endpunkt des Remote-Brokers konfiguriert. Wenn mehr als eine Methode zur Verfügung steht, bestimmt der annehmende Endpunkt (Zielendpunkt), welche Methode zuerst versucht wird. Folgende Werte sind möglich:<br /><br /> **Keiner**. Es wird keine Authentifizierungsmethode konfiguriert.<br /><br /> **NTLM**. Erfordert die NTLM-Authentifizierung.<br /><br /> **KERBEROS**. Erfordert die Kerberos-Authentifizierung.<br /><br /> **NEGOTIATE**. Windows verhandelt die Authentifizierungsmethode.<br /><br /> **CERTIFICATE**. Erfordert das Zertifikat, das für den in der **master** -Datenbank gespeicherten Endpunkt konfiguriert wurde.<br /><br /> **NTLM, CERTIFICATE**. Die NTLM-Authentifizierung oder die Authentifizierung durch SSL-Zertifikat wird akzeptiert.<br /><br /> **KERBEROS, CERTIFICATE**. Die Kerberos-Authentifizierung oder die Authentifizierung durch Endpunktzertifikat wird akzeptiert.<br /><br /> **NEGOTIATE, CERTIFICATE**. Windows verhandelt die Authentifizierungsmethode, oder es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden.<br /><br /> **CERTIFICATE, NTLM**. Nimmt ein Endpunktzertifikat oder NTLM für die Authentifizierung an.<br /><br /> **CERTIFICATE, KERBEROS**. Nimmt ein Endpunktzertifikat oder Kerberos für die Authentifizierung an.<br /><br /> **CERTIFICATE, NEGOTIATE**. Es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden, oder Windows handelt die Authentifizierungsmethode aus.|36|nein|  
|**HostName**|**nvarchar**|Wird in dieser Ereignisklasse nicht verwendet.|8|ja|  
|**IsSystem**|**int**|Gibt an, ob das Ereignis bei einem Systemprozess oder einem Benutzerprozess aufgetreten ist. 1 = System, 0 = Benutzer.|60|nein|  
|**LoginSid**|**image**|Die Sicherheits-ID (SID, Security Identification Number) des angemeldeten Benutzers. Die SID ist für jede Anmeldung beim Server eindeutig.|41|ja|  
|**NTDomainName**|**nvarchar**|Die Windows-Domäne, der der Benutzer angehört.|7|ja|  
|**NTUserName**|**nvarchar**|Der Name des Benutzers, der Besitzer der Verbindung ist, die dieses Ereignis generiert hat.|6|ja|  
|**ObjectName**|**nvarchar**|Die für diese Verbindung verwendete Verbindungszeichenfolge.|34|nein|  
|**OwnerName**|**nvarchar**|Die auf dem Endpunkt des lokalen Brokers konfigurierte unterstützte Authentifizierungsmethode. Wenn mehr als eine Methode zur Verfügung steht, bestimmt der annehmende Endpunkt (Zielendpunkt), welche Methode zuerst versucht wird. Folgende Werte sind möglich:<br /><br /> **Keiner**. Es wird keine Authentifizierungsmethode konfiguriert.<br /><br /> **NTLM**. Erfordert die NTLM-Authentifizierung.<br /><br /> **KERBEROS**. Erfordert die Kerberos-Authentifizierung.<br /><br /> **NEGOTIATE**. Windows verhandelt die Authentifizierungsmethode.<br /><br /> **CERTIFICATE**. Erfordert das Zertifikat, das für den in der **master** -Datenbank gespeicherten Endpunkt konfiguriert wurde.<br /><br /> **NTLM, CERTIFICATE**. Die NTLM-Authentifizierung oder die Authentifizierung durch SSL-Zertifikat wird akzeptiert.<br /><br /> **KERBEROS, CERTIFICATE**. Die Kerberos-Authentifizierung oder die Authentifizierung durch Endpunktzertifikat wird akzeptiert.<br /><br /> **NEGOTIATE, CERTIFICATE**. Windows verhandelt die Authentifizierungsmethode, oder es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden.<br /><br /> **CERTIFICATE, NTLM**. Die Endpunktzertifikat- oder NTLM-Authentifizierung wird akzeptiert.<br /><br /> **CERTIFICATE, KERBEROS**. Nimmt ein Endpunktzertifikat oder Kerberos für die Authentifizierung an.<br /><br /> **CERTIFICATE, NEGOTIATE**. Es kann ein Endpunktzertifikat für die Authentifizierung verwendet werden, oder Windows handelt die Authentifizierungsmethode aus.|37|nein|  
|**ProviderName**|**nvarchar**|Die für diese Verbindung verwendete Authentifizierungsmethode.|46|nein|  
|**RoleName**|**nvarchar**|Die Rolle der Verbindung. Dabei handelt es sich um **initiator** oder **target**.|38|nein|  
|**ServerName**|**nvarchar**|Der Name der Instanz von SQL Server, für die eine Ablaufverfolgung ausgeführt wird.|26|nein|  
|**SPID**|**int**|Die Serverprozess-ID, die SQL Server dem Prozess zugewiesen hat, der diesem Client zugeordnet ist.|12|ja|  
|**StartTime**|**datetime**|Der Zeitpunkt, zu dem das Ereignis begonnen hat, falls verfügbar.|14|ja|  
|**Status**|**int**|Gibt den Speicherort im SQL Server-Quellcode an, von dem aus das Ereignis erstellt wurde. Jeder Ort, von dem aus dieses Ereignis ggf. erstellt werden kann, besitzt einen anderen Statuscode. Der Microsoft Software Service kann mithilfe dieses Statuscodes herausfinden, wo das Ereignis generiert wurde.|30|nein|  
|**TargetUserName**|**nvarchar**|Anmeldestatus. Folgende Angaben sind möglich:<br /><br /> INITIAL<br /><br /> WAIT LOGIN NEGOTIATE<br /><br /> ONE ISC<br /><br /> ONE ASC<br /><br /> TWO ISC<br /><br /> TWO ASC<br /><br /> WAIT ISC Confirm<br /><br /> WAIT ASC Confirm<br /><br /> WAIT REJECT<br /><br /> WAIT PRE-MASTER SECRET<br /><br /> WAIT VALIDATION<br /><br /> WAIT ARBITRATION<br /><br /> ONLINE<br /><br /> Fehler<br /><br /> <br /><br /> **Hinweis**: ISC = Sicherheitskontext initiieren. ASC = Sicherheitskontext akzeptieren.|39|nein|  
|**TransactionID**|**bigint**|Die vom System zugewiesene ID der Transaktion.|4|nein|  
  
 In der folgenden Tabelle sind die Unterklassenwerte für diese Ereignisklasse aufgelistet.  
  
|ID|Unterklasse|Description|  
|--------|--------------|-----------------|  
|1|Login Success|Ein Login Success-Ereignis gibt an, dass der Anmeldeprozess des Brokers erfolgreich abgeschlossen wurde.|  
|2|Login Protocol Error|Ein Login Protocol Error-Ereignis gibt an, dass der Broker eine wohlgeformte, aber für den aktuellen Status des Anmeldeprozesses ungültige Nachricht empfängt. Die Meldung ging eventuell verloren oder wurde außer der Reihe versendet.|  
|3|Message Format Error|Ein Message Format Error-Ereignis gibt an, dass der Broker eine Nachricht empfangen hat, die nicht das erwartete Format aufweist. Die Nachricht wurde möglicherweise beschädigt, oder ein anderes Programm als SQL Server sendet Nachrichten an den Port, der von Service Broker verwendet wird.|  
|4|Negotiate Failure|Ein Negotiate Failure-Ereignis gibt an, dass der lokale Broker und der Remote-Broker sich gegenseitig ausschließende Authentifizierungsebenen unterstützen.|  
|5|Authentication Failure|Ein Authentication Failure-Ereignis gibt an, dass die Authentifizierung der Verbindung aufgrund eines Fehlers nicht von Service Broker ausgeführt werden kann. Bei der Windows-Authentifizierung gibt dieses Ereignis an, dass Service Broker die Windows-Authentifizierung nicht verwenden kann. Bei der zertifikatbasierten Authentifizierung gibt dieses Ereignis an, dass Service Broker nicht auf das Zertifikat zugreifen kann.|  
|6|Authorization Failure|Ein Authorization Failure-Ereignis gibt an, dass die Autorisierung der Verbindung von Service Broker verweigert wurde. Bei der Windows-Authentifizierung meldet dieser Bericht, dass die Sicherheits-ID für die Verbindung mit keinem Datenbankbenutzer übereinstimmt. Bei der zertifikatbasierten Authentifizierung gibt dieses Ereignis an, dass der mit der Nachricht übermittelte öffentliche Schlüssel keinem Zertifikat in der Datenbank entspricht.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
