---
title: Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung (SQL Server-Hilfsprogramm) | Microsoft-Dokumentation
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
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18d7c0d9db15cdbcfa8adf02de6b4febaa99c5bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>Reduzieren von Informationsrauschen bei Richtlinien zur CPU-Auslastung (SQL Server-Hilfsprogramm)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Verwenden Sie die folgenden Strategien, um Berichte mit geringem Informationsgehalt und unerwünschte Verstöße in den Ressourcennutzungsrichtlinien des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Hilfsprogramms einzudämmen.  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>Wie viele Verstöße in Bezug auf die Prozessorauslastung können auftreten, bevor eine Überauslastung gemeldet wird?  
 Der Auswertungszeitraum und die prozentuale Toleranz für Verstöße können beide über die Einstellungen auf der Registerkarte **Richtlinie** unter dem Knoten **Hilfsprogrammverwaltung** des Hilfsprogramm-Explorers konfiguriert werden. Zum Ändern von Richtlinien verwenden Sie die Schieberegler-Steuerelemente rechts neben den Richtlinienbeschreibungen und klicken dann auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Das Datensammlungsintervall beträgt 15 Minuten. Dieser Wert ist nicht konfigurierbar.  
  
-   Der obere Standardschwellenwert für die Richtlinie zur Prozessorauslastung beträgt 70 %. Es können Werte zwischen 0 % und 100 % ausgewählt werden.  
  
-   Der Standardauswertungszeitraum für die Überauslastung des Prozessors beträgt eine Stunde. Es können Werte zwischen einer Stunde und einer Woche ausgewählt werden.  
  
-   Der Standardprozentsatz kritischer Datenpunkte, die aufkommen dürfen, bevor die CPU als überausgelastet gemeldet wird, liegt bei 20 %. Es können Werte zwischen 0 % und 100 % ausgewählt werden.  
  
 Gemäß den Standardwerten werden pro Stunde z. B. vier Datenpunkte gesammelt, und der Richtlinienschwellenwert liegt bei 20 %. Deshalb wird jeder Verstoß innerhalb des einstündigen Sammlungszeitraums standardmäßig mit 25 % von vier Datenpunkten angerechnet. Gemäß den Standardwerten wird jeder Verstoß gegen den Richtlinienschwellenwert für die CPU-Überauslastung gemeldet.  
  
 Sie haben folgende Möglichkeiten, um das durch einen einzelnen Verstoß verursachte Informationsrauschen zu reduzieren:  
  
-   Verlängern Sie den Auswertungszeitraum um einen Schrittwert auf sechs Stunden. Ein einzelner Verstoß innerhalb von sechs Stunden würde einem Datenpunkt in einer Stichprobengröße von 24 entsprechen. In diesem Fall würde die Richtlinie in sechs Stunden vier Verstöße gegen den Richtlinienschwellenwert tolerieren (16,7 % der Datenpunkte), es werden jedoch mindestens fünf Verstöße in Bezug auf Überauslastung (>20 % der Datenpunkte) in einem sechsstündigen Sammlungszeitraum gemeldet.  
  
-   Erhöhen Sie die prozentuale Toleranz für Verstöße um einen Schrittwert auf 30 %. Ein einzelner Verstoß innerhalb einer Stunde würde einem Datenpunkt in einer Stichprobengröße von 4 entsprechen. In diesem Fall würde die Richtlinie eine Verletzung pro Stunde tolerieren, es würden jedoch mindestens zwei Verstöße in Bezug auf Überauslastung (>30 % der Datenpunkte) in einem einstündigen Sammlungszeitraum gemeldet.  
  
-   Erhöhen Sie die Richtlinienschwellenwerte für die Prozessorauslastung verwalteter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen und Datenebenenanwendungen. Weitere Informationen zum Ändern der globalen Richtlinien zur CPU-Auslastung für verwaltete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen oder Datenebenenanwendungen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Weitere Informationen zum Ändern von Richtlinien zur CPU-Auslastung für einzelne Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2). Weitere Informationen zum Ändern von Richtlinien zur CPU-Auslastung für einzelne Datenebenenanwendungen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>Wie viele Verstöße in Bezug auf die Prozessorauslastung können auftreten, bevor eine Unterauslastung gemeldet wird?  
 Der Auswertungszeitraum und die prozentuale Toleranz für Verstöße können beide über die Einstellungen auf der Registerkarte **Richtlinie** unter dem Knoten **Hilfsprogrammverwaltung** des Hilfsprogramm-Explorers konfiguriert werden. Zum Ändern von Richtlinien verwenden Sie die Schieberegler-Steuerelemente rechts neben den Richtlinienbeschreibungen und klicken dann auf **Anwenden**. Mithilfe der Schaltflächen unten in der Anzeige können Sie auch Standardwerte wiederherstellen oder Änderungen verwerfen.  
  
-   Das Datensammlungsintervall beträgt 15 Minuten. Dieser Wert ist nicht konfigurierbar.  
  
-   Der untere Standardschwellenwert für die Richtlinie zur Prozessorauslastung beträgt 0 %. Es können Werte zwischen 0 % und 100 % ausgewählt werden.  
  
-   Der Standardauswertungszeitraum für die Unterauslastung des Prozessors beträgt eine Woche. Es können Werte zwischen einem Tag und einem Monat ausgewählt werden.  
  
-   Der Standardprozentsatz kritischer Datenpunkte, die aufkommen dürfen, bevor die CPU als unterausgelastet gemeldet wird, liegt bei 90 %. Es können Werte zwischen 0 % und 100 % ausgewählt werden.  
  
 Gemäß den Standardwerten werden pro Woche 672 Datenpunkte gesammelt, der Richtlinienschwellenwert liegt jedoch bei 0 %. Diese Richtlinie generiert standardmäßig also keine Verstöße in Bezug auf die Unterauslastung des Prozessors. Weitere Informationen zum Ändern der globalen Richtlinien zur CPU-Auslastung für verwaltete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen oder Datenebenenanwendungen finden Sie unter [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Weitere Informationen zum Ändern von Richtlinien zur CPU-Auslastung für einzelne Instanzen von SQL Server finden Sie unter [Details zu verwalteten Instanzen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2). Weitere Informationen zum Ändern von Richtlinien zur CPU-Auslastung für einzelne Datenebenenanwendungen finden Sie unter [Details zu bereitgestellten Datenebenenanwendungen &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Hilfsprogrammverwaltung &#40;SQL Server-Hilfsprogramm&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d)   
 [Überwachen von SQL Server-Instanzen im SQL Server-Hilfsprogramm](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Ändern der Definition von Ressourcenintegritätsrichtlinien &#40;SQL Server-Hilfsprogramm&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [Funktionen und Tasks im SQL Server-Hilfsprogramm](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
