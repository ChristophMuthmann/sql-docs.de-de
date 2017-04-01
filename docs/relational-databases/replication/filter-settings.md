---
title: "Filtereinstellungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.filtersettings.f1"
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
caps.latest.revision: 6
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 6
---
# Filtereinstellungen
  Im Dialogfeld **Filtereinstellungen** können Sie Filter für Raster im Replikationsmonitor definieren. Wenn Sie z. B. nur die aktiven Abonnements auf der Registerkarte **Alle Abonnements** anzeigen möchten, wählen Sie in der Spalte **Spaltenname** den Eintrag **Status** , in der Spalte **Operator** den Eintrag **Ist gleich** und in der Spalte **Wert1** den Eintrag **Aktiv** aus. Wenn Sie einen auf einer oder mehreren Spalten basierenden Filter definiert haben, wird dieser Filter angewendet, sodass im Raster nur die Teilmenge von Zeilen angezeigt wird, die die Filterkriterien erfüllen.  
  
## Optionen  
 **Spaltenname**  
 Wählen Sie den Namen der Spalte aus, für die Sie einen Filter definieren möchten. Sie können einen Filter für eine oder mehrere Spalten definieren.  
  
 **Operator**  
 Wählen Sie einen Operator für den Filter ein, z. B. **kleiner als oder gleich**.  
  
 **Wert1** und **Wert2**  
 Geben Sie einen Wert für den Filter ein, oder wählen Sie einen Wert aus. Für die meisten Operatoren muss nur in der Spalte **Wert1** ein Wert eingegeben werden. Für die Operatoren **Zwischen** und **Nicht zwischen** muss jedoch auch in der Spalte **Wert2** ein Wert eingegeben werden.  
  
 **Filter löschen**  
 Klicken Sie auf diese Schaltfläche, um alle definierten Filter zu löschen. Wenn Sie einen einzelnen Filter entfernen möchten, wählen Sie die Filterzeile aus, und drücken Sie die ENTF-TASTE.  
  
## Siehe auch  
 [Überwachen der Replikation](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  