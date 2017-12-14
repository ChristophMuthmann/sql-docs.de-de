---
title: Verbindung mit Server herstellen (Oracle), Verbindungseigenschaften | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.oracleconnection.connectionprops.f1
helpviewer_keywords: Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 93059248f5787a812d22c30c915afe40a5ce2b86
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="connect-to-server-oracle-connection-properties"></a>Verbindung mit Server herstellen (Oracle), Verbindungseigenschaften
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe der Registerkarte **Verbindungseigenschaften** des Dialogfelds **Verbindung mit Server herstellen** können Sie eine Veröffentlichungsoption von **Gateway** oder **Vollständig** angeben. Nachdem ein Verleger identifiziert wurde, kann diese Option nicht mehr geändert werden, ohne dass der Verleger gelöscht und neu konfiguriert wird. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>enthalten  
 **Verlegertyp**  
 Wählen Sie **Gateway** oder **Vollständig**aus. Mithilfe der Option **Vollständig** kann für Momentaufnahme- und Transaktionsveröffentlichungen der vollständige Satz an unterstützten Funktionen für Oracle-Veröffentlichungen verfügbar gemacht werden. Die Option **Gateway** bietet spezielle Designoptimierungen, um die Leistung in Fällen zu verbessern, in denen die Replikation als Gateway zwischen Systemen verwendet wird. Sie können die Option **Gateway** nicht verwenden, wenn Sie planen, dieselbe Tabelle in mehreren Transaktionsveröffentlichungen zu veröffentlichen. Wenn Sie **Gateway**auswählen, kann eine Tabelle höchstens in einer Transaktionsveröffentlichung und in einer beliebigen Zahl an Momentaufnahmeveröffentlichungen erscheinen.  
  
 **Timeouts**  
 Geben Sie an, wie lange der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler versuchen soll, eine Verbindung mit dem Oracle-Verleger herzustellen, bevor ein Timeout-Fehler auftritt.  
  
## <a name="see-also"></a>Siehe auch  
 [Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Performance Tuning for Oracle Publishers](../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
