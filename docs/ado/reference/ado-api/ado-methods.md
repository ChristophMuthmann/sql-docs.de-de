---
title: ADO-Methoden | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4a2b180e8886931819dafe089e9012dcaa578694
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="ado-methods"></a>ADO-Methoden
|||  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|Erstellt einen neuen Datensatz für ein aktualisierbares **Recordset** Objekt.|  
|[Anfügen](../../../ado/reference/ado-api/append-method-ado.md)|Fügt ein Objekt für eine Sammlung an. Wenn die Auflistung **Felder**, ein neues **Feld** Objekt kann erstellt werden, bevor sie auf die Auflistung angefügt wird.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|Fügt Daten an eine große Text- oder Binärdaten **Feld**, oder auf eine **Parameter** Objekt.|  
|[BeginTrans, CommitTrans und RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|Verwaltet die transaktionsverarbeitung in einem **Verbindung** Objekt wie folgt:<br /><br /> **BeginTrans** – beginnt eine neue Transaktion.<br /><br /> **CommitTrans** – speichert alle Änderungen, und beendet die aktuelle Transaktion. Es kann auch eine neue Transaktion starten.<br /><br /> **RollbackTrans** – verwirft alle Änderungen, und beendet die aktuelle Transaktion. Es kann auch eine neue Transaktion starten.|  
|[Abbrechen](../../../ado/reference/ado-api/cancel-method-ado.md)|Bricht die Ausführung einer ausstehenden asynchronen Methodenaufrufs.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|Bricht einen ausstehenden BatchUpdate ab.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|Verwirft alle Änderungen, die an die aktuelle oder neue Zeile vorgenommen wurden eine **Recordset** -Objekt, oder die **Felder** Auflistung von einer **Datensatz** -Objekt, vor dem Aufruf der  **Update** Methode.|  
|[Löschen](../../../ado/reference/ado-api/clear-method-ado.md)|Entfernt alle der **Fehler** Objekte aus der **Fehler** Auflistung.|  
|[Klon](../../../ado/reference/ado-api/clone-method-ado.md)|Erstellt ein Duplikat **Recordset** Objekt aus einer vorhandenen **Recordset** Objekt. Optional gibt an, dass der Klon schreibgeschützt ist.|  
|[Schließen](../../../ado/reference/ado-api/close-method-ado.md)|Schließt einen geöffneten Objekt und alle abhängigen Objekte.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|Vergleicht zwei Textmarken und gibt eine Angabe über das Verhältnis der entsprechenden Werte zurück.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|Kopiert eine Datei oder Verzeichnis und dessen Inhalt an einen anderen Speicherort an.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|Kopiert die angegebene Anzahl von Zeichen oder Bytes (je nach **Typ**) in der **Stream** in eine andere **Stream** Objekt.|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|Erstellt ein neues **Parameter** Objekt, das die angegebenen Eigenschaften verfügt.|  
|[Löschen Sie (ADO-Parameters-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|Löscht ein Objekt aus der **Parameter** Auflistung.|  
|[Löschen Sie (ADO Fields-Auflistung)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|Löscht ein Objekt aus der **Felder** Auflistung.|  
|[Löschen Sie (ADO-Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|Löscht den aktuellen Datensatz oder eine Gruppe von Datensätzen.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|Löscht eine Datei oder Verzeichnis und alle Unterverzeichnisse.|  
|[Führen Sie (ADO-Befehl)](../../../ado/reference/ado-api/execute-method-ado-command.md)|Führt die Abfrage, die SQL-Anweisung oder die gespeicherte Prozedur, die im angegebenen der **CommandText** Eigenschaft.|  
|[Führen Sie (ADO-Verbindung)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|Führt die angegebene Abfrage, SQL-Anweisung, gespeicherte Prozedur oder anbieterspezifischen Text.|  
|[Suchen](../../../ado/reference/ado-api/find-method-ado.md)|Sucht eine **Recordset** für die Zeile, die die angegebenen Kriterien erfüllt.|  
|[leeren](../../../ado/reference/ado-api/flush-method-ado.md)|Erzwingt, dass der Inhalt des der **Stream** verbleiben in der ADO-Puffer, in der zugrunde liegenden Objekts, dem die **Stream** zugeordnet ist.|  
|[get_OLEDBCommand-Methode](../../../ado/reference/ado-api/get-oledbcommand-method.md)|Gibt den zugrunde liegenden OLE DB-Befehl, weitergeben zuerst alle Parameterinformationen für den ADO-Befehl festgelegt, um den OLE DB-Befehl.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|Gibt eine **Recordset** darstellen, deren Zeilen, die Dateien und Unterverzeichnisse im Verzeichnis dargestellt, die von diesem **Datensatz**.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|Gibt alle oder einen Teil des Inhalts eines große Text-oder Binärdaten **Feld** Objekt.|  
|[GetDataProviderDSO-Methode](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Ruft das zugrunde liegende Objekt für den OLE DB-Datenquelle aus der Shape-Anbieters ab.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|Ruft mehrere Datensätze eine **Recordset** -Objekt in ein Array.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|Gibt die **Recordset** als Zeichenfolge.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|Lädt den Inhalt einer vorhandenen Datei in eine **Stream**.|  
|[Verschieben](../../../ado/reference/ado-api/move-method-ado.md)|Verschiebt die Position des aktuellen Datensatzes in einem **Recordset** Objekt.|  
|[MoveFirst, MoveLast, MoveNext und MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|Wechselt zum ersten, letzten, nächsten oder vorherigen Datensatz in einem angegebenen **Recordset** Objekt und macht, die zum aktuellen Datensatz.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|Verschiebt eine Datei oder ein Verzeichnis und dessen Inhalt an einen anderen Speicherort an.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|Löscht die aktuelle **Recordset** -Objekt und gibt die nächste **Recordset** durch eine Reihe von Befehlen gelangt.|  
|[Öffnen Sie (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)|Öffnet eine Verbindung mit einer Datenquelle.|  
|[Öffnen Sie (ADO-Datensatz)](../../../ado/reference/ado-api/open-method-ado-record.md)|Öffnet ein vorhandenes **Datensatz** -Objekt oder erstellt eine neue Datei oder ein Verzeichnis.|  
|[Öffnen Sie (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|Öffnet einen Cursor.|  
|[Öffnen Sie (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)|Öffnet eine **Stream** Objekt Datenströme Binär oder Text zu bearbeiten.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|Ruft die Schemainformationen für die Datenbank vom Anbieter ab.|  
|[put_OLEDBCommand-Methode](../../../ado/reference/ado-api/put-oledbcommand-method.md)|Diese Methode führt keine Operation – sie stets S_OK zurückgibt.|  
|[Lesen](../../../ado/reference/ado-api/read-method.md)|Liest eine angegebene Anzahl von Bytes aus einem **Stream** Objekt.|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|Liest eine angegebene Anzahl von Zeichen aus einem Textobjekt **Stream** Objekt.|  
|[Aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md)|Aktualisiert die Objekte in einer Auflistung von verfügbaren Objekte entsprechend, und spezifische an den Anbieter an.|  
|[Requery](../../../ado/reference/ado-api/requery-method.md)|Aktualisiert die Daten in einem **Recordset** Objekt durch erneutes Ausführen der Abfrage auf der das Objekt basiert.|  
|[Erneut synchronisieren](../../../ado/reference/ado-api/resync-method.md)|Aktualisiert die Daten in der aktuellen **Recordset** -Objekt, oder **Felder** Auflistung von einem **Datensatz** Objekt, aus der zugrunde liegenden Datenbank.|  
|[Speichern](../../../ado/reference/ado-api/save-method.md)|Speichert die **Recordset** in einer Datei oder **Stream** Objekt.|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|Speichert den binären Inhalt von einem **Stream** in eine Datei.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|Sucht den Index des eine **Recordset** schnell die Zeile finden, die mit den angegebenen Werten übereinstimmt, und ändert die aktuelle Zeilenposition Zeile.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|Legt die Position, die das Ende des Streams fest.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|Überspringt eine gesamte Zeile, beim Lesen eines Text-Streams.|  
|[STAT](../../../ado/reference/ado-api/stat-method.md)|Ruft die statistische Informationen zu einem geöffneten Datenstrom ab.|  
|[Unterstützt](../../../ado/reference/ado-api/supports-method.md)|Bestimmt, ob ein angegebener **Recordset** Objekt unterstützt eine bestimmte Art von Funktionen.|  
|[Update](../../../ado/reference/ado-api/update-method.md)|Speichert alle Änderungen an der aktuellen Zeile ein **Recordset** -Objekt, oder die **Felder** Auflistung von einem **Datensatz** Objekt.|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|Schreibt alle ausstehenden BatchUpdates auf den Datenträger an.|  
|[Schreiben](../../../ado/reference/ado-api/write-method.md)|Schreibt binäre Daten in einem **Stream** Objekt.|  
|[WRITETEXT-Anweisung](../../../ado/reference/ado-api/writetext-method.md)|Schreibt eine angegebene Zeichenfolge an eine **Stream** Objekt.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md)   
 [Dynamische Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO--Enumerationskonstanten](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md)   
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO-Objekte und Schnittstellen](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO-Eigenschaften](../../../ado/reference/ado-api/ado-properties.md)
