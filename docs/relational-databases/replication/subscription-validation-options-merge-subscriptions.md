---
title: "Optionen für die Abonnementüberprüfung (Mergeabonnements) | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.validate.mergeoptions.f1
helpviewer_keywords: Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b073c50763e64d4fe8bb602f1be90ccc31e1d78d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="subscription-validation-options-merge-subscriptions"></a>Optionen für die Abonnementüberprüfung (Mergeabonnements)
  Mithilfe des Dialogfelds **Optionen für die Abonnementüberprüfung** können Sie angeben, ob zur Überprüfung nur die Zeilenanzahl oder die Zeilenanzahl und eine binäre Prüfsumme verwendet werden soll.  
  
## <a name="options"></a>Optionen  
 **Nur Zeilenanzahl überprüfen**  
 Wählen Sie diese Option aus, um zu überprüfen, ob die Anzahl der Zeilen in der Tabelle auf dem Abonnenten mit der Anzahl der Zeilen in der Tabelle auf dem Verleger übereinstimmt. Mit dieser Methode wird nicht überprüft, ob die Inhalte der Zeilen übereinstimmen. Die Überprüfung der Zeilenanzahl bietet einen Überprüfungsansatz, der kaum Ressourcen beansprucht und Sie Probleme bei den Daten erkennen lässt.  
  
 **Die Zeilenanzahl überprüfen und Prüfsummen vergleichen, um die Zeilendaten zu überprüfen**  
 Zusätzlich zum Einbinden einer Reihe von Zeilen auf Verleger- und Abonnentenebene wird eine Prüfsumme aller Daten mit dem binären Prüfsummenalgorithmus berechnet. Ist die Zeilenanzahl fehlerhaft, wird die Berechnung der Prüfsumme nicht ausgeführt. Diese Option gilt nicht für [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Überprüfen der Daten am Abonnenten](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md)  
  
  
