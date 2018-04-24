---
title: Anzeigen der Facets der richtlinienbasierten Verwaltung für ein SQL Server-Objekt | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2222dd3c6b28d1d30469c5adbf85062c419e22c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>Anzeigen der Facets der richtlinienbasierten Verwaltung für ein SQL Server-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie alle Facets der richtlinienbasierten Verwaltung, die auf ein bestimmtes SQL Server-Objekt in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] angewendet wurden, mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **Anzeigen aller Facets in einem Objekt mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>So zeigen Sie alle Facets in einem Objekt an  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ein Instanzobjekt, eine Datenbank oder ein Datenbankobjekt, und klicken Sie dann auf **Facets**.  
  
2.  Wählen Sie im Dialogfeld **Facets anzeigen** > *Objektname* in der Liste **Facet** ein Facet aus, dessen Eigenschaften Sie anzeigen möchten. Weitere Informationen zu den Optionen in diesem Dialogfeld finden Sie unter [View Facets Dialog Box](../../relational-databases/policy-based-management/view-facets-dialog-box.md).  
  
3.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
  
