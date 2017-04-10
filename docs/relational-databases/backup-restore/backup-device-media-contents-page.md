---
title: "Sicherungsmedium (Seite Medieninhalt) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.backupdevice.contents.f1"
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
caps.latest.revision: 38
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 38
---
# Sicherungsmedium (Seite Medieninhalt)
  Mithilfe des Dialogfelds **Sicherungsmedium** können Sie die Sicherungsinformationen anzeigen. Diese Informationen beschreiben das Gerät, die Medien, den Mediensatz und den Sicherungssatz bzw. die Sicherungssätze.  
  
 **So verwenden Sie SQL Server Management Studio zum Anzeigen des Inhalts eines Sicherungsmediums**  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## Optionen  
 Zeigt Informationen zu den einzelnen Medien, zum Mediensatz und zu den Sicherungssätzen an.  
  
 **Medien**  
 Ein Datenträger oder ein Satz von Bändern, auf dem Sicherungsinformationen gespeichert sind.  
  
 **Mediensequenz**  
 Führt die Mediensequenznummer, die Familiensequenznummer und ggf. den Spiegelbezeichner auf. Die physischen Sicherungsmedien sind jeweils mit einer Mediensequenznummer gekennzeichnet, die die Reihenfolge angibt, in der die Medien verwendet wurden. Das erste Sicherungsmedium wird mit 1 markiert, das zweite Medium (das erste Anschlussband) mit 2 usw. Beim Wiederherstellen des Sicherungssatzes stellen die Sequenznummern sicher, dass der Operator, der die Sicherung wiederherstellt, das richtige Medium in der richtigen Reihenfolge einlegt.  
  
 **Erstellt am**  
 Zeigt das Datum und die Uhrzeit der Erstellung des Mediensatzes an.  
  
 **Mediensatz**  
 Ein Mediensatz ist eine geordnete Sammlung von Sicherungsmedien, auf die mithilfe einer konstanten Anzahl von Sicherungsmedien ein oder mehrere Sicherungsvorgänge geschrieben wurden.  
  
 **Name**  
 Zeigt ggf. den Namen des Mediensatzes an.  
  
 **Beschreibung**  
 Zeigt ggf. die Beschreibung des Mediensatzes an.  
  
 **Anzahl von Medienfamilien**  
 Zeigt die Anzahl von Medienfamilien im Mediensatz an. Jeder Mediensatz ist eine Sammlung, die sich aus einer oder mehreren Medienfamilien zusammensetzt. Die gesamte Ausgabe auf ein angegebenes einzelnes Sicherungsmedium (oder eine Gruppe gespiegelter Sicherungsmedien) bildet eine einzelne Medienfamilie. Jeder Mediensatz enthält eine Medienfamilie pro separates Medium (oder Gruppe gespiegelter Medien). Wenn ein Mediensatz beispielsweise zwei nicht gespiegelte Sicherungsmedien verwendet, enthält der Mediensatz zwei Medienfamilien.  
  
 **Sicherungssätze**  
 Zeigt Informationen zum Sicherungssatz bzw. den Sicherungssätzen an, der oder die auf dem Medium enthalten sind. Ein Sicherungssatz ist das Ergebnis eines erfolgreichen Sicherungsvorgangs, dessen Inhalt auf die Medien im Satz von Sicherungsmedien verteilt wird.  
  
|Header|Werte|  
|------------|------------|  
|**Name**|Name des Sicherungssatzes.|  
|**Typ**|Das gesicherte Objekt: Datenbank, Datei oder *\<leer>* (bei Transaktionsprotokollen)|  
|**Komponente**|Der Typ der ausgeführten Sicherung: Vollständig, Differenziell oder Transaktionsprotokoll.|  
|**Server**|Name der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , durch die der Sicherungsvorgang ausgeführt wurde.|  
|**Datenbank**|Name der Datenbank, die gesichert wurde.|  
|**Position**|Position des Sicherungssatzes auf dem Volume.|  
|**Datum**|Datum und Uhrzeit des Endes des Sicherungsvorgangs, entsprechend den Ländereinstellungen des Clients.|  
|**Größe**|Größe des Sicherungssatzes in Byte.|  
|**Benutzername**|Name des Benutzers, der den Sicherungsvorgang ausgeführt hat.|  
|**Ablauf**|Datum und Uhrzeit des Zeitpunkts, an dem der Sicherungssatz verfällt.|  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
  
-   [Definieren eines logischen Sicherungsmediums für eine Datenträgerdatei &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definieren eines logischen Sicherungsmediums für ein Bandlaufwerk &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Angeben eines Datenträgers oder ein Bands als Sicherungsziel &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Löschen eines Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Festlegen des Ablaufdatums für eine Sicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Anzeigen der Inhalte eines Sicherungsbands oder einer -datei &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Anzeigen der Daten und Protokolldateien in einem Sicherungssatz &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Anzeigen der Eigenschaften und des Inhalts eines logischen Sicherungsmediums &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Wiederherstellung einer Sicherung von einem Medium &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## Siehe auch  
 [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  