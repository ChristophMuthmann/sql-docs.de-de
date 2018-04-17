---
title: Sp_vupgrade_replication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d99e942d4b1aeb6e0268398800766366d3e8930f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wird vom Setup-Programm aktiviert, wenn ein Update für einen Replikationsserver durchgeführt wird. Aktualisiert bei Bedarf Schema- und Systemdaten, um die Replikation auf der aktuellen Produktebene zu unterstützen. Erstellt neue Replikationssystemobjekte in System- und Benutzerdatenbanken. Diese gespeicherte Prozedur wird auf dem Computer ausgeführt, auf dem das Replikationsupgrade erfolgen soll.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@login=**] **"***Anmeldung***"**  
 Gibt den Anmeldenamen des Systemadministrators an, der verwendet werden soll, wenn neue Systemobjekte in der Verteilungsdatenbank erstellt werden. *login* ist vom Datentyp **sysname**und hat den Standardwert NULL. Dieser Parameter ist nicht erforderlich, wenn *Security_mode* festgelegt ist, um **1**, d. h. auf Windows-Authentifizierung.  
  
> [!NOTE]  
>  Dieser Parameter wird ignoriert, wenn Sie ein Upgrade auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höhere Versionen durchführen.  
  
 [  **@password=**] **"***Kennwort***"**  
 Ist das Kennwort des Systemadministrators zu verwenden, wenn neue Systemobjekte in der Verteilungsdatenbank zu erstellen. *Kennwort* ist **Sysname**, hat den Standardwert **''** (leere Zeichenfolge). Dieser Parameter ist nicht erforderlich, wenn *Security_mode* festgelegt ist, um **1**, d. h. auf Windows-Authentifizierung.  
  
> [!NOTE]  
>  Dieser Parameter wird ignoriert, wenn Sie eine auf SQL Aktualisierung [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen.  
  
 [  **@ver_old=**] **"***Old_version***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 Diese gespeicherte Prozedur ist als veraltet markiert und wird in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entfernt.  
  
 [  **@force_remove=**] **"***Force_removal***"**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **"***Security_mode***"**  
 Gibt den Anmeldungssicherheitsmodus an, der verwendet werden soll, wenn neue Systemobjekte in der Verteilungsdatenbank erstellt werden. *Security_mode* ist **Bit** hat den Standardwert des **0**. Wenn **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung verwendet. Wenn **1**, Windows-Authentifizierung verwendet werden.  
  
> [!NOTE]  
>  Dieser Parameter wird ignoriert, wenn Sie ein Upgrade auf [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höhere Versionen durchführen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_vupgrade_replication** wird bei der Aktualisierung von allen Replikationstypen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Sysadmin** -Serverrolle kann ausführen **Sp_vupgrade_replication**.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md)  
  
  
