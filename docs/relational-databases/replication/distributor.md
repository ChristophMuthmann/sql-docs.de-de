---
title: "Verteiler | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replicationutilities.selectdistributor.f1"
ms.assetid: 787f0e9c-09dd-438a-bc04-5b8f99c127b8
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Verteiler
  Die Seite **Verteiler** wird im Verteilungskonfigurations-Assistenten und im Assistenten für neue Veröffentlichung angezeigt. Beim Verteiler handelt es sich um einen Server, der die Verteilungsdatenbank beinhaltet und auf dem die Metadaten und Verlaufsdaten für alle Replikationstypen gespeichert werden. Darüber hinaus werden auf dem Verteiler Transaktionen für die Transaktionsreplikation gespeichert. Beim Verteiler kann es sich um denselben Server, der als Verleger (lokaler Verteiler) verwendet wird, oder um einen anderen Server als den Verleger (Remoteverteiler) handeln. Die Rolle des Verteilers variiert je nach implementiertem Replikationstyp. Im Allgemeinen spielt er bei der Transaktionsreplikation eine größere Rolle als bei der Merge- oder Momentaufnahmereplikation. Bei der Merge- und Momentaufnahmereplikation wird normalerweise ein lokaler Verteiler verwendet, allerdings kann sich die Verwendung eines Remoteverteilers bei ausgelasteten Systemen positiv auf die Transaktionsreplikation auswirken.  
  
 Der Verteiler verwendet die folgenden zusätzlichen Ressourcen auf dem Server, auf dem er sich befindet:  
  
-   Zusätzlichen Speicherplatz, falls die Momentaufnahmedateien für die Veröffentlichung darin gespeichert werden (was normalerweise der Fall ist).  
  
-   Zusätzlichen Speicherplatz zum Speichern der Verteilungsdatenbank.  
  
-   Zusätzliche Prozessornutzung durch Replikations-Agents für auf dem Verteiler ausgeführte Pushabonnements.  
  
 Der Server, den Sie als Verteiler auswählen, sollte ausreichend Speicherplatz und Prozessorleistung für die Replikation und sonstige Aktivitäten, die auf diesem Server basieren, aufweisen.  
  
## Optionen  
 **' \< ServerName>"fungiert als sein eigener Verteiler; SQL Server erstellt eine Verteilungsdatenbank und ein Protokoll**  
 Wählen Sie diese Option aus, um den Server zu konfigurieren, mit dem Sie als Verteiler verbunden sind.  
  
 **Folgenden Server als Verteiler verwenden (Hinweis: Der ausgewählte Server muss bereits als Verteiler konfiguriert sein)**  
 Wählen Sie diese Option aus, und klicken Sie anschließend unten auf den Namen eines Servers, um einen anderen Server als Verteiler zu konfigurieren.  
  
 **Hinzufügen**  
 Wenn der Server zu verwenden, wie ein Verteiler nicht aufgeführt ist, klicken Sie auf **Hinzufügen** können Sie den Server zu identifizieren und zur Liste hinzufügen.  
  
> [!NOTE]  
>  Um einen Remoteserver als Verteiler zu verwenden, muss der Remoteserver bereits als Verteiler konfiguriert sein. Der Server, für den der Assistent ausgeführt wird, muss auf diesem Verteiler als Verleger aktiviert sein.  
  
## Siehe auch  
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  