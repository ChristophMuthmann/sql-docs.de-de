---
title: SQL Server, Transaktionen-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Transactions
- Transactions object
ms.assetid: 85240267-78fd-476a-9ef6-010d6cf32dd8
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 757b2b72fe2066f452e53087e2ae73ea67d45aa8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-transactions-object"></a>SQL Server, Transaktionen-Objekt
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Das **Transaktionen**-Objekt in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Leistungsindikatoren zum Überwachen der Anzahl aktiver Transaktionen in einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] und der Auswirkungen solcher Transaktionen auf Ressourcen wie dem Momentaufnahmeisolations-Zeilenversionsspeicher in **tempdb**. Transaktionen sind logische Arbeitseinheiten - eine Reihe von Vorgängen, die entweder alle erfolgreich ausgeführt oder aber komplett aus einer Datenbank gelöscht werden müssen, damit die logische Integrität der Daten beibehalten werden kann. Jede Veränderung an Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbanken wird in Transaktionen vorgenommen.  
  
 Wenn für eine Datenbank die Möglichkeit der Momentaufnahmeisolationsstufe gegeben ist, muss von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Datensatz der Änderungen beibehalten werden, die an jeder Zeile in einer Datenbank vorgenommen wurden. Bei jeder Änderung an einer Zeile wird eine Kopie der Zeile im Zustand vor der Änderung in einem Zeilenversionsspeicher in **tempdb**aufgezeichnet. Viele der Leistungsindikatoren im **Transaction** -Objekt können zum Überwachen der Größe und Wachstumsrate des Zeilenversionsspeichers in **tempdb**verwendet werden.  
  
 Von den **Transaktionen** -Objektleistungsindikatoren werden alle Transaktionen in einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]ausgegeben.  
  
 In dieser Tabelle werden die **SQLServer:Transaktionen** -Leistungsindikatoren beschrieben.  
  
|Transaktionsleistungsindikatoren von SQL Server|Description|  
|--------------------------------------|-----------------|  
|**Freier Speicherplatz in tempdb (KB)**|Der verfügbare Speicherplatz (in Kilobytes) in **tempdb**. Es muss ausreichend Speicherplatz zur Aufnahme des Momentaufnahmeisolationsstufen-Versionsspeichers und aller neuer temporärer Objekte vorhanden sein, die in der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]erstellt worden sind.|  
|**Längste Transaktionsausführungszeit**|Die verstrichene Zeit (in Sekunden) seit dem Start der Transaktion, die länger aktiv war als alle anderen aktuellen Transaktionen. Dieser Leistungsindikator zeigt nur Aktivität an, wenn die Datenbank unter der READ_COMMITTED_SNAPSHOT-Isolationsstufe ausgeführt wird. Es werden keine Aktivitäten protokolliert, wenn die Datenbank eine andere Isolationsstufe aufweist.|  
|**NonSnapshot-Versionstransaktionen**|Die Anzahl der aktuell aktiven Transaktionen, die keine Momentaufnahmeisolationsstufe verwenden und von denen keine Änderungen ausgeführt worden sind, die Zeilenversionen im **tempdb** -Versionsspeicher generiert haben.|  
|**Momentaufnahmetransaktionen**|Die Anzahl aktuell aktiver Transaktionen, die die Momentaufnahmeisolationsstufe verwenden.<br /><br /> Hinweis: Der **Momentaufnahmetransaktionen** -Objektleistungsindikator reagiert, wenn der erste Datenzugriff auftritt, nicht wenn die `BEGIN TRANSACTION` -Anweisung ausgegeben wird.|  
|**Transaktionen**|Die Anzahl aktuell aktiver Transaktionen aller Typen.|  
|**Updatekonfliktquote**|Der Prozentsatz derjenigen Transaktionen, die die Momentaufnahmeisolationsstufe verwenden und bei denen innerhalb der letzten Sekunde Updatekonflikte aufgetreten sind. Ein Updatekonflikt tritt auf, wenn von einer Momentaufnahmeisolationsstufen-Transaktion der Versuch unternommen wird, eine Zeile zu ändern, die zuletzt von einer anderen Transaktion geändert wurde, für die kein Commit ausgeführt worden ist, als die Momentaufnahmeisolationsstufen-Transaktion gestartet wurde.|  
|**Basis der Updatekonfliktquote**|Nur zur internen Verwendung.|
|**Update-Momentaufnahmetransaktionen**|Die Anzahl aktuell aktiver Transaktionen, von denen die Momentaufnahmeisolationsstufe verwendet wird und Daten geändert wurden.|  
|**Versionscleanuprate (KB/s)**|Die Rate (in Kilobytes pro Sekunde), mit der Zeilenversionen aus dem Versionsspeicher für Momentaufnahmeisolationen in **tempdb**entfernt werden.|  
|**Versionsgenerierungsrate (KB/s)**|Die Rate (in Kilobytes pro Sekunde), mit der neue Zeilenversionen zum Versionsspeicher für Momentaufnahmeisolationen in **tempdb**hinzugefügt werden.|  
|**Versionsspeichergröße (KB)**|Der Speicherplatz (in Kilobytes) in **tempdb** , der für die Speicherung von Zeilenversionen für Momentaufnahmeisolationsstufen verwendet wird.|  
|**Anzahl der Versionsspeichereinheiten**|Die Anzahl aktiver Zuordnungseinheiten im Momentaufnahmeisolations-Versionsspeicher in **tempdb**.|  
|**Erstellung von Versionsspeichereinheiten**|Die Anzahl der Zuordnungseinheiten, die seit dem Start der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] im Momentaufnahmeisolationsspeicher erstellt worden sind.|  
|**Abschneiden von Versionsspeichereinheiten**|Die Anzahl der Zuordnungseinheiten, die seit dem Start der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] aus dem Momentaufnahmeisolationsspeicher entfernt worden sind.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
