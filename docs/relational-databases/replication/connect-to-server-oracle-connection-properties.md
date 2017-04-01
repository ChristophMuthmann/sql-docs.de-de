---
title: "Verbindung mit Server herstellen (Oracle), Verbindungseigenschaften | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.oracleconnection.connectionprops.f1"
helpviewer_keywords: 
  - "Dialogfeld "Verbindung mit Server herstellen", Replikation"
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# Verbindung mit Server herstellen (Oracle), Verbindungseigenschaften
  Mithilfe der Registerkarte **Verbindungseigenschaften** des Dialogfelds **Verbindung mit Server herstellen** können Sie eine Veröffentlichungsoption von **Gateway** oder **Vollständig**angeben. Nachdem ein Verleger identifiziert wurde, kann diese Option nicht mehr geändert werden, ohne dass der Verleger gelöscht und neu konfiguriert wird. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Optionen  
 **Verlegertyp**  
 Wählen Sie **Gateway** oder **vollständige**. Mithilfe der Option **Vollständig** kann für Momentaufnahme- und Transaktionsveröffentlichungen der vollständige Satz an unterstützten Funktionen für Oracle-Veröffentlichungen verfügbar gemacht werden. Die Option **Gateway** bietet spezielle Designoptimierungen, um die Leistung in Fällen zu verbessern, in denen die Replikation als Gateway zwischen Systemen verwendet wird. Sie können die Option **Gateway** nicht verwenden, wenn Sie planen, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Wenn Sie **Gateway**auswählen, kann eine Tabelle höchstens in einer Transaktionsveröffentlichung und in einer beliebigen Zahl an Momentaufnahmeveröffentlichungen erscheinen.  
  
 **Timeouts**  
 Geben Sie wie lange der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler versuchen soll, mit dem Oracle-Verleger herzustellen, bevor ein Timeoutfehler auftritt.  
  
## Siehe auch  
 [Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Leistungsoptimierung für Oracle-Verleger](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  