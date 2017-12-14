---
title: Initialisieren eines Abonnements mit einer Momentaufnahme | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf65d1d658c89a50d38c66a3c119a74b08eab28c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Initialisieren eines Abonnements mit einer Momentaufnahme
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Nachdem eine Veröffentlichung erstellt wurde, wird normalerweise eine Anfangsmomentaufnahme erstellt und in den Momentaufnahmeordner kopiert (dies erfolgt standardmäßig bei Mergeveröffentlichungen, die mit dem Assistenten für neue Veröffentlichung erstellt wurden). Die Momentaufnahme wird dann während der Erstsynchronisierung des Abonnements vom Verteilungs-Agent (für Transaktions- und Snapshotveröffentlichungen) oder vom Merge-Agent (für Mergeveröffentlichungen) auf den Abonnenten angewendet. Der Momentaufnahmeprozess hängt vom Veröffentlichungstyp ab:  
  
-   Handelt es sich um eine Momentaufnahme für eine Momentaufnahmeveröffentlichung, eine Transaktionsveröffentlichung oder eine Mergeveröffentlichung, die keine parametrisierte Filter verwendet, enthält die Momentaufnahme das Schema und die Daten in BCP-Dateien (Bulk Copy Program, Massenkopierprogramm) sowie Einschränkungen, erweiterte Eigenschaften, Indizes, Trigger und die für die Replikation erforderlichen Systemtabellen. Weitere Informationen zum Erstellen und Anwenden einer Momentaufnahme finden Sie unter [Erstellen und Anwenden der Momentaufnahme](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
-   Handelt es sich um eine Momentaufnahme für eine Mergeveröffentlichung, die parametrisierte Filter verwendet, wird die Momentaufnahme mit einem zweiteiligen Prozess erstellt. Zuerst wird eine Schemamomentaufnahme erstellt, die die Replikationsskripts und das Schema der veröffentlichten Objekte enthält, nicht jedoch die Daten. Jedes Abonnement wird dann mit einer Momentaufnahme initialisiert, die die aus der Schemamomentaufnahme kopierten Skripts und das Schema sowie die Daten enthält, die zur Partition des Abonnements gehören. Weitere Informationen finden Sie unter [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 Die Momentaufnahme besteht aus verschiedenen Dateien, die vom Replikationstyp und den Artikeln in der Veröffentlichung abhängen. Diese Dateien werden in den Standardmomentaufnahmeordner kopiert, der beim Konfigurieren des Verteilers angegeben wurde, oder in den beim Erstellen der Veröffentlichung angegeben alternativen Momentaufnahmeordner.  
  
|Replikationstyp|Gemeinsame Momentaufnahmedateien|  
|-------------------------|---------------------------|  
|Momentaufnahmereplikation oder Transaktionsreplikation|Schema (SCH); Daten (BCP); Einschränkungen und Indizes (DRI); Einschränkungen (IDX); Trigger (TRG): nur für Updateabonnenten; komprimierte Momentaufnahmedateien (CAP).|  
|Mergereplikation|Schema (SCH); Daten (BCP); Einschränkungen und Indizes (DRI); Trigger (TRG); Systemtabellendaten (SYS); Konflikttabellen (CFT); komprimierte Momentaufnahmedateien (CAP).|  
  
 Falls das Übertragen der Momentaufnahme an einer Stelle unterbrochen wird, wird es anschließend automatisch fortgesetzt. Bereits vollständig übertragene Dateien werden nicht noch einmal gesendet. Teilweise übermittelte Dateien müssen vollständig neu übermittelt werden, da beim Momentaufnahme-Agent die BCP-Datei für jeden Veröffentlichungsartikel zur Übermittlung verwendet wird. Das Fortsetzen der Momentaufnahmeübertragung kann jedoch die Menge der übermittelten Daten erheblich reduzieren und eine rechtzeitige Übermittlung der Momentaufnahme auch bei einer unzuverlässigen Verbindung sicherstellen.  
  
## <a name="snapshot-options"></a>Momentaufnahmeoptionen  
 Zum Initialisieren eines Abonnements mit einer Momentaufnahme stehen verschiedene Optionen zur Verfügung. Folgende Aktionen sind möglich:  
  
-   Geben Sie anstelle des oder zusätzlich zum Speicherort des Standardmomentaufnahmeordners einen alternativen Speicherort für den Momentaufnahmeordner an. Weitere Informationen finden Sie unter [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md).  
  
-   Komprimieren Sie Momentaufnahmen zum Speichern auf Wechselmedien oder zum Übertragen in einem langsamen Netzwerk. Weitere Informationen finden Sie unter [Compressed Snapshots](../../relational-databases/replication/compressed-snapshots.md).  
  
-   Führen Sie vor oder nach dem Anwenden der Momentaufnahme Transact-SQL-Skripts aus. Weitere Informationen finden Sie unter [Ausführen von Skripts vor und nach dem Anwenden der Momentaufnahme](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md).  
  
-   Übertragen Sie Momentaufnahmedateien über FTP (File Transfer Protocol). Weitere Informationen finden Sie unter [Übertragen von Momentaufnahmen über FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md)   
 [Sichern des Momentaufnahmeordners](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
