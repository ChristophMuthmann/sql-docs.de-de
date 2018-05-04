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
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 49595bb772d2ac5cd49be9f67c9004f2f0e1e098
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
  
