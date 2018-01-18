---
title: SQL-Volltextfilterdaemon-Startprogramm (Registerkarte Anmelden) | Microsoft Docs
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
ms.assetid: 13e260f9-a75f-430b-88a3-959ddcead8fe
caps.latest.revision: "9"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d1c6b9e4c73f1df1aafc3940a44b51149a7121b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="sql-full-text-filter-daemon-launcher-log-on-tab"></a>Startprogramm für SQL-Volltextfilterdaemon (Registerkarte Anmelden)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQL Volltext-Filter-Startprogramm (FDHOST-Startprogramm) Inanspruchnahme von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Volltext-Suchdienst. Dieser Dienst muss ausgeführt werden, wenn Sie die Volltextsuche verwenden. Informationen über die Prozesse des Filterdaemonhosts finden Sie unter "Architektur der Volltextsuche" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
 Verwenden Sie im Dialogfeld **Eigenschaften von Startprogramm für SQL-Volltextfilterdaemon** die Registerkarte **Anmelden** , um das vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Volltextdienst verwendete Konto anzugeben, das Kennwort des Kontos zu ändern sowie den Dienst zu starten und zu beenden. Das Ändern eines Kennworts für ein Konto wird nach einem Neustart des Diensts wirksam.  
  
> [!NOTE]  
>  Beim Ändern des Kontonamens, der von einem Dienst auf einer gruppierten Instanz verwendet wird, muss das neue Konto Mitglied der Domänengruppe sein, die während des Setups für den zu ändernden Dienst angegeben wird, oder Sie müssen die Berechtigung zum Hinzufügen von Mitgliedern zu dieser Gruppe besitzen. Wenden Sie sich an Ihren Domänenadministrator, falls Sie keine Berechtigung zum Ändern der Gruppenmitgliedschaft haben.  
>   
>  Weitere Informationen über das Auswählen eines Kontos zum Ausführen des Dienstes finden Sie unter "Einrichten von Windows-Dienstkonten" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="options"></a>enthalten  
 **Integriertes Konto**  
 **Lokales System**  
 Geben Sie das lokale Systemkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Systemkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Lokaler Dienst**  
 Geben Sie das lokale Dienstkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Dienstkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Netzwerkdienst**  
 Für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienste empfiehlt sich die Verwendung des Netzwerkdienstkontos. Lokale Benutzerkonten oder Domänenbenutzerkonten sind für die Dienste besser geeignet.  
  
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
 Halten Sie den Dienst an. Für diesen Dienst nicht verfügbar.  
  
 **Fortsetzen**  
 Setzen Sie einen angehaltenen Dienst fort.  
  
  
