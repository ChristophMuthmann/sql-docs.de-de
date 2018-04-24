---
title: Veröffentlichungsdatenbank | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
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
- sql13.rep.newpubwizard.publicationdatabase.f1
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5453a747b502c01f7bc16b5e0f0bd18c9c2669e8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="publication-database"></a>Veröffentlichungsdatenbank
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Bei der Veröffentlichungsdatenbank handelt es sich um die Datenbank auf dem Verleger, die als Quelle der zu replizierenden Daten und Datenbankobjekte fungiert. Die in einer Replikation verwendeten Veröffentlichungsdatenbanken müssen aktiviert werden. Die Datenbank wird aktiviert, wenn ein Mitglied der festen Serverrolle **sysadmin** Folgendes ausführt:  
  
-   Erstellt eine Veröffentlichung auf der betreffenden Datenbank mithilfe des Assistenten für neue Veröffentlichung.  
  
-   Wählt die Datenbank im Dialogfeld **Verlegereigenschaften** aus.  
  
-   Führt **sp_replicationdboption** aus und legt für die Option **publish** (bei Momentaufnahme- oder Transaktionsveröffentlichungen) oder die Option **merge publish** (bei Mergeveröffentlichungen) **True**fest.  
  
## <a name="options"></a>Tastatur  
 **Datenbanken**  
 Wählen Sie den Namen der Datenbank aus, die die Daten und Datenbankobjekte enthält, die veröffentlicht werden sollen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  
