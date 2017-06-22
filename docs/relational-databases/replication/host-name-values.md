---
title: HOST_NAME-Werte | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c8175cd22da36e5b07c0c7b0807701d64df3d8d8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="hostname-values"></a>HOST_NAME-Werte
  In Mergeveröffentlichungen mit parametrisierten Filtern werden zum Filtern der Daten die SUSER_SNAME()-Funktion und/oder die HOST_NAME()-Funktion verwendet. Die Funktion wird im Assistenten für neue Veröffentlichung oder im Dialogfeld **Veröffentlichungseigenschaften** angegeben.  
  
 Standardmäßig wird durch die HOST_NAME()-Funktion der Name des Computers zurückgegeben, der die Verbindung mit dem Verleger herstellt. Wenn Sie parametrisierte Filter verwenden, wird dieser Wert normalerweise überschrieben, indem Sie auf dieser Seite des Assistenten einen Wert bereitstellen. Daraufhin wird durch die HOST_NAME()-Funktion nicht der Name des Computers, sondern der von Ihnen angegebene Wert zurückgegeben. Weitere Informationen finden Sie im Abschnitt „Überschreiben des HOST_NAME()-Wertes“ in [Parametrisierte Zeilenfilter](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
> [!NOTE]  
>  Wenn Sie HOST_NAME() überschreiben, wird für sämtliche Aufrufe der HOST_NAME()-Funktion der von Ihnen angegebene Wert zurückgegeben. Stellen Sie sicher, dass keine andere Anwendung darauf angewiesen ist, dass HOST_NAME() den Computernamen zurückgibt.  
  
## <a name="options"></a>Optionen  
 **Abonnementeigenschaften**  
 Geben Sie in der **HOST_NAME Value** -Spalte für jeden Abonnenten einen Wert ein, oder übernehmen Sie den als Standardwert angegebenen Namen des Abonnentencomputers.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen eines Pullabonnements](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Anzeigen und Ändern der Eigenschaften von Pullabonnements](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Anzeigen und Ändern der Eigenschaften von Pushabonnements](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/host-name-transact-sql.md)   
 [Abonnieren von Veröffentlichungen](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
