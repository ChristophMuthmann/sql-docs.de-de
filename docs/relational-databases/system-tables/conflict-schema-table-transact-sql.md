---
title: Conflict_&lt;Schema&gt;_&lt;Tabelle&gt; (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 01/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- conflict_
- conflict_TSQL
dev_langs: TSQL
helpviewer_keywords: conflict_<schema>_<table>
ms.assetid: 15ddd536-db03-454e-b9b5-36efe1f756d7
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfb2f078495256ee53d021bb09801323bdca094f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="conflictltschemagtlttablegt-transact-sql"></a>Conflict_&lt;Schema&gt;_&lt;Tabelle&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Die Conflict_\<Schema > _\<Tabelle > Tabelle enthält Informationen über in Konflikt stehende Zeilen in der Peer-zu-Peer-Replikation. Eine Konflikttabelle besteht für jede replizierte Tabelle in einer Veröffentlichung, wobei der Name der Konflikttabelle mit dem Schema- und Artikelnamen angefügt wird. Diese artikelspezifischen Konflikttabellen sind in jeder Veröffentlichungsdatenbank vorhanden.  
  
 Bei der Peer-zu-Peer-Replikation schlägt der Verteilungs-Agent standardmäßig fehl, wenn er einen Konflikt erkennt. Im Fehlerprotokoll wird ein Konfliktfehler protokolliert, jedoch werden in der Konflikttabelle keine Konfliktdaten erfasst; daher können sie nicht angezeigt werden. Wenn der Verteilungs-Agent fortfahren kann, wird der Konflikt lokal auf jedem Knoten protokolliert, auf dem er erkannt wurde. Weitere Informationen finden Sie im Abschnitt "Konfliktbehandlung" unter [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|__$originator_id|**int**|ID des Knotens, aus dem die konfliktverursachende Änderung stammt. Führen Sie eine Liste von IDs, [Sp_help_peerconflictdetection](../../relational-databases/system-stored-procedures/sp-help-peerconflictdetection-transact-sql.md).|  
|__$origin_datasource|**int**|Knoten, aus dem die konfliktverursachende Änderung stammt.|  
|__$tranid|**Nvarchar (40)**|Protokollsequenznummer (LSN) der den Konflikt verursachenden Änderung bei der Anwendung auf __$origin_datasource.|  
|__$conflict_type|**int**|Typ des Konflikts. Die folgenden Werte sind möglich:<br /><br /> 1: Ein Update ist fehlgeschlagen, da die lokale Zeile durch ein anderes Update geändert wurde oder gelöscht und dann erneut eingefügt wurde.<br /><br /> 2: Ein Update ist fehlgeschlagen, da die lokale Zeile bereits gelöscht wurde.<br /><br /> 3: Ein Löschvorgang ist fehlgeschlagen, da die lokale Zeile durch ein anderes Update geändert wurde oder gelöscht und dann erneut eingefügt wurde.<br /><br /> 4: Ein Löschvorgang ist fehlgeschlagen, da die lokale Zeile bereits gelöscht wurde.<br /><br /> 5: Ein Einfügevorgang ist fehlgeschlagen, da die lokale Zeile bereits eingefügt wurde oder eingefügt und anschließend aktualisiert wurde.|  
|__$is_winner|**bit**|Gibt an, ob die Zeile in dieser Tabelle der Konfliktgewinner war. Das bedeutet, dass sie auf den lokalen Knoten angewendet wurde.|  
|__$pre_version|**Varbinary (32)**|Version der Datenbank, aus der die konfliktverursachende Änderung stammt.|  
|__$reason_code|**int**|Auflösungscode für den Konflikt. Folgende Werte sind möglich:<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> <br /><br /> Weitere Informationen finden Sie unter **__ $Reason_text**.|  
|__$reason_text|**Nvarchar (720)**|Auflösung für den Konflikt. Folgende Werte sind möglich:<br /><br /> Aufgelöst (1)<br /><br /> Nicht aufgelöst (2)<br /><br /> Unbekannt (0)|  
|__$update_bitmap|**Varbinary (**  *n*  **)**. Größe variiert je nach Inhalt.|Bitmap, die angibt, welche Spalten im Fall eines UPDATE/UPDATE-Konflikts aktualisiert wurden.|  
|__$inserted_date|**datetime**|Datum und Uhrzeit, zu der die Konfliktzeile in diese Tabelle eingefügt wurde.|  
|__$row_id|**timestamp**|Zeilenversion, die mit der Zeile verknüpft ist, die den Konflikt verursacht hat.|  
|__$change_id|**Binär (8)**|Für eine lokale Zeile entspricht dieser Wert der __$row_id der eingehenden Zeile, die in Konflikt mit der lokalen Zeile steht. Dieser Wert ist NULL für eine eingehende Zeile.|  
|\<basistabellenspaltennamen >|\<Tabelle Spalte Basistypen >|Die Konflikttabelle enthält eine Spalte für jede Spalte in der Basistabelle.|  
  
## <a name="see-also"></a>Siehe auch  
 [Replikationstabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replikationssichten &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
