---
title: dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77f8652347f0093b84be4853880bb504defc3b6c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Gibt eine Zeile für jede Eigenschaft in Verbindung mit der CLR-Integration (Common Language Runtime) von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück, einschließlich der Version und des Status der gehosteten CLR. Die gehostete CLR wird initialisiert, indem Sie mit der [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), oder [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) -Anweisungen oder durch Ausführen alle CLR-Routine, Typ oder Trigger. Die **dm_clr_properties** -Sicht wird nicht angegeben, ob die Ausführung von benutzerdefiniertem CLR-Code auf dem Server aktiviert wurde. Ausführung von benutzerdefiniertem CLR-Code aktiviert ist, mithilfe der [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) gespeicherte Prozedur mit der [Clr-fähig](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) option auf 1 festgelegt ist.  
  
 Die **dm_clr_properties** -Ansicht enthält die **Namen** und **Wert** Spalten. Jede Zeile in dieser Sicht enthält Details zu einer Eigenschaft der gehosteten CLR. Mit dieser Sicht können Sie Informationen zur gehosteten CLR zusammentragen, z. B. das CLR-Installationsverzeichnis, die CLR-Version und den aktuellen Status der gehosteten CLR. Mit dieser Sicht können Sie bestimmen, ob der CLR-Integrationscode aufgrund von Problemen mit der CLR-Installation auf dem Servercomputer nicht funktioniert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Der Name der Eigenschaft.|  
|**value**|**nvarchar(128)**|Wert der Eigenschaft.|  
  
## <a name="properties"></a>Eigenschaften  
 Die **Directory** Eigenschaft gibt an, das Verzeichnis, das .NET Framework auf dem Server installiert wurde. Möglicherweise sind mehrere Installationen von .NET Framework auf dem Servercomputer vorhanden, und durch den Wert dieser Eigenschaft wird angegeben, welche Installation derzeit von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet wird.  
  
 Die **Version** Eigenschaft gibt die Version von .NET Framework und der gehosteten CLR auf dem Server.  
  
 Die **dm_clr_properties** dynamische verwaltungssicht kann zurückgeben sechs verschiedene Werte für die **Status** -Eigenschaft, die den Zustand des widerspiegelt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gehosteten CLR. Die Überladungen sind:  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 Die **Mscoree wurde nicht geladen** und **Mscoree geladen** Zuständen zeigen den Fortschritt der Initialisierung der gehosteten CLR beim Start des Servers und voraussichtlich nicht angezeigt werden.  
  
 Die **gesperrt CLR-Version mit Mscoree** Status wird angezeigt, in denen die gehostete CLR nicht verwendet wird, und daher, es wurde noch nicht initialisiert wurde. Die gehostete CLR wird initialisiert das erste Mal eine DDL-Anweisung (z. B. [CREATE ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md)) oder ein verwaltetes Datenbankobjekt ausgeführt wird.  
  
 Die **CLR wird initialisiert** Status bedeutet, dass die gehostete CLR erfolgreich initialisiert wurde. Beachten Sie, dass dadurch nicht angegeben wird, ob die Ausführung von benutzerdefiniertem CLR-Code aktiviert wurde. Wenn die Ausführung von benutzerdefiniertem CLR-Code first ist aktiviert, und klicken Sie dann mit deaktiviert die [!INCLUDE[tsql](../../includes/tsql-md.md)] [Sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) gespeicherte Prozedur der Statuswert werden trotzdem **CLR wird initialisiert**.  
  
 Die **CLR Initialisierungsfehler dauerhaft** Status zeigt an, der gehosteten CLR Fehler bei der Initialisierung. Mögliche Gründe sind ungenügend Arbeitsspeicher oder ein Fehler im Hosthandshake zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und der CLR. In diesem Fall wird die Fehlermeldung 6512 oder 6513 ausgegeben.  
  
 Die **CLR wird beendet Zustand** wird nur angezeigt, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] heruntergefahren wird.  
  
## <a name="remarks"></a>Hinweise  
 Die Eigenschaften und Werte dieser Sicht möglicherweise ändern, in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufgrund von Verbesserungen an der CLR-Integrationsfunktionalität.  
  
## <a name="permissions"></a>Berechtigungen  
 Auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
 Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] benötigen Premium-Ebenen die VIEW DATABASE STATE-Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die [!INCLUDE[ssSDS](../../includes/sssds-md.md)] -Administratorkonto ein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Informationen zur gehosteten CLR abgerufen:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Common Language Runtime in Verbindung mit dynamischen Verwaltungssichten &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
