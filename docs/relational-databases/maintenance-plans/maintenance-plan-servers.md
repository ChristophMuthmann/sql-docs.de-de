---
title: Wartungsplan (Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d5dc28d4981d00b357f292724a2899d703f4f89
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="maintenance-plan-servers"></a>Wartungsplan (Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe des Dialogfelds **Server** können Sie die Server auswählen, auf denen der Wartungsplan ausgeführt werden soll.  
  
 Es muss eine Multiserverumgebung mit einem Masterserver und mindestens einem Zielserver konfiguriert sein, um einen Multiserver-Wartungsplan erstellen zu können. Für Multiserver-Wartungspläne sollte der lokale Server als Masterserver konfiguriert werden. Bei Multiserverumgebungen werden in diesem Dialogfeld der **(lokale)** Masterserver und alle entsprechenden Zielserver angezeigt. Für den lokalen Server wird ein Auftrag des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents erstellt. Er wird aktiviert oder deaktiviert, je nachdem, ob Sie den **(lokalen)** Server auswählen. Wenn Zielserver ausgewählt sind, wird für jeden ausgewählten Zielserver ein Multiserverauftrag erstellt und auf diesen heruntergeladen. Wenn keine Zielserver ausgewählt sind, wird der Multiserverauftrag gelöscht.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Erstellen einer Multiserverumgebung](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6)   
 [Einrichten eines Masterservers](http://msdn.microsoft.com/library/05739a73-1fdf-4d9d-92a6-70f328380322)   
 [Erstellen eines Zielservers](http://msdn.microsoft.com/library/13aabe2d-67fe-4c67-8d49-2928dd705b7a)  
  
  
