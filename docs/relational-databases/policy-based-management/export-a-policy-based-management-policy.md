---
title: Exportieren einer Richtlinie der richtlinienbasierten Verwaltung | Microsoft-Dokumentation
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
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58e4a509dbb48aef071a6b5904490a09318e9de2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="export-a-policy-based-management-policy"></a>Exportieren einer Richtlinie der richtlinienbasierten Verwaltung
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie eine Richtlinie der richtlinienbasierten Verwaltung mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]exportieren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **Exportieren einer Richtlinie mit:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die Mitgliedschaft in der PolicyAdministratorRole-Rolle in der msdb-Datenbank.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-export-a-policy"></a>So exportieren Sie eine Richtlinie  
  
1.  Klicken Sie im Objekt-Explorer auf das Pluszeichen, um den Server zu erweitern, in dem die zu exportierende Richtlinie der richtlinienbasierten Verwaltung enthalten ist.  
  
2.  Klicken Sie auf das Pluszeichen, um den Ordner **Verwaltung** zu erweitern.  
  
3.  Klicken Sie auf das Pluszeichen, um **Richtlinienverwaltung**zu erweitern.  
  
4.  Klicken Sie auf das Pluszeichen, um den Ordner **Richtlinien** zu erweitern.  
  
5.  Klicken Sie mit der rechten Maustaste auf die zu exportierende Richtlinie, und wählen Sie **Richtlinie exportieren**aus.  
  
6.  Geben Sie im Dialogfeld **Richtlinie exportieren** den Pfad und den Namen der Datei in der Adressleiste ein. Suchen Sie alternativ im Navigationsbereich des Dialogfelds einen geeigneten Speicherort für die Datei, und geben Sie den Namen der XML-Datei in das Feld **Dateiname** ein.  
  
7.  Wenn Sie fertig sind, klicken Sie auf **Speichern**.  
  
  
