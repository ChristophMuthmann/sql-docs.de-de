---
title: HOST_NAME-Werte | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 609fd9472a8bd88b4c3b5cb290dfcf6da5e8757d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="hostname-values"></a>HOST_NAME-Werte
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In Mergeveröffentlichungen mit parametrisierten Filtern werden zum Filtern der Daten die SUSER_SNAME()-Funktion und/oder die HOST_NAME()-Funktion verwendet. Die Funktion wird im Assistenten für neue Veröffentlichung oder im Dialogfeld **Veröffentlichungseigenschaften** angegeben.  
  
 Standardmäßig wird durch die HOST_NAME()-Funktion der Name des Computers zurückgegeben, der die Verbindung mit dem Verleger herstellt. Wenn Sie parametrisierte Filter verwenden, wird dieser Wert normalerweise überschrieben, indem Sie auf dieser Seite des Assistenten einen Wert bereitstellen. Daraufhin wird durch die HOST_NAME()-Funktion nicht der Name des Computers, sondern der von Ihnen angegebene Wert zurückgegeben. Weitere Informationen finden Sie im Abschnitt „Überschreiben des HOST_NAME()-Wertes“ in [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
> [!NOTE]  
>  Wenn Sie HOST_NAME() überschreiben, wird für sämtliche Aufrufe der HOST_NAME()-Funktion der von Ihnen angegebene Wert zurückgegeben. Stellen Sie sicher, dass keine andere Anwendung darauf angewiesen ist, dass HOST_NAME() den Computernamen zurückgibt.  
  
## <a name="options"></a>Tastatur  
 **Abonnementeigenschaften**  
 Geben Sie in der **HOST_NAME Value** -Spalte für jeden Abonnenten einen Wert ein, oder übernehmen Sie den als Standardwert angegebenen Namen des Abonnentencomputers.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
