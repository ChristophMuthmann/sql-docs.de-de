---
title: "Festlegen einer maximalen Dateigr&#246;&#223;e f&#252;r eine Ablaufverfolgungsdatei (SQL Server Profiler) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Maximale Dateigröße für Ablaufverfolgungen"
  - "Größe [SQL Server], Ablaufverfolgungsdateien"
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Festlegen einer maximalen Dateigr&#246;&#223;e f&#252;r eine Ablaufverfolgungsdatei (SQL Server Profiler)
  Verwenden Sie die folgende Prozedur, um die maximale Dateigröße für eine Ablaufverfolgungsdatei festzulegen.  
  
### So legen Sie die maximale Dateigröße für eine Ablaufverfolgungsdatei fest  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung zu einer Instanz von Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein.  
  
3.  Geben Sie im Feld **Vorlagenname**eine Ablaufverfolgungsvorlage aus.  
  
4.  Wählen Sie **In Datei speichern**aus, und geben Sie dann eine Datei zum Speichern der Ablaufverfolgungsinformationen an.  
  
5.  Aktivieren Sie das Kontrollkästchen **Maximale Dateigröße festlegen** , und geben Sie die maximale Dateigröße für die Ablaufverfolgung an. Erreicht die Datei die maximale Größe, werden die Ablaufverfolgungsereignisse in dieser Datei nicht mehr aufgezeichnet. Folgende Situation tritt ein, wenn Sie die Option **Dateirollover aktivieren** auswählen (dies ist standardmäßig ausgewählt):  
  
     Die Dateirolloveroption führt dazu, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die aktuelle Datei schließt und eine neue Datei erstellt, wenn die maximale Dateigröße erreicht ist. Die neue Datei hat den gleichen Namen wie die vorige, sie wird jedoch zur Angabe der Abfolge um eine ganze Zahl ergänzt. Wenn z. B. der Name der ursprünglichen Ablaufverfolgungsdatei filename_1.trc lautet, lautet der Name der folgenden Ablaufverfolgungsdatei filename_2.trc usw. Wird der einer neuen Rolloverdatei zugewiesene Name bereits von einer vorhandenen Datei verwendet, wird die vorhandene Datei überschrieben, es sei denn, sie ist schreibgeschützt. Die Dateirolloveroption ist standardmäßig aktiviert, wenn Sie Ablaufverfolgungsdaten in einer Datei speichern.  
  
     Bei aktivierter Dateirolloveroption wird die Ablaufverfolgung fortgesetzt, bis sie auf andere Weise beendet wird. Um die Ablaufverfolgung zu beenden, nachdem die Dateigrößenbeschränkung erreicht wurde, deaktivieren Sie die Dateirolloveroption.  
  
    > [!NOTE]  
    >  Durch das FAT32-Dateisystem wird die Größe von Dateien auf knapp 4 Gigabyte (GB) beschränkt. Wenn diese Dateigröße erreicht wird, schlägt die Ablaufverfolgung mit dem Fehler "Nicht genügend Speicherplatz" fehl. Verwenden Sie zum Erstellen größerer Dateien das NTFS-Dateisystem.  
  
## Siehe auch  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  