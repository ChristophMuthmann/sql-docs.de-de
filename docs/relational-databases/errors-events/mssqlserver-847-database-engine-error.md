---
title: MSSQLSERVER_847 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 16faf8a17c540e25650ce35b298895dc5704e45f
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver847"></a>MSSQLSERVER_847
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|847|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|Nicht zutreffend|  
|Meldungstext|Timeout beim Warten auf einen Latch: Klasse „%ls“, ID „%p“, Typ „%d“, Task „0x%p“ : „%d“, Wartezeit „%d“, Flags „0x%I64x“, besitzender Task „0x%p“. Der Wartevorgang wird fortgesetzt.|  
  
## <a name="explanation"></a>Erklärung  
Möglicherweise reagiert ein Computer nicht mehr (der Computer hängt), oder ein Timeout bzw. eine andere Unterbrechung des regulären Betriebs tritt möglicherweise zur gleichen Zeit auf, wenn von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Pufferlatchfehler in das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll geschrieben werden.  
  
Wenn im STAT-Feld in der Meldung der Wert 0x04 aktiviert ist, wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein E/A-Vorgang erwartet. Zudem wird möglicherweise die Meldung [MSSQLSERVER_833](~/relational-databases/errors-events/mssqlserver-833-database-engine-error.md) im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll ausgegeben.  
  
Wenn im STAT-Feld in der Meldung der Wert 0x04 deaktiviert ist, bestehen für eine Seite schwerwiegende Konflikte. Wenn es sich bei dem Objekt um eine Datenseite handelt, kann dies auf ineffiziente Codeentwürfe zurückzuführen sein. Wenn die Seite keine Daten darstellt, wird der Fehler möglicherweise durch Serverengpässe wie unzureichende Hardwareressourcen verursacht.  
  
## <a name="user-action"></a>Benutzeraktion  
Wenn Sie dieses Problem umgehen möchten, werden die Fehlermeldungen in Abhängigkeit von Ihrer Umgebung durch einen oder mehrere der folgenden Schritte möglicherweise reduziert oder behoben:  
  
-   Ermitteln Sie, ob Hardware-Engpässe vorliegen. Rüsten Sie gegebenenfalls Ihre Hardware auf, sodass die Konfigurations-, Abfrage- und Ladeanforderungen Ihrer Umgebung unterstützt werden. Weitere Informationen zu Engpässen finden Sie unter [Identifizieren von Engpässen](~/relational-databases/performance/identify-bottlenecks.md).  
  
-   Überprüfen Sie alle protokollierten Fehler, und führen Sie alle von Ihrem Hardwarehersteller bereitgestellten Diagnosen aus.  
  
-   Stellen Sie sicher, dass Ihre Laufwerke nicht komprimiert sind. Das Speichern von Daten bzw. Protokolldateien auf komprimierten Laufwerken wird nicht unterstützt. Weitere Informationen zu Dateien und Dateigruppen finden Sie unter [Database Files and Filegroups](~/relational-databases/databases/database-files-and-filegroups.md).  
  
-   Prüfen Sie, ob die Fehlermeldungen behoben werden, wenn Sie folgende Optionen deaktivieren:  
  
    -   SQL Server-Prioritätserhöhung (Konfigurationsoption)  
  
    -   Lightweightpooling (Fibermodus), Option  
  
    -   Festgelegte Workingsetgröße (Option)  
  
    > [!NOTE]  
    > Die vorherigen Einstellungen können häufig kontraproduktiv sein, wenn Sie die Standardeinstellung OFF ändern. Weitere Informationen finden Sie unter [Serverkonfigurationsoptionen &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
-   Optimieren Sie die Abfragen, um die für das System verwendeten Ressourcen zu reduzieren. Durch Leistungsoptimierung kann die Belastung für ein System reduziert und die Reaktionszeit für einzelne Abfragen verbessert werden.  
  
-   Legen Sie die Option AUTO_SHRINK auf OFF fest, um den Aufwand für Änderungen an der Datenbankgröße zu verringern.  
  
-   Stellen Sie sicher, dass Sie die Option FILEGROWTH auf Inkremente festlegen, die groß genug sind und somit nicht häufig auftreten. Planen Sie einen Auftrag, um den verfügbaren Speicherplatz in den Datenbanken zu überprüfen, und erhöhen Sie dann die Datenbankgröße außerhalb der Spitzenzeiten.  
  

