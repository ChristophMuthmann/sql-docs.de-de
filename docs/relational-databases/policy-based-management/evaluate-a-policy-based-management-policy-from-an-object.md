---
title: Auswerten einer Richtlinie der richtlinienbasierten Verwaltung von einem Objekt aus | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: b9e9d646-4894-4dee-a02a-0c71a8dc020e
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f875e9b7858937d69a1106e8a08d139aefe6e445
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="evaluate-a-policy-based-management-policy-from-an-object"></a>Auswerten einer Richtlinie der richtlinienbasierten Verwaltung von einem Objekt aus
  In diesem Thema wird beschrieben, wie eine Richtlinie aus einer Serverinstanz, Datenbank oder einem Datenbankobjekt in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ausgewertet wird.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   **Auswerten einer Richtlinie aus einem Objekt mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Ausführungsmodus wird als Teil der Richtlinie definiert und kann im Dialogfeld **Richtlinien auswerten** nicht geändert werden.  
  
-   Das Dialogfeld **Richtlinien auswerten** zeigt nur Richtlinien an, die für das Datenbankobjekt geeignet sind.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-from-an-object"></a>So werten Sie eine Richtlinie für ein Objekt aus  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine Serverinstanz, eine Datenbank oder ein Datenbankobjekt, zeigen Sie auf **Richtlinien**, und wählen Sie dann **Auswerten**aus.  
  
2.  Wählen Sie im Dialogfeld **Richtlinien auswerten** eine oder mehrere Richtlinien aus, und klicken Sie auf **Auswerten** , um die Richtlinie im Auswertungsmodus auszuführen. Dadurch wird ein Kompatibilitätsbericht für den Zielsatz generiert. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird jedoch nicht neu konfiguriert, und es wird auch keine zukünftige Kompatibilität durchgesetzt. Für Ziele, die mit den ausgewählten Richtlinien nicht übereinstimmen und Eigenschaften besitzen, die von der richtlinienbasierten Verwaltung neu konfiguriert werden können, erzwingen Sie die Richtlinieneinhaltung, indem Sie auf **Anwenden**klicken. Weitere Informationen zu den Optionen im Dialogfeld **Richtlinien auswerten** finden Sie unter [Evaluate Policies Dialog Box, Policy Selection Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-policy-selection-page.md), [Evaluate Policies Dialog Box, Evaluation Results Page](../../relational-databases/policy-based-management/evaluate-policies-dialog-box-evaluation-results-page.md)und [Results Detailed View Dialog Box](../../relational-databases/policy-based-management/results-detailed-view-dialog-box.md).  
  
3.  Wenn Sie fertig sind, klicken Sie auf **Schließen**.  
  
  

