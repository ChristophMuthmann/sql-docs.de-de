---
title: Aktualisieren Sie aus der Datenbank (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9fcc074a16f5fc794dc4339bb58bd552371206a8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="refresh-from-database-mysqltosql"></a>Aktualisieren Sie aus der Datenbank (MySQLToSQL)
Die **aus der Datenbank aktualisieren** Dialogfeld können Sie auswählen, welche Objekte von der MySQL-Datenbank zu aktualisieren. Zeilen, die Sie im Dialogfeld sind farblich codiert, basierend auf dem Status der Metadaten:  
  
-   Wenn die Metadaten des Objekts lokal und in der MySQL-Datenbank geändert wurde, ist die Zeile blau.  
  
-   Wenn die Objektmetadaten in der MySQL-Datenbank jedoch nicht in SSMA geändert wurde, ist die Zeile gelb.  
  
-   Wenn die Metadaten des Objekts wurde lokal geändert, aber nicht in der MySQL-Datenbank, die Zeile grün ist.  
  
-   Wenn das Objekt in der MySQL-Datenbank neu ist, ist die Zeile rosa.  
  
Sie können angeben, die Einstellungen der Standardrichtlinie Objekt aktualisieren in der **Projekteinstellungen** (Dialogfeld). Weitere Informationen finden Sie unter [Projekteinstellungen &#40;Synchronisierung&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Für den Zugriff auf die **aus der Datenbank aktualisieren** mit der rechten Maustaste ein Objekt in MySQL-Metadaten-Explorer, und klicken Sie im Dialogfeld **aus der Datenbank aktualisieren**.  
  
## <a name="options"></a>enthalten  
  
|||  
|-|-|  
|**Begriff**|**Definition**|  
|**Reduzieren (-)**|Reduzieren Sie alle Objektgruppen, um einzelne Objekte auszublenden.|  
|**Erweitern (+)**|Erweitern Sie alle Objektgruppen, um einzelne Objekte anzuzeigen.|  
|**Gleich Objekte ein-/ausblenden**|Blendet Objekte aus der Liste aus, wenn die Objektmetadaten in der MySQL-Datenbank und SSMA identisch ist.|  
|**Aktualisieren Sie aus der Datenbank (Pfeil)**|Verwenden Sie die Pfeiltaste klicken, um anzugeben, dass die Metadaten für die ausgewählten Objekte in SSMA aktualisiert werden sollen.|  
|**Führen Sie aus der Datenbank nicht aktualisiert werden (X-Schaltfläche)**|Verwenden Sie die Schaltfläche "X", um anzugeben, dass die Metadaten für die ausgewählten Objekte in SSMA nicht aktualisiert werden sollten.|  
|**Legende**|Zeigt eine **Legende** (Dialogfeld). Die Legende enthält die Zuordnung zwischen Zeilenfarben und Metadaten-Status.<br /><br />Beibehalten der **Legende** Dialogfeld auf der Basis von der **aus der Datenbank aktualisieren** wählen Sie im Dialogfeld die **im Vordergrund anzeigen** Kontrollkästchen.|  
  
