---
title: Sys. conversation_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5cbfc13a807b2ec7c61ab2f12ec6f6cfe9f4ae82
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysconversationendpoints-transact-sql"></a>sys.conversation_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Jeder Seite einer [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Konversation wird durch einen Konversationsendpunkt dargestellt. Diese Katalogsicht enthält eine Zeile pro Konversationsendpunkt in der Datenbank.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|Bezeichner für diesen Konversationsendpunkt. Lässt keine NULL-Werte zu.|  
|conversation_id|**uniqueidentifier**|Bezeichner für die Konversation. Dieser Bezeichner wird von beiden Teilnehmern an der Konversation gemeinsam genutzt. In Kombination mit der is_initiator-Spalte ist dieser Bezeichner in der Datenbank eindeutig. Lässt keine NULL-Werte zu.|  
|is_initiator|**tinyint**|Gibt an, ob dieser Endpunkt Initiator oder Ziel der Konversation ist.  Lässt keine NULL-Werte zu.<br /><br /> 1 = Initiator<br /><br /> 0 = Ziel|  
|service_contract_id|**int**|Bezeichner des Vertrags für diese Konversation. Lässt keine NULL-Werte zu.|  
|conversation_group_id|**uniqueidentifier**|Bezeichner für die Konversationsgruppe, zu der diese Konversation gehört. Lässt keine NULL-Werte zu.|  
|service_id|**int**|Bezeichner des Diensts für diese Seite der Konversation. Lässt keine NULL-Werte zu.|  
|lifetime|**datetime**|Ablaufdatum/-zeitpunkt für diese Konversation. Lässt keine NULL-Werte zu.|  
|state|**char(2)**|Der aktuelle Status der Konversation. Lässt keine NULL-Werte zu. Folgende Angaben sind möglich:<br /><br /> Daher ausgehende gestartet. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]eine BEGIN CONVERSATION-Anweisung für diese Konversation verarbeitet, aber noch keine Nachrichten gesendet wurden.<br /><br /> SI eingehende gestartet. Eine andere Instanz gestartet, eine neue Konversation mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aber [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wurde noch nicht vollständig empfangen die erste Nachricht. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]möglicherweise erstellen Sie die Konversation in diesem Zustand, wenn die erste Meldung fragmentiert ist oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Nachrichten in falscher Reihenfolge empfängt. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] könnte die Konversation jedoch im Status CO (Konversation begonnen) erstellen, wenn die erste empfangene Übertragung für die Konversation die erste Nachricht vollständig enthält.<br /><br /> CO Konversation. Die Konversation wurde aufgenommen, und beide Seiten der Konversation können Nachrichten senden. Der Großteil der Kommunikation für einen Standarddienst findet in diesem Status der Konversation statt.<br /><br /> DI Disconnected eingehende. Die Remoteseite der Konversation hat eine END CONVERSATION-Anweisung ausgegeben. Die Konversation verbleibt in diesem Status, bis die lokale Seite der Konversation eine END CONVERSATION-Anweisung ausgibt. Eine Anwendung kann weiter Nachrichten für die Konversation empfangen. Da die Remoteseite der Konversation die Konversation beendet hat, kann eine Anwendung in dieser Konversation keine Nachrichten mehr senden. Wenn eine Anwendung eine END CONVERSATION-Anweisung ausgibt, geht die Konversation in den CD-Status (Geschlossen) über.<br /><br /> Führen Sie die ausgehende Konversation beenden. Die lokale Seite der Konversation hat eine END CONVERSATION-Anweisung ausgegeben. Die Konversation bleibt so lange in diesem Status, bis die Remoteseite der Konversation END CONVERSATION anerkennt. Eine Anwendung kann keine Nachrichten für die Konversation senden oder empfangen. Wenn die Remoteseite der Konversation die END CONVERSATION-Anweisung bestätigt, geht die Konversation in den CD-Zustand (Geschlossen) über.<br /><br /> ER-Fehler. An diesem Endpunkt ist ein Fehler aufgetreten. Die Fehlermeldung wird in die Anwendungswarteschlange eingefügt. Wenn die Anwendungswarteschlange leer ist, deutet dies darauf hin, dass die Fehlermeldung bereits von der Anwendung verarbeitet wurde.<br /><br /> CD geschlossen. Der Konversationsendpunkt wird nicht mehr verwendet.|  
|state_desc|**nvarchar(60)**|Beschreibung des Konversationsstatus des Endpunkts. In dieser Spalte ist NULL zulässig. Folgende Angaben sind möglich:<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **KONVERSATION**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **GESCHLOSSEN**<br /><br /> **ERROR**|  
|far_service|**nvarchar(256)**|Name des Diensts auf der Remoteseite der Konversation. Lässt keine NULL-Werte zu.|  
|far_broker_instance|**nvarchar(128)**|Die Brokerinstanz für die Remoteseite der Konversation. Lässt NULL-Werte zu.|  
|principal_id|**int**|Bezeichner des Prinzipals, dessen Zertifikat von der lokalen Seite des Dialogs verwendet wird. Lässt keine NULL-Werte zu.|  
|far_principal_id|**int**|Bezeichner des Benutzers, dessen Zertifikat von der Remoteseite des Dialogs verwendet wird. Lässt keine NULL-Werte zu.|  
|outbound_session_key_identifier|**uniqueidentifier**|Bezeichner für den ausgehenden Verschlüsselungsschlüssel für diesen Dialog. Lässt keine NULL-Werte zu.|  
|inbound_session_key_identifier|**uniqueidentifier**|Bezeichner für den eingehenden Verschlüsselungsschlüssel für diesen Dialog. Lässt keine NULL-Werte zu.|  
|security_timestamp|**datetime**|Zeitpunkt, zu dem der lokale Sitzungsschlüssel erstellt wurde. Lässt keine NULL-Werte zu.|  
|dialog_timer|**datetime**|Zeitpunkt, zu dem der Konversationszeitgeber für diesen Dialog eine DialogTimer-Nachricht sendet. Lässt keine NULL-Werte zu.|  
|send_sequence|**bigint**|Nächste Nachrichtennummer in der Sendesequenz. Lässt keine NULL-Werte zu.|  
|last_send_tran_id|**binary(6)**|Interne Transaktions-ID der letzten Transaktion, die eine Nachricht senden soll. Lässt keine NULL-Werte zu.|  
|end_dialog_sequence|**bigint**|Die Sequenznummer der Nachricht über das Beenden des Dialogs. Lässt keine NULL-Werte zu.|  
|receive_sequence|**bigint**|Erwartete nächste Nachrichtennummer in der Nachrichtenempfangssequenz. Lässt keine NULL-Werte zu.|  
|receive_sequence_frag|**int**|Erwartete nächste Nachrichtenfragmentnummer in der Nachrichtenempfangssequenz. Lässt keine NULL-Werte zu.|  
|system_sequence|**bigint**|Die Sequenznummer der letzten Systemnachricht für diesen Dialog. Lässt keine NULL-Werte zu.|  
|first_out_of_order_sequence|**bigint**|Die Sequenznummer der ersten Nachricht in den nicht in der richtigen Reihenfolge angeordneten Nachrichten für diesen Dialog. Lässt keine NULL-Werte zu.|  
|last_out_of_order_sequence|**bigint**|Die Sequenznummer der letzten Nachricht in den nicht in der richtigen Reihenfolge angeordneten Nachrichten für diesen Dialog. Lässt keine NULL-Werte zu.|  
|last_out_of_order_frag|**int**|Die Sequenznummer der letzten Nachricht in den nicht in der richtigen Reihenfolge angeordneten Fragmenten für diesen Dialog. Lässt keine NULL-Werte zu.|  
|is_system|**bit**|1, wenn dies ein Systemdialog ist. Lässt keine NULL-Werte zu.|  
|priority|**tinyint**|Die Konversationspriorität, die diesem Konversationsendpunkt zugewiesen ist. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
