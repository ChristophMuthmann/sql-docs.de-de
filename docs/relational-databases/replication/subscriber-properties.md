---
title: Abonnenteneigenschaften | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords: Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e30afaa2582fcb5c0dea17d01338cc520057a7a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="subscriber-properties"></a>Abonnenteneigenschaften
  Das Dialogfeld **Abonnenteneigenschaften** enthält Informationen, die für Abonnenten wichtig sind, auf denen Versionen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ausgeführt werden.  
  
## <a name="options"></a>Optionen  
 **Agentverbindung mit dem Abonnenten**  
 Der Kontext, in dem der Verteilungs-Agent und der Merge-Agent die Verbindung vom Verteiler zum Abonnenten herstellen. Dieser gilt nur für Versionen vor [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Wählen Sie die Option **Identität des Agentprozesskontos annehmen** , um unter Verwendung des Kontexts des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Kontos auf Verteilerebene Verbindungen zum Abonnenten herzustellen. Geben Sie alternativ die **SQL Server-Authentifizierung**an, und geben Sie dann einen Wert für die **Anmeldung** und das **Kennwort**ein. [!INCLUDE[msCoName](../../includes/msconame-md.md)] empfiehlt die Auswahl von **Identität des Agentprozesskontos annehmen**.  
  
 In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen werden die Verbindungsinformationen für jedes Abonnement im Assistent für neue Abonnements angegeben. Die Informationen können im Dialogfeld **Abonnementeigenschaften** geändert werden.  
  
 **Standardzeitpläne für Agent**  
 Der Standardzeitplan, der im Assistenten für neue Abonnements für Abonnenten verwendet wird, auf denen Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vor [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]ausgeführt werden.  
  
 **Sonstiges**  
 Enthält Informationen zum Abonnenten und zum Typ des Abonnenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Eigenschaftenreferenz &#40;Replikation&#41;](../../relational-databases/replication/properties-reference-replication.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
