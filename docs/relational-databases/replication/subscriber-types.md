---
title: Abonnententypen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eecf0e51d45edaa4d13fae76c87ad6019d4c2d70
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="subscriber-types"></a>Abonnententypen
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Mithilfe der Mergereplikation können Sie die Typen der Abonnenten angeben, die eine Veröffentlichung unterstützen muss. Die Auswahl der Abonnententypen legt den *Veröffentlichungskompatibilitätsgrad*fest, der bestimmt, welche Funktionen von einer Veröffentlichung verwendet werden können.  
  
 Nachdem eine Veröffentlichungsmomentaufnahme erstellt wurde, kann der Veröffentlichungskompatibilitätsgrad im Dialogfeld **Veröffentlichungseigenschaften** auf der Seite **Allgemein** gesteigert (restriktiver gemacht) werden. Der Veröffentlichungskompatibilitätsgrad kann nicht gesenkt werden.  
  
## <a name="options"></a>Tastatur  
 Wählen Sie jeden Abonnententypen aus, der von der Veröffentlichung unterstützt werden muss.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Die Veröffentlichung kann alle Funktionen verwenden.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 Momentaufnahmedateien für die Veröffentlichung müssen ein Zeichenformat aufweisen (dies wird automatisch vom Momentaufnahme-Agent gehandhabt). Für[!INCLUDE[ssEW](../../includes/ssew-md.md)] gilt auch eine Reihe von Einschränkungen ohne Bezug zum Kompatibilitätsgrad.  
  
 Wenn diese Option ausgewählt ist, dann ist die Option zur Websynchronisierung für die Veröffentlichung aktiviert. Weitere Informationen zur Websynchronisierung finden Sie unter [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Eigenschaftenreferenz &#40;Replikation&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
