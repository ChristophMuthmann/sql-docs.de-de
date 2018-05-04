---
title: Sp_adddistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 49b2250ac8c6a6ec634c1e141c28cc5056a80a24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen Eintrag in der [sys.sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) Tabelle (sofern es nicht), markiert ihn als Verteiler und speichert Eigenschafteninformationen. Diese gespeicherte Prozedur wird auf dem Verteiler für die master-Datenbank ausgeführt, um den Server als Verteiler zu registrieren und zu markieren. Im Falle eines Remoteverteilers wird sie zusätzlich auf dem Verleger für die master-Datenbank ausgeführt, um den Remoteverteiler zu registrieren.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@distributor=**] **"***Verteiler***"**  
 Der Verteilungsservername. *Verteiler* ist **Sysname**, hat keinen Standardwert. Dieser Parameter wird nur bei der Einrichtung eines Remoteverteilers verwendet. Er fügt Einträge für die Verteilereigenschaften der **Msdb... MSdistributor** Tabelle.  
  
 [  **@heartbeat_interval=**] *Heartbeat_interval*  
 Die maximale Anzahl von Minuten, für die ein Agent ausgeführt werden kann, ohne dass eine Statusmeldung protokolliert wird. *Heartbeat_interval* ist **Int**, hat den Standardwert von 10 Minuten. Ein Auftrag des SQL Server-Agents wird erstellt, der nach diesem Zeitraum ausgeführt wird, um den Status der ausgeführten Replikations-Agents zu überprüfen.  
  
 [  **@password=**] **"***Kennwort***"**]  
 Das Kennwort des der **Distributor_admin** Anmeldung. *Kennwort* ist **Sysname**, hat den Standardwert NULL. Bei NULL oder einer leeren Zeichenfolge wird das Kennwort auf einen Zufallswert festgelegt. Das Kennwort muss konfiguriert sein, wenn der erste Remoteverteiler hinzugefügt wird. **Distributor_admin** Anmeldung und *Kennwort* gespeichert sind, für den verbindungsservereintrag für eine *Verteiler* RPC-Verbindung, einschließlich lokaler Verbindungen. Wenn *Verteiler* ist lokal, das Kennwort für **Distributor_admin** auf einen neuen Wert festgelegt ist. Für Verleger mit einem Remoteverteiler der gleiche Wert für *Kennwort* muss angegeben werden, für die Ausführung **Sp_adddistributor** auf dem Verleger und Verteiler. [Sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) kann zum Ändern des verteilerkennworts verwendet werden.  
  
> [!IMPORTANT]  
>  Benutzer sollten nach Möglichkeit dazu aufgefordert werden, Anmeldeinformationen zur Laufzeit anzugeben. Wenn Anmeldeinformationen in einer Skriptdatei gespeichert werden müssen, muss die Datei an einem sicheren Ort gespeichert werden, um unberechtigten Zugriff zu vermeiden.  
  
 [  **@from_scripting=** ] *From_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_adddistributor** wird bei der Momentaufnahme-, Transaktions- und Mergereplikation verwendet.  
  
## <a name="example"></a>Beispiel  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_adddistributor**.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [Sp_dropdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Verteilung konfigurieren](../../relational-databases/replication/configure-distribution.md)  
  
  
