---
title: Aktualisieren Sie aus der Datenbank (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a346119111cc876bfb794e5361a22a5cc51e593b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-from-database-oracletosql"></a>Aktualisieren Sie aus der Datenbank (OracleToSQL)
Die **aus der Datenbank aktualisieren** Dialogfeld können Sie auswählen, welche Objekte aus der Oracle-Datenbank zu aktualisieren. Zeilen, die Sie im Dialogfeld sind farblich codiert, basierend auf dem Status der Metadaten:  
  
-   Wenn die Metadaten des Objekts lokal und in der Oracle-Datenbank geändert wurde, ist die Zeile blau.  
  
-   Wenn die Objektmetadaten in der Oracle-Datenbank jedoch nicht in SSMA geändert wurde, ist die Zeile gelb.  
  
-   Wenn die Metadaten des Objekts wurde lokal geändert, aber nicht in der Oracle-Datenbank, die Zeile grün ist.  
  
-   Wenn das Objekt in der Oracle-Datenbank neu ist, ist die Zeile rosa.  
  
Sie können angeben, die Einstellungen der Standardrichtlinie Objekt aktualisieren in der **Projekteinstellungen** (Dialogfeld). Weitere Informationen finden Sie unter [Projekteinstellungen&#40;Synchronisierung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
Für den Zugriff auf die **aus der Datenbank aktualisieren** mit der rechten Maustaste ein Objekt in der Oracle-Metadaten-Explorer, und klicken Sie im Dialogfeld **aus der Datenbank aktualisieren**.  
  
## <a name="options"></a>enthalten  
**Reduzieren (-)**  
Reduzieren Sie alle Objektgruppen, um einzelne Objekte auszublenden.  
  
**Erweitern (+)**  
Erweitern Sie alle Objektgruppen, um einzelne Objekte anzuzeigen.  
  
**Gleich Objekte ein-/ausblenden**  
Blendet Objekte aus der Liste aus, wenn die Objektmetadaten in der Oracle-Datenbank und SSMA identisch ist.  
  
**Aktualisieren Sie aus der Datenbank (Pfeil)**  
Verwenden Sie die Pfeiltaste klicken, um anzugeben, dass die Metadaten für die ausgewählten Objekte in SSMA aktualisiert werden sollen.  
  
**Führen Sie aus der Datenbank nicht aktualisiert werden (X-Schaltfläche)**  
Verwenden Sie die Schaltfläche "X", um anzugeben, dass die Metadaten für die ausgewählten Objekte in SSMA nicht aktualisiert werden sollten.  
  
**Legende**  
Zeigt eine **Legende** (Dialogfeld). Die Legende enthält die Zuordnung zwischen Zeilenfarben und Metadaten-Status.  
  
Beibehalten der **Legende** Dialogfeld auf der Basis von der **aus der Datenbank aktualisieren** wählen Sie im Dialogfeld die **im Vordergrund anzeigen** Kontrollkästchen.  
  
