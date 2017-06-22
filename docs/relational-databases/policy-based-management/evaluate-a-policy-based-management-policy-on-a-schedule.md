---
title: Auswerten einer Richtlinie der richtlinienbasierten Verwaltung nach einem Zeitplan | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8bd8881f2c7ed11141091e117cefa037818f7ea
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Auswerten einer Richtlinie der richtlinienbasierten Verwaltung nach einem Zeitplan
  In diesem Thema wird beschrieben, wie Sie eine Richtlinie der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nach einem Zeitplan in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]auswerten.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Auswerten einer Richtlinie nach einem Zeitplan mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>So werten Sie eine Richtlinie nach einem Zeitplan aus  
  
1.  Klicken Sie im **Objekt-Explorer**auf das Pluszeichen, um den Server zu erweitern, in dem der auszuwertende Richtlinienzeitplan enthalten ist.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Richtlinien** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Richtlinie, deren Zeitplan Sie auswerten möchten, und wählen Sie **Eigenschaften**aus.  
  
6.  Wählen Sie im Dialogfeld **Richtlinie öffnen –***Richtlinienname* in der Liste **Auswertungsmodus** die Option **Nach Zeitplan**aus.  
  
7.  Klicken Sie unter **Zeitplan**auf **Auswählen** , um einen vorhandenen Zeitplan anzugeben, oder klicken Sie auf **Neu** , um einen neuen Zeitplan zu erstellen.  
  
8.  Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
  
