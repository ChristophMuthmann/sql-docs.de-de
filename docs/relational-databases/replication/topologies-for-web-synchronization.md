---
title: "Topologien f&#252;r die Websynchronisierung | Microsoft Docs"
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
  - "Websynchronisierung, Topologien"
  - "IIS-Serverkonfiguration [SQL Server-Replikation]"
ms.assetid: 59444faf-bcb6-4421-a3df-8715753e453b
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Topologien f&#252;r die Websynchronisierung
  Sie können aus unterschiedlichen Websynchronisierungs-Replikationstopologien von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auswählen. Hier einige der gängigen Konfigurationsmethoden für die Websynchronisierung:  
  
-   Einzelner Server  
  
-   Zwei Server  
  
-   Mehrere Systeme mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internetinformationsdiensten (IIS, Internet Information Services) und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Wiederveröffentlichung  
  
 Informationen zum Konfigurieren der websynchronisierung finden Sie unter [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Einzelner Server  
 In der einfachsten Topologie befinden sich IIS, der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger sowie der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler auf einem einzigen Server. Die Abonnenten führen den Synchronisierungsvorgang aus, indem sie mit IIS auf dem Verleger eine Verbindung herstellen. Der Verleger kann sich hinter einer Firewall befinden.  
  
> [!NOTE]  
>  Diese Konfiguration wird nur für Intranetszenarien empfohlen. Bei anderen Szenarien sollten sich der IIS-Server und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verleger/-Verteiler auf separaten Computern befinden.  
  
 ![Websynchronisierung mit einem einzelnen Server](../../relational-databases/replication/media/web-sync02.gif "Websynchronisierung mit einem einzelnen Server")  
  
## Zwei Server  
 Sie können IIS auf dem einen Server installieren und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verleger/-Verteiler auf dem anderen Server konfigurieren. Der Server, auf dem IIS ausgeführt wird, kann durch eine Firewall vom Internet isoliert werden. Die Abonnenten führen den Synchronisierungsvorgang aus, indem sie mit IIS auf dem Verleger eine Verbindung herstellen.  
  
 ![Websynchronisierung mit zwei Servern](../../relational-databases/replication/media/web-sync03.gif "Websynchronisierung mit zwei Servern")  
  
## Mehrere IIS-Systeme und SQL Server-Wiederveröffentlichung  
 Wenn eine große Anzahl an Abonnenten unterstützt werden müssen, die gleichzeitig synchronisieren, kann die Arbeitsauslastung auf mehrere Computer verteilt werden, auf denen IIS ausgeführt wird.  
  
 ![Websynchronisierung mit mehreren IIS-Servern](../../relational-databases/replication/media/web-sync04.gif "Websynchronisierung mit mehreren IIS-Servern")  
  
 Wenn auf dem Computer, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt ist, weiterer Lastenausgleich erforderlich ist, können Sie auf mehreren Computern eine Wiederveröffentlichungshierarchie erstellen. Der Verleger der obersten Ebene veröffentlicht Daten für Abonnenten, die die Daten wiederum erneut veröffentlichen; hierbei erfolgt der Lastenausgleich hinsichtlich Anforderungen von Abonnenten.  
  
> [!NOTE]  
>  Abonnenten können nur mit einem bestimmten Verleger synchronisiert werden. Beispielsweise kann ein Abonnent von Neuverleger A nicht mit Neuverleger B synchronisiert werden, wenn A nicht verfügbar ist.  
  
 ![Websynchronisierung mit Wiederveröffentlichung](../../relational-databases/replication/media/web-sync05.gif "Websynchronisierung mit Wiederveröffentlichung")  
  
## Siehe auch  
 [Websynchronisierung konfigurieren](../../relational-databases/replication/configure-web-synchronization.md)   
 [Websynchronisierung für die Mergereplikation](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  