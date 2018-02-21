---
title: Behandeln von Problemen mit der Volltextindizierung | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ddb9ea039218fa967132572df461103957300161
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="troubleshoot-full-text-indexing"></a>Behandeln von Problemen mit der Volltextindizierung
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
     
##  <a name="failure"></a> Beheben von Fehlern bei der Volltextindizierung  
 Beim Auffüllen oder Verwalten eines Volltextindexes werden vom Volltextindexer aus den unten beschriebenen Gründen möglicherweise eine oder mehrere Zeilen nicht indiziert. Diese Fehler auf Zeilenebene verhindern nicht, dass die Auffüllung beendet wird. Diese Zeilen werden vom Indexer ausgelassen, was bedeutet, dass Sie anschließend keine in diesen Zeilen enthaltenen Inhalte abfragen können.  
  
 Indizierungsfehler können in folgenden Fällen auftreten:  
  
-   Vom Indexer kann eine Filter- oder Wörtertrennungskomponente nicht gefunden oder geladen werden. Dieser Fehler kann auftreten, wenn die Tabellenzeile ein Dokumentformat oder Inhalte in einer Sprache enthält, die bei der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht registriert wurde. Zu diesem Fehler kann es auch kommen, wenn die registrierte Wörtertrennungs- oder Filterungskomponente nicht signiert wurde oder die Signaturprüfung beim Laden fehlschlug.  
  
-   Eine Komponente wie eine Wörtertrennung oder ein Filter kann nicht ausgeführt werden und gibt einen Fehler an den Indexer zurück. Dies kann vorkommen, wenn das indizierte Dokument beschädigt ist und der Filter keinen Text aus dem Dokument extrahieren kann. Dazu kann es auch kommen, wenn eine Komponente den Inhalt einer einzelnen Zeile oberhalb einer bestimmten Größe aufgrund von Arbeitsspeicherlimits beim Host des Volltextfilterdaemons (fdhost.exe) nicht verarbeiten kann.  
  
 Für jeden Fehler auf Zeilenebene enthält das Durchforstungsprotokoll Details zum Grund des Fehlers. Die Fehleranzahl wird am Ende einer vollständigen oder inkrementellen Auffüllung zusammengefasst.  
  
 Es gibt noch weitere Fehler, die den Indizierungsprozess selbst beeinträchtigen können und verhindern, dass die Auffüllung beendet wird:  
  
-   Der Volltextindex überschreitet die maximale Anzahl von Zeilen, die in einem Volltextkatalog enthalten sein dürfen.  
  
-   Ein gruppierter Index oder Volltextschlüsselindex in der indizierten Tabelle wird geändert, gelöscht oder neu erstellt.  
  
-   Ein Hardwarefehler oder eine Datenträgerbeschädigung führt zur Beschädigung des Volltextkatalogs.  
  
-   Eine Dateigruppe, die die Tabelle enthält, für die der Volltextindex erstellt werden soll, wird offline genommen oder auf schreibgeschützt gesetzt.  
  
 Untersuchen Sie das Durchforstungsprotokoll nach Abschluss eines umfangreichen Volltext-Indexauffüllungsvorgangs oder im Fall einer nicht beendeten Auffüllung.  
  
### <a name="unsigned-components"></a>Unsignierte Komponenten  
 Standardmäßig müssen vom Volltextindexer geladene Filter und Wörtertrennungen signiert sein. Wenn sie nicht signiert sind, was manchmal der Fall  ist, wenn benutzerdefinierte Komponenten installiert werden, müssen Sie den Volltextindexer so konfigurieren, dass die Signaturprüfung ignoriert wird.  
  
> [!IMPORTANT]  
>  Das Ignorieren der Signaturprüfung macht die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] weniger sicher. Es empfiehlt sich, von Ihnen implementierte Komponenten zu signieren oder sicherzustellen, dass von Ihnen erworbene Komponenten signiert sind. Informationen zum Signieren von Komponenten finden Sie unter [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
  
##  <a name="state"></a> Volltextindex nach der Wiederherstellung eines Transaktionsprotokolls inkonsistent  
 Beim Wiederherstellen des Transaktionsprotokolls einer Datenbank wird möglicherweise eine Warnung angezeigt, die besagt, dass sich der Volltextindex nicht in einem konsistenten Status befindet. Der Grund ist, dass der Volltextindex für eine Tabelle nach der Sicherung der Datenbank geändert wurde. Sie müssen eine vollständige Auffüllung (Durchforstung) für die Tabelle ausführen, um den Volltextindex in einen konsistenten Status zu versetzen. Weitere Informationen finden Sie unter [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md).  
  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [Auffüllen von Volltextindizes](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
