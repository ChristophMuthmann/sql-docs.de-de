---
title: Anzeigen der Eigenschaften eines Facets der richtlinienbasierten Verwaltung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
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
- Policy-Based Management, view facet properties
ms.assetid: 022a244c-c2e7-4467-b9a2-c7a27859be22
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e304f1ca0ddb0b22206201b853a2d5d30adb4ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="view-the-properties-of-a-policy-based-management-facet"></a>Anzeigen der Eigenschaften eines Facets der richtlinienbasierten Verwaltung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie die Eigenschaften eines Facets der richtlinienbasierten Verwaltung i mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **Anzeigen der Eigenschaften eines Facets mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-a-facet"></a>So zeigen Sie die Eigenschaften eines Facets an  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, in dem das Facet mit den anzuzeigenden Eigenschaften enthalten ist.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Facets** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Facet, dessen Eigenschaften Sie anzeigen möchten, und wählen Sie **Eigenschaften**aus. Weitere Informationen über die verfügbaren Optionen im Dialogfeld **Faceteigenschaften** > *Facetname* finden Sie unter [Facet Properties Dialog Box, General Page (Dialogfeld „Faceteigenschaften“, Seite „Allgemein“)](../../relational-databases/policy-based-management/facet-properties-dialog-box-general-page.md), [Facet Properties Dialog Box, Dependent Policies Page (Dialogfeld „Faceteigenschaften“, Seite „Abhängige Richtlinien“)](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-policies-page.md) und [Facet Properties Dialog Box, Dependent Conditions Page (Dialogfeld „Faceteigenschaften“, Seite „Abhängige Bedingungen“)](../../relational-databases/policy-based-management/facet-properties-dialog-box-dependent-conditions-page.md).  
  
6.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
  
