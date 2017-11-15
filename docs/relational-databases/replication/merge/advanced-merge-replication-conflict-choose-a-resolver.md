---
title: "Wählen eines Konfliktlösers | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default conflict resolver
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: b7dec3fa-d9d9-409d-b946-f9b9a3202829
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cba1ee9c5659d84f4fbe5a1c6ac5957794df0a88
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-merge-replication-conflict---choose-a-resolver"></a>Wählen eines Konfliktlösers – Wählen Sie einen Konfliktlöser aus
  Beim Auswählen eines Konfliktlösers sollten Sie die Bedeutung der Konfliktlösung in Ihrer Anwendung und die Frage berücksichtigen, ob der standardmäßige prioritätsbasierte Konfliktlöser verwendet werden kann oder ob ein Artikelkonfliktlöser verwendet werden muss.  
  
 Wenn die Daten partitioniert werden, ohne dass mehrere Benutzer in dieselben Partitionen schreiben, und die Replikationstopologie relativ einfach ist (ein Verleger und wenige Abonnenten) sollten Konflikte selten oder nie vorkommen. In diesen Umgebungen ist eine komplexe Konfliktauflösungsstrategie eher nicht notwendig. Es wird eine Strategie empfohlen, die die Standardeinstellungen für die Konfliktlösung, Clientabonnements und eine Richtlinie verwendet, bei der die erste Änderung gewinnt. Wenn die Topologie komplexer ist (z. B. weil Wiederveröffentlichungsabonnenten verwendet werden), sind Serverabonnements mit spezifischen Prioritäten möglicherweise geeigneter.  
  
 Die Verwendung eines Artikelkonfliktlösers wird empfohlen, wenn die Anforderungen in Ihrem Unternehmen eine genauer abgestimmte Lösung als die mit dem Standardkonfliktlöser verfügbare Lösung nötig machen. Wenn Sie sich für die Verwendung eines Artikelkonfliktlösers entscheiden, empfiehlt sich die Verwendung eines Geschäftslogikhandlers. Weitere Informationen finden Sie unter [Ausführen von Geschäftslogik während der Mergesynchronisierung](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 Letztendlich sollte sich die Entscheidung, ob der Standardkonfliktlöser oder ein Artikelkonfliktlöser verwendet wird, nach den Daten und den Geschäftslogikanforderungen der Anwendung richten. Nehmen wir z. B. eine Firma, in der Mitarbeiter in eine Gruppe von nicht partitionierten Tabellen auf unterschiedlichen Abonnenten Kundeneinstufungsdaten eingeben. Die Mitarbeiter gehören unterschiedlichen Funktionskategorien (Filialleiter, Abteilungsleiter, Vertriebsmitarbeiter) an. Für die Entscheidung, welche Daten Priorität erhalten, soll die jeweilige Funktionskategorie herangezogen werden. In diesem Fall kann ein Artikelkonfliktlöser erstellt werden, der beim Auftreten eines Konflikts anhand der Funktionskategorie aus dem Artikel den Prioritätsgewinner bestimmt.  
  
 Wenn die Wahrscheinlichkeit von häufigen Konflikten relativ hoch ist, sollten Sie bei der Implementierung einer Konfliktauflösungsstrategie u. a. die folgenden Punkte berücksichtigen:  
  
|Konfliktlösungsproblem|Empfehlung|  
|-------------------------------|--------------------|  
|Verschiedene Kategorien von Benutzern erfordern verschiedene Prioritätswerte.|Verwenden Sie den Standardkonfliktlöser, und erstellen Sie Serverabonnements mit unterschiedlichen Prioritätswerten.<br /><br /> oder<br /><br /> Verwenden Sie einen Artikelkonfliktlöser, der eine Spalte mit Autoritätswerten im Artikel erkennt und damit die Konfliktlösung vereinfacht.|  
|Lösung wird gewünscht, bei der die erste Änderung den Konflikt gewinnt.|Verwenden Sie den Standardkonfliktlöser, und erstellen Sie Clientabonnements.|  
|Mehrere Benutzer, die dieselbe Datenzeile ändern, sollen zulässig sein, sofern keine konfliktverursachenden Änderungen an derselben Spalte vorgenommen werden.|Verwenden Sie entweder den Standardkonfliktlöser oder einen Artikelkonfliktlöser mit aktivierter Nachverfolgung auf Spaltenebene.|  
|Mehrere Änderungen an einem Wert in einer Zeile sollen als Konflikt markiert werden.|Verwenden Sie entweder den Standardkonfliktlöser oder einen Artikelkonfliktlöser mit Nachverfolgung auf Zeilenebene.|  
|Mehrere Änderungen an einem Wert in einem logischen Datensatz sollen als Konflikt markiert werden.|Verwenden Sie den Standardkonfliktlöser mit Nachverfolgung auf der Ebene des logischen Datensatzes (bei Verwendung logischer Datensätze werden weder benutzerdefinierte Konfliktlöser noch Geschäftslogikhandler unterstützt).|  
|Die resultierenden Konfliktdaten müssen sich von den ursprünglichen Konfliktdaten unterscheiden.|Verwenden Sie einen Artikelkonfliktlöser, der neue Werte berechnet.|  
  
## <a name="see-also"></a>Siehe auch  
 [Ermitteln und Lösen von Konflikten in logischen Datensätzen](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Erweiterte Konflikterkennung und -lösung bei der Mergereplikation](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Erneutes Veröffentlichen von Daten](../../../relational-databases/replication/republish-data.md)  
  
  
