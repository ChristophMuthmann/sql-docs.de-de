---
title: Verkleinern (Task) Datenbank | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.shrinkdatabasetask.f1
helpviewer_keywords:
- Shrink Database task
- database shrinking [Integration Services]
- shrinking databases
ms.assetid: e66286f8-97b1-4e5a-86b4-e56f1932b7d5
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 09f100f683f6ecabd697f751fdac39bbabe9598f
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="shrink-database-task"></a>Datenbank verkleinern (Task)
  Der Task &amp;lt;ui&amp;gt;Datenbank verkleinern&amp;lt;/ui&amp;gt; reduziert die Größe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankdaten und -Protokolldateien.  
  
 Mithilfe des Tasks <ui>Datenbank verkleinern</ui> kann ein Paket Dateien für eine einzelne oder mehrere Datenbanken verkleinern.  
  
 Mit dem Verkleinern von Datendateien wird Platz gewonnen, indem Datenseiten vom Ende der Datei an nicht belegten Platz weiter am Dateianfang verschoben werden. Wurde am Ende der Datei ausreichend Platz geschaffen, kann die Zuordnung der Datenseiten am Ende der Datei aufgehoben und die Datenseiten können ins Dateisystem zurückgegeben werden.  
  
> [!WARNING]  
>  Die zum Verkleinern einer Datei verschobenen Daten können an beliebigen freien Platz in der Datei verschoben werden. Dies führt zur Indexfragmentierung und kann die Leistung von Abfragen, die einen Bereich des Indexes suchen, verlangsamen. Zur Vermeidung von Fragmentierung sollten die Dateiindizes nach der Verkleinerung neu erstellt werden.  
  
## <a name="commands"></a>Befehle  
 Dieser Task kapselt eine DBCC SHRINKDATABASE-Anweisung, einschließlich der folgenden Argumente und Optionen:  
  
-   *database_name*  
  
-   *target_percent*  
  
-   NOTRUNCATE oder TRUNCATEONLY.  
  
 Wenn der Task Datenbank verkleinern mehrere Datenbanken verkleinert, führt der Task mehrere SHRINKDATABASE-Befehle aus, und zwar einen Befehl pro Datenbank. Alle Instanzen des SHRINKDATABASE-Befehls verwenden die gleichen Argumentwerte; dies gilt nicht für das Argument *database_name*. Weitere Informationen finden Sie unter [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="configuration-of-the-shrink-database-task"></a>Konfiguration des Tasks "Datenbank verkleinern"  
 Eigenschaften können Sie mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen. Dieser Task ist im **-Designer in der** Toolbox **im Abschnitt** Wartungsplantasks [!INCLUDE[ssIS](../../includes/ssis-md.md)] enthalten.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Task „Datenbank verkleinern“ &#40;Wartungsplan&#41;](../../relational-databases/maintenance-plans/shrink-database-task-maintenance-plan.md)  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  

