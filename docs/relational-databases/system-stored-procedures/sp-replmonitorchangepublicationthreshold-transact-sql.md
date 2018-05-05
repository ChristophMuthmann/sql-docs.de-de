---
title: Sp_replmonitorchangepublicationthreshold (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bfc9b3ad0f67fa462db098a44603cc9cb1a4d586
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Schwellenwertmetrik für die Überwachung einer Veröffentlichung. Diese gespeicherte Prozedur, die zum Überwachen der Replikation verwendet wird, wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@publisher** = ] **'***publisher***'**  
 Der Name des Verlegers. *Publisher* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Der Name der veröffentlichten Datenbank. *Publisher_db* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publication** =] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung, deren Attribute für den Überwachungsschwellenwert geändert werden. *Veröffentlichung* ist **Sysname**, hat keinen Standardwert.  
  
 [ **@publication_type** =] *Publication_type*  
 Der Typ der Veröffentlichung. *Publication_type* ist **Int**, und kann einen der folgenden Werte sein.  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|**0**|Transaktionsveröffentlichung.|  
|**1**|Momentaufnahmeveröffentlichung.|  
|**2**|Mergeveröffentlichung.|  
|NULL (Standard)|Replikationsversuche zum Bestimmen des Veröffentlichungstyps.|  
  
 [ **@metric_id** =] *Metric_id*  
 Die ID der Schwellenwertmetrik für die Veröffentlichung, die geändert wird. *Metric_id* ist **Int**, hat den Standardwert NULL und kann einen der folgenden Werte sein.  
  
|Wert|Metrikname|  
|-----------|-----------------|  
|**1**|**expiration** - überwacht den bevorstehenden Ablauf von Abonnements für Transaktionsveröffentlichungen.|  
|**2**|**latency** - überwacht die Leistung von Abonnements für Transaktionsveröffentlichungen.|  
|**4**|**mergeexpiration** - überwacht den bevorstehenden Ablauf von Abonnements für Mergeveröffentlichungen.|  
|**5**|**Mergeslowrunduration** -überwacht die Dauer von mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ).|  
|**6**|**Mergefastrunduration** -überwacht die Dauer von mergesynchronisierungen über Verbindungen hoher Bandbreite Local Area Network (LAN).|  
|**7**|**mergefastrunspeed** - Überwachung der Synchronisierungsgeschwindigkeit von Mergesynchronisierungen über Verbindungen mit hoher Bandbreite (LAN-Verbindungen).|  
|**8**|**Mergeslowrunspeed** -überwacht die synchronisierungsgeschwindigkeit von mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ).|  
  
 Geben Sie *Metric_id* oder *Thresholdmetricname*. Wenn *Thresholdmetricname* angegeben ist, klicken Sie dann *Metric_id* sollte NULL sein.  
  
 [ **@thresholdmetricname** =] **"***Thresholdmetricname***"**  
 Der Name der Schwellenwertmetrik für die Veröffentlichung, die geändert wird. *Thresholdmetricname* ist **Sysname**, hat den Standardwert NULL. Geben Sie *Thresholdmetricname* oder *Metric_id*. Wenn *Metric_id* angegeben ist, klicken Sie dann *Thresholdmetricname* sollte NULL sein.  
  
 [ **@value** =] *Wert*  
 Der neue Wert der Schwellenwertmetrik für die Veröffentlichung. *Wert* ist **Int**, hat den Standardwert NULL. Wenn **null**, und klicken Sie dann der Metrikwert nicht aktualisiert wird.  
  
 [ **@shouldalert** =] *Shouldalert*  
 Gibt an, ob eine Warnung generiert wird, wenn die Schwellenwertmetrik für die Veröffentlichung erreicht wird. *Shouldalert* ist **Bit**, hat den Standardwert NULL. Der Wert **1** bedeutet, dass eine Warnung generiert wird, und der Wert der **0** bedeutet, dass keine Warnung generiert wird.  
  
 [ **@mode** =] *Modus*  
 Gibt an, ob die Schwellenwertmetrik für die Veröffentlichung aktiviert ist. *Modus* ist **"tinyint"**, hat den Standardwert **1**. Der Wert **1** bedeutet, dass die Überwachung dieser Metrik aktiviert ist, und der Wert der **2** bedeutet, dass die Überwachung dieser Metrik deaktiviert ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replmonitorchangepublicationthreshold** wird für alle Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Db_owner** oder **Replmonitor** festen Datenbankrolle "" in der Verteilungsdatenbank kann ausführen **Sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
