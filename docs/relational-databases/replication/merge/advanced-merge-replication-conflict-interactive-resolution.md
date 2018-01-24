---
title: "Interaktive Konfliktlösung | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0acc68329b1b9b07633c24db2521f5cf3502b38f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="advanced-merge-replication-conflict---interactive-resolution"></a>Erweiterte Konflikte bei der Mergereplikation – Interaktive Lösung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Replikation steht ein interaktiver Konfliktlöser zur Verfügung, mit dem Sie Konflikte bei einer bedarfsgesteuerten Synchronisierung in der Synchronisierungsverwaltung von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows manuell lösen können. Der interaktive Konfliktlöser, der zur Laufzeit aktiviert wird, ist eine grafische Schnittstelle, mit der Daten für jede konfliktverursachende Zeile angezeigt und Optionen zum Anzeigen und Bearbeiten der Konfliktdaten sowie zum individuellen Lösen aller Konflikte bereitgestellt werden.  
  
 Der interaktive Konfliktlöser ist mit dem Konflikt-Viewer vergleichbar. Der Konflikt-Viewer zeigt jedoch die Ergebnisse von Konflikten an, die nach der Mergesynchronisierung bereits gelöst sind, während der interaktive Konfliktlöser einen Konflikt vor der Lösung anzeigt und Ihnen ermöglicht, das Ergebnis eines Konflikts während der Mergesynchronisierung zu bestimmen. Wenn ein Konflikt auftritt, sollte ein Benutzer zur Verfügung stehen, um den interaktiven Konfliktlöser zu überwachen.  
  
> [!NOTE]  
>  Für die interaktive Konfliktlösung ist die Synchronisierungsverwaltung von Windows erforderlich. Wenn die Synchronisierung nicht im Rahmen der Synchronisierungsverwaltung von Windows erfolgt (sondern als geplante Synchronisierung oder als bedarfsgesteuerte Synchronisierung in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder des Replikationsmonitors), werden Konflikte ohne Benutzereingriff automatisch gemäß dem Konfliktlöser gelöst, der für den Artikel angegeben ist. Konflikte im Zusammenhang mit logischen Datensätzen werden nicht im interaktiven Konfliktlöser angezeigt. Mit den gespeicherten Replikationsprozeduren können Informationen zu diesen Konflikten angezeigt werden. Weitere Informationen finden Sie unter [Anzeigen von Konfliktinformationen zu Mergeveröffentlichungen &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>Artikelkonfliktlöser und der interaktive Konfliktlöser  
 Konfliktlöser (entweder der Standardkonfliktlöser, ein Geschäftslogikhandler oder ein benutzerdefinierter Konfliktlöser) werden beim Erstellen einer Veröffentlichung bestimmten Artikeln zugewiesen und verwenden eine Gruppe von vordefinierten Regeln, um die zu verwendende Datengruppe zu bestimmen, wenn konfliktverursachende Zeilendaten eingegeben werden. Der interaktive Konfliktlöser ist kein separater Konfliktlöser mit Regeln zum Bestimmen von Konfliktgewinnern und -verlierern, sondern ein Tool, das zusammen mit dem Standardkonfliktlöser und den benutzerdefinierten Konfliktlösern verwendet wird. Der Artikelkonfliktlöser bestimmt zwar die gewinnende und die verlierende Zeile, der interaktive Konfliktlöser ermöglicht aber den Benutzereingriff, um die Ergebnisse zu akzeptieren, abzulehnen oder zu ändern.  
  
 Damit der interaktive Konfliktlöser verwendet werden kann, muss die interaktive Konfliktlösung für alle Artikel und alle Abonnements aktiviert sein, für die sie erforderlich ist. Wenn der interaktive Konfliktlöser für einen oder mehrere Artikel und Abonnements aktiviert wurde, wird er verwendet, wenn während einer Mergesynchronisierung ein Konflikt erkannt wird.  
  
 Informationen zur Verwendung des interaktiven Konfliktlösers finden Sie unter [Angeben der interaktiven Konfliktlösung für Mergeveröffentlichungen](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md) und [Synchronisieren eines Abonnements mithilfe der Synchronisierungsverwaltung von Windows &#40;Windows Synchronization Manager&#41;](../../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Advanced Merge Replication Conflict Detection and Resolution (Erweiterte Konflikterkennung und -lösung bei der Mergereplikation)](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
