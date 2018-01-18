---
title: "SQL Server-Eigenschaften (Always On-Registerkarte hohe Verfügbarkeit) | Microsoft Docs"
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
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87645b4a48c157c65876ecfad89a4fef4dcd62c2
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>SQL Server-Eigenschaften (Registerkarte „Always On High Availability Tab“ (Hohe Verfügbarkeit bei Always On))
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Verwenden der **hohe Verfügbarkeit mit AlwaysOn** auf der Registerkarte die **SQL Server-Eigenschaften** im Dialogfeld [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Konfigurations-Manager zum Aktivieren oder deaktivieren Sie die Funktion AlwaysOn-Verfügbarkeitsgruppen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Die Aktivierung von Always On-Verfügbarkeitsgruppen ist eine Voraussetzung dafür, dass eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz Verfügbarkeitsgruppen als Lösung für Hochverfügbarkeit und Notfallwiederherstellung verwenden kann.  
  
##  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Damit eine Serverinstanz für Always On-Verfügbarkeitsgruppen aktiviert werden kann, muss sie die folgenden Voraussetzungen erfüllen:  
  
-   Die Serverinstanz muss sich auf einem WSFC-Knoten (Windows Server Failover Clustering) befinden.  
  
-   Instanzen müssen sich im gleichen WSFC-Cluster befinden, damit sie derselben Verfügbarkeitsgruppe angehören. Eine Verfügbarkeitsgruppe kann sich nicht über mehrere WSFC-Cluster erstrecken.  
  
-   Auf der Serverinstanz muss eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Edition mit [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]-Unterstützung ausgeführt werden.  
  
-   Always On-Verfügbarkeitsgruppen sollten jeweils nur für eine Serverinstanz aktiviert werden. Warten Sie nach der Aktivierung von Always On-Verfügbarkeitsgruppen, bis der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst neu gestartet wurde, bevor Sie die nächste Serverinstanz aktivieren.  
  
> [!NOTE]  
>  Informationen zur Funktionsunterstützung sowie zu zusätzlichen Voraussetzungen, Einschränkungen und Empfehlungen zu [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]finden Sie in der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Onlinedokumentation.  
  
## <a name="dialog-options"></a>Dialogfeldoptionen  
 **Name des Windows-Failoverclusters**  
 Zeigt den Namen des WSFC-Clusters an, in dem der lokale Computer einen Knoten darstellt.  
  
 **Aktivieren von AlwaysOn-Verfügbarkeitsgruppen**  
 Verwenden Sie dieses Kontrollkästchen, um Always On-Verfügbarkeitsgruppen auf dieser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz wie folgt zu aktivieren oder deaktivieren:  
  
-   Wenn dieses Kontrollkästchen leer ist, sind Always On-Verfügbarkeitsgruppen derzeit deaktiviert. Aktivieren Sie dieses Kontrollkästchen, um Always On-Verfügbarkeitsgruppen zu aktivieren, klicken Sie auf **OK**, und starten Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst manuell erneut.  
  
-   Wenn dieses Kontrollkästchen bereits aktiviert ist, sind Always On-Verfügbarkeitsgruppen derzeit aktiviert. Um Always On-Verfügbarkeitsgruppen zu deaktivieren, deaktivieren Sie das Kontrollkästchen, und klicken Sie auf **OK**. Dadurch wird die Serverinstanz neu gestartet.  
  
    > [!TIP]  
    >  Nach der Deaktivierung von Always On-Verfügbarkeitsgruppen sollten Sie alle lokalen Verfügbarkeitsreplikate aus der Serverinstanz entfernen. Nachdem Sie das letzte Replikat einer bestimmten Verfügbarkeitsgruppe entfernt haben, sollten Sie auch die Gruppe entfernen.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
  
> [!NOTE]  
>  Weitere Informationen zu den Schritten, die im Anschluss an die Deaktivierung von Always On-Verfügbarkeitsgruppen erforderlich sind, sowie Informationen zum Erstellen und Konfigurieren von Verfügbarkeitsgruppen finden Sie in der [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Onlinedokumentation.  
  
  
