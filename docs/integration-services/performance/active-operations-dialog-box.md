---
title: "Aktive Vorg&#228;nge (Dialogfeld) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isoperations.executions.f1"
  - "sql13.ssis.ssms.isoperations.general.f1"
ms.assetid: 5bb0fcd6-0ce9-488a-85b8-25dddaa03cda
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Aktive Vorg&#228;nge (Dialogfeld)
  Verwenden Sie das Dialogfeld **Aktive Vorgänge** , um den Status der derzeit ausgeführten [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Vorgänge auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server anzuzeigen, z. B. Bereitstellung, Überprüfung und Paketausführung. Diese Daten werden im SSISDB-Katalog gespeichert.  
  
 Weitere Informationen zu verwandten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Ansichten finden Sie unter [catalog.operations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md), [catalog.validations &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) und [catalog.executions &#40;SSISDB-Datenbank&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).  
  
 **Was möchten Sie tun?**  
  
-   [Dialogfeld "Aktive Vorgänge" öffnen](../../integration-services/performance/active-operations-dialog-box.md#open_dialog)  
  
-   [enthalten](#options)  
  
##  <a name="open_dialog"></a> Dialogfeld "Aktive Vorgänge" öffnen  
  
1.  Öffnen Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Stellen Sie eine Verbindung mit einer Microsoft SQL Server-Datenbank her.  
  
3.  Erweitern Sie im Objekt-Explorer den Knoten **Integration Services**, klicken Sie mit der rechten Maustaste auf den Knoten **SSISDB**, und klicken Sie dann auf **Aktive Vorgänge**.  
  
## Konfigurieren der Optionen  
  
###  <a name="options"></a> enthalten  
 **Typ**  
 Gibt den Vorgangstyp an. Im Folgenden sind die Werte aufgeführt, die im Feld **Typ** zulässig sind, und die entsprechenden Werte in der operations_type-Spalte der Transact-SQL-Sicht **catalog.operations**.  
  
|||  
|-|-|  
|Initialisierung der Integration Services|1|  
|Vorgangsbereinigung (SQL Agent-Auftrag)|2|  
|Projektversions-Cleanup (SQL Agent-Auftrag)|3|  
|Projekt bereitstellen|101|  
|Projekt wiederherstellen|106|  
|Paketausführung erstellen und starten|200|  
|Vorgang beenden (Beenden einer Überprüfung oder Ausführung)|202|  
|Projekt überprüfen|300|  
|Paket überprüfen|301|  
|Katalog konfigurieren|1000|  
  
 **Beenden**  
 Klicken Sie, um einen gerade ausgeführten Vorgang zu beenden.  
  
  