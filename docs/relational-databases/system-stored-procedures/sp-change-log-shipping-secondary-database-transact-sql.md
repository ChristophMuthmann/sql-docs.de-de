---
title: Sp_change_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc7ed57e7f6f64f3fc2527cdaff3766690032489
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert Einstellungen sekundärer Datenbanken.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@restore_delay =** ] '*restore_delay*'  
 Die Zeit in Minuten, die der sekundäre Server vor dem Wiederherstellen einer bestimmten Sicherungsdatei wartet. *Restore_delay* ist **Int** und darf nicht NULL sein. Der Standardwert ist 0.  
  
 [ **@restore_all =** ] '*restore_all*'  
 Falls 1, stellt der sekundäre Server bei Ausführung des Wiederherstellungsauftrags alle verfügbaren Sicherungen des Transaktionsprotokolls wieder her. Andernfalls wird nach der Wiederherstellung einer Datei beendet. *Restore_all* ist **Bit** und darf nicht NULL sein.  
  
 [ **@restore_mode =** ] '*restore_mode*'  
 Der Wiederherstellungsmodus für die sekundäre Datenbank.  
  
 0 = Wiederherstellungsprotokoll mit NORECOVERY.  
  
 1 = das Protokoll mit STANDBY wiederhergestellt.  
  
 *Wiederherstellen* ist **Bit** und darf nicht NULL sein.  
  
 [ **@disconnect_users =** ] '*disconnect_users*'  
 Wird der Wert auf 1 festgelegt, werden die Verbindungen von Benutzern mit der sekundären Datenbank getrennt, wenn ein Wiederherstellungsvorgang durchgeführt wird. Standard = 0. *Disconnect_users* ist **Bit** und darf nicht NULL sein.  
  
 [ **@block_size =** ] '*block_size*'  
 Die Größe in Bytes, die als Blockgröße für das Sicherungsmedium verwendet wird. *Block_size* ist **Int** hat den Standardwert "-1".  
  
 [ **@buffer_count =** ] '*buffer_count*'  
 Die Gesamtanzahl der beim Sicherungs- oder Wiederherstellungsvorgang verwendeten Puffer. *Buffer_count* ist **Int** hat den Standardwert "-1".  
  
 [ **@max_transfer_size =** ] '*max_transfer_size*'  
 Die Größe der maximalen Eingabe- oder Ausgabeanforderung in Bytes, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an das Sicherungsmedium ausgegeben wird. *Max_transfersize* ist **Int** und kann NULL sein.  
  
 [  **@restore_threshold =** ] "*Restore_threshold*"  
 Die Anzahl der zulässigen Minuten zwischen Wiederherstellungsvorgängen, bevor eine Warnung generiert wird. *Restore_threshold* ist **Int** und darf nicht NULL sein.  
  
 [  **@threshold_alert =** ] "*Threshold_alert*"  
 Die Warnung, die ausgelöst wird, wenn die Wiederherstellungsschwelle überschritten wird. *Threshold_alert* ist **Int**, hat den Standardwert 14420.  
  
 [  **@threshold_alert_enabled =** ] "*Threshold_alert_enabled*"  
 Gibt an, ob eine Warnung wird ausgelöst, wenn *Restore_threshold*überschritten wird. 1 = aktiviert; 0 = deaktiviert. *Threshold_alert_enabled* ist **Bit** und darf nicht NULL sein.  
  
 [  **@history_retention_period =** ] "*History_retention_period*"  
 Der Zeitraum (in Minuten), für den der Verlauf beibehalten wird. *History_retention_period* ist **Int**. Wenn keine Angabe erfolgt, wird der Wert 1440 verwendet werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Hinweise  
 **sp_change_log_shipping_secondary_database** must be run from the **master** database on the secondary server. Diese gespeicherte Prozedur führt folgende Aktionen aus:  
  
1.  Ändert die Einstellungen in der **Log_shipping_secondary_database** zeichnet nach Bedarf.  
  
2.  Ändert den lokalen Überwachungsdatensatz in **Log_shipping_monitor_secondary** auf dem sekundären Server mithilfe bereitgestellter Argumente, falls erforderlich.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle **sysadmin** können diese Prozedur ausführen.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird die Verwendung **Sp_change_log_shipping_secondary_database** Parameter sekundärer Datenbanken für die Datenbank aktualisieren **LogShipAdventureWorks**.  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Über den Protokollversand &#40; SQLServer &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
