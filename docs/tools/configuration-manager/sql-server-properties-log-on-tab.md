---
title: SQL Server-Eigenschaften (Registerkarte Anmelden) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 405073fc-eaa3-43c6-bf82-2cd58cacc1c3
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 623948bfc41640e1aebe0b492872fbc095c056f6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-properties-log-on-tab"></a>SQL Server-Eigenschaften (Registerkarte Anmelden)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verwenden der **anmelden** auf der Registerkarte die **SQL Server-Eigenschaften** (Dialogfeld), das von verwendete Konto anzugeben der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst, das Kennwort des Kontos zu ändern und zu starten und beenden Sie den Dienst. Die Kennwortänderung eines Kontos wird sofort wirksam.  
  
> [!NOTE]  
>  Beim Ändern des Kontonamens, der von einem Dienst auf einer gruppierten Instanz verwendet wird, muss das neue Konto Mitglied der Domänengruppe sein, die während des Setups für den zu ändernden Dienst angegeben wird. Andernfalls müssen Sie die Berechtigung zum Hinzufügen von Mitgliedern zu dieser Gruppe besitzen. Wenden Sie sich an Ihren Domänenadministrator, falls Sie keine Berechtigung zum Ändern der Gruppenmitgliedschaft haben.  
>   
>  Weitere Informationen über das Auswählen eines Kontos zum Ausführen des Dienstes finden Sie unter "Einrichten von Windows-Dienstkonten" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="options"></a>Tastatur  
 **Integriertes Konto**  
 **Lokales System**  
 -   Geben Sie das lokale Systemkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Systemkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Lokaler Dienst**  
 -   Geben Sie das lokale Dienstkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Dienstkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Netzwerkdienst**  
 -   Für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - oder den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst empfiehlt sich die Verwendung des Netzwerkdienstkontos. Lokale Benutzerkonten oder Domänenbenutzerkonten sind für die Dienste besser geeignet.  
  
 **Dieses Konto**  
 Geben Sie ein lokales oder ein Domänenbenutzerkonto an, das die Windows-Authentifizierung verwendet. Das Verwenden eines Domänenbenutzerkontos mit minimalen Berechtigungen für Dienste wird empfohlen.  
  
 **Kontoname**  
 Geben Sie den Kontonamen des lokalen oder Domänenbenutzers an.  
  
 **Kennwort**  
 Geben Sie das Kennwort des Kontos ein.  
  
 **Kennwort bestätigen**  
 Geben Sie das Kennwort des Kontos erneut ein.  
  
 **Start**  
 Starten Sie den Dienst.  
  
 **Beenden**  
 Beenden Sie den Dienst.  
  
 **Anhalten**  
 Halten Sie den Dienst an.  
  
 **Fortsetzen**  
 Setzen Sie einen angehaltenen Dienst fort.  
  
> [!IMPORTANT]  
>  Standardmäßig können nur Mitglieder der lokalen Administratorgruppe einen Dienst starten, beenden, anhalten, fortsetzen oder neu starten. Informationen dazu, wie Sie es Nichtadministratoren ermöglichen, Dienste zu verwalten, finden Sie unter [How to grant users rights to manage services in Windows Server 2003](http://support.microsoft.com/kb/325349)(So erteilen Sie Benutzern die Berechtigung zum Verwalten von Diensten in Windows Server 2003). (Dieser Vorgang ist bei anderen Versionen von Windows ähnlich.)  
  
> [!NOTE]  
>  Beim Starten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]könnte ein WMI-Fehler, der den Ausdruck "Nicht implementiert [0x80004001]" enthält, darauf hinweisen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht auf dem Zielcomputer installiert ist.  
  
  
