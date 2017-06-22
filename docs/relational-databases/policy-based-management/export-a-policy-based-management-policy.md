---
title: Exportieren einer Richtlinie der richtlinienbasierten Verwaltung | Microsoft-Dokumentation
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
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c409fd3fc46ce2612290737bf658dd4358280495
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="export-a-policy-based-management-policy"></a>Exportieren einer Richtlinie der richtlinienbasierten Verwaltung
  In diesem Thema wird beschrieben, wie Sie eine Richtlinie der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]exportieren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Sicherheit](#Security)  
  
-   **Exportieren einer Richtlinie mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
  
#### <a name="to-export-a-policy"></a>So exportieren Sie eine Richtlinie  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um den Server zu erweitern, in dem die zu exportierende Richtlinie der richtlinienbasierten Verwaltung enthalten ist.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Richtlinien** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf die zu exportierende Richtlinie, und wählen Sie **Richtlinie exportieren**aus.  
  
6.  Geben Sie im Dialogfeld **Richtlinie exportieren** den Pfad und den Namen der Datei in der Adressleiste ein. Suchen Sie alternativ im Navigationsbereich des Dialogfelds einen geeigneten Speicherort für die Datei, und geben Sie den Namen der XML-Datei in das Feld **Dateiname** ein.  
  
7.  Wenn Sie fertig sind, klicken Sie auf **Speichern**.  
  
  
