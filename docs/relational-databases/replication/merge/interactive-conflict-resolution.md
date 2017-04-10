---
title: "Interaktive Konfliktl&#246;sung | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Interaktive Konfliktlösung [SQL Server-Replikation]"
  - "Interaktiver Konfliktlöser [SQL Server-Replikation]"
  - "Artikel [SQL Server-Replikation], Konfliktlösung"
  - "Konfliktlösung [SQL Server-Replikation], Mergereplikation "
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Interaktive Konfliktl&#246;sung
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die Replikation bietet eine interaktive Konfliktlöser, können Sie zum manuellen Beheben von Konflikten während der bedarfsgesteuerten Synchronisierung in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Synchronisierungsverwaltung von Windows. Der interaktive Konfliktlöser, der zur Laufzeit aktiviert wird, ist eine grafische Schnittstelle, mit der Daten für jede konfliktverursachende Zeile angezeigt und Optionen zum Anzeigen und Bearbeiten der Konfliktdaten sowie zum individuellen Lösen aller Konflikte bereitgestellt werden.  
  
 Der interaktive Konfliktlöser ist mit dem Konflikt-Viewer vergleichbar. Der Konflikt-Viewer zeigt jedoch die Ergebnisse von Konflikten an, die nach der Mergesynchronisierung bereits gelöst sind, während der interaktive Konfliktlöser einen Konflikt vor der Lösung anzeigt und Ihnen ermöglicht, das Ergebnis eines Konflikts während der Mergesynchronisierung zu bestimmen. Wenn ein Konflikt auftritt, sollte ein Benutzer zur Verfügung stehen, um den interaktiven Konfliktlöser zu überwachen.  
  
> [!NOTE]  
>  Für die interaktive Konfliktlösung ist die Synchronisierungsverwaltung von Windows erforderlich. Wenn die Synchronisierung nicht im Rahmen der Synchronisierungsverwaltung von Windows erfolgt (sondern als geplante Synchronisierung oder als bedarfsgesteuerte Synchronisierung in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] oder des Replikationsmonitors), werden Konflikte ohne Benutzereingriff automatisch gemäß dem Konfliktlöser gelöst, der für den Artikel angegeben ist. Konflikte im Zusammenhang mit logischen Datensätzen werden nicht im interaktiven Konfliktlöser angezeigt. Mit den gespeicherten Replikationsprozeduren können Informationen zu diesen Konflikten angezeigt werden. Weitere Informationen finden Sie unter [Anzeigen von Konfliktinformationen für Mergeveröffentlichungen & #40; Replikationsprogrammierung mit Transact-SQL & #41;](../../../relational-databases/replication/view conflict information for merge publications.md).  
  
## Artikelkonfliktlöser und der interaktive Konfliktlöser  
 Konfliktlöser (entweder der Standardkonfliktlöser, ein Geschäftslogikhandler oder ein benutzerdefinierter Konfliktlöser) werden beim Erstellen einer Veröffentlichung bestimmten Artikeln zugewiesen und verwenden eine Gruppe von vordefinierten Regeln, um die zu verwendende Datengruppe zu bestimmen, wenn konfliktverursachende Zeilendaten eingegeben werden. Der interaktive Konfliktlöser ist kein separater Konfliktlöser mit Regeln zum Bestimmen von Konfliktgewinnern und -verlierern, sondern ein Tool, das zusammen mit dem Standardkonfliktlöser und den benutzerdefinierten Konfliktlösern verwendet wird. Der Artikelkonfliktlöser bestimmt zwar die gewinnende und die verlierende Zeile, der interaktive Konfliktlöser ermöglicht aber den Benutzereingriff, um die Ergebnisse zu akzeptieren, abzulehnen oder zu ändern.  
  
 Damit der interaktive Konfliktlöser verwendet werden kann, muss die interaktive Konfliktlösung für alle Artikel und alle Abonnements aktiviert sein, für die sie erforderlich ist. Wenn der interaktive Konfliktlöser für einen oder mehrere Artikel und Abonnements aktiviert wurde, wird er verwendet, wenn während einer Mergesynchronisierung ein Konflikt erkannt wird.  
  
 Für die Verwendung des interaktiven Konfliktlösers finden Sie unter [Angeben der interaktiven Konfliktlösung für Mergeveröffentlichungen](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md) und [synchronisieren Sie ein Abonnement mithilfe von Windows Synchronization Manager & #40; Windows-Synchronisierungs-Manager & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
## Siehe auch  
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  