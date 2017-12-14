---
title: Webserverinformationen | Microsoft-Dokumentation
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
f1_keywords: sql13.rep.newsubwizard.webserverinformation.f1
ms.assetid: 86d72275-45c7-459f-98cf-f5a366ed279c
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ed7c0bf464296693b5a036684d55f94c56b439c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="web-server-information"></a>Webserverinformationen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Webserverinformationen sind erforderlich, um die Websynchronisierungsoption für die Mergereplikation zu verwenden. Informationen zur Konfiguration der Websynchronisierung finden Sie unter [Konfigurieren der Websynchronisierung](../../relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="options"></a>enthalten  
 **Webserveradresse**  
 Wenn Sie auf der Seite **FTP-Momentaufnahme und Internet** des Dialogfelds **Veröffentlichungseigenschaften** eine Webserveradresse angegeben haben, wird diese in diesem Feld als Standardwert angezeigt. Übernehmen Sie entweder den Standardwert, oder geben Sie eine vollqualifizierte Webserveradresse für den Server für [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internetinformationsdienste (IIS, Internet Information Services) an, der diese Abonnements synchronisiert.  
  
 **Wie stellt der Abonnent eine Verbindung mit dem Webserver her?**  
 Geben Sie den für das Herstellen einer Verbindung mit dem Webserver verwendeten Authentifizierungstyp an. Sie sollten für SSL-Verbindungen (Secure Sockets Layer) mit dem IIS-Server die Standardauthentifizierung verwenden. Geben Sie bei Auswahl der Standardauthentifizierung den Anmeldenamen und das Kennwort ein, die beim Herstellen der Verbindung vom Abonnenten zum IIS-Server verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Nicht-SQL Server-Abonnenten](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)   
 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
