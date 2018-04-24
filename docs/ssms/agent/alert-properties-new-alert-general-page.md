---
title: Warnungseigenschaften – Neue Warnung (Seite „Allgemein“) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ag.alert.general.f1
ms.assetid: f5c11610-62e3-44df-9800-a5dc35be4a09
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f9a23a0e81e295034395a799d472ee47c92d5345
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alert-properties---new-alert-general-page"></a>Warnungseigenschaften – Neue Warnung (Seite „Allgemein“)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]


> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Mithilfe dieser Seite können Sie die allgemeinen Eigenschaften von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Warnungen anzeigen und ändern.  

## <a name="options"></a>Tastatur  
**Name**  
Ändern Sie den Namen der Warnung.  
  
**Aktivieren von**  
Aktivieren Sie die Warnung. Wenn die Warnung nicht aktiviert ist, werden die in der Warnung angegebenen Aktionen nicht ausgeführt.  
  
**Typ**  
Wählen Sie den Typ der Warnung aus:  
  
-   **SQL Server-Ereigniswarnung** reagiert auf Meldungen im [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Ereignisprotokoll.  
  
-   **SQL Server-Leistungsstatuswarnung** reagiert auf eine bestimmte Bedingung in einem Leistungsindikator.  
  
-   **WMI-Ereigniswarnung** reagiert auf ein WMI-Ereignis (Windows Management Instrumentation).  
  
## <a name="sql-server-event-alert-options"></a>Optionen für die SQL Server-Ereigniswarnung  
**Datenbankname**  
Geben Sie eine Datenbank für das Ereignis an, oder geben Sie **Alle Datenbanken** an, damit auf eine Meldung unabhängig von der Datenbank reagiert wird, in der das Ereignis auftritt.  
  
**Fehlernummer**  
Geben Sie an, dass dieses Ereignis auf einen Fehler reagiert, und geben Sie die Fehlernummer an.  
  
**Severity**  
Geben Sie an, dass dieses Ereignis auf alle Meldungen innerhalb eines bestimmten Schweregrads reagiert, und geben Sie den Schweregrad an.  
  
**Warnung auslösen, wenn eine Meldung Folgendes enthält**  
Filtert Ereignisse nach einer bestimmten Zeichenfolge. Wenn diese Option ausgewählt ist, reagiert die Warnung nur auf Ereignisse, die eine bestimmte Zeichenfolge enthalten.  
  
**Meldungstext**  
Geben Sie die Zeichenfolge ein, die zum Filtern von Ereignissen verwendet werden soll.  
  
## <a name="sql-server-performance-condition-alerts"></a>SQL Server-Leistungsstatuswarnungen  
**Objekt**  
Geben Sie das zu überwachende Leistungsobjekt an.  
  
**Leistungsindikator**  
Geben Sie den Leistungsindikator innerhalb des Leistungsobjekts an, der überwacht werden soll.  
  
**Instanz**  
Geben Sie die Instanz des Leistungsindikators an, die überwacht werden soll.  
  
**Warnung, falls Leistungsindikator**  
Geben Sie das Verhalten des Leistungsindikators an, auf das die Warnung reagiert. Die Warnung könnte beispielsweise auf eine Bedingung reagieren, bei der der Wert des Leistungsindikators **Freier Speicherplatz in 'tempdb' (KB)** unter eine bestimmte Grenze fällt, oder auf eine Bedingung, bei der der Wert für **SQL-Kompilierungen/Sekunde** einen bestimmten Wert übersteigt.  
  
**ReplTest1**  
Geben Sie einen Wert für den Leistungsindikator an.  
  
## <a name="wmi-event-alert-options"></a>WMI-Ereigniswarnungsoptionen  
**Namespace**  
Geben Sie den Namespace an, der für die WQL-Anweisung (WMI Query Language) verwendet werden soll. Es werden nur Namespaces auf dem Computer unterstützt, auf dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent ausgeführt wird.  
  
**Dataseteigenschaften**  
Geben Sie die WQL-Anweisung an, die das Ereignis identifiziert, auf das die Warnung reagiert.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Warnungen](../../ssms/agent/alerts.md)  
[Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://msdn.microsoft.com/en-us/58b67426-1e66-4445-8e2c-03182e94c4be)  
[Erstellen einer Warnung mithilfe einer Fehlernummer](../../ssms/agent/create-an-alert-using-an-error-number.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
