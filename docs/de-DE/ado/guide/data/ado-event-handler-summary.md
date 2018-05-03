---
title: ADO-Handler-ereigniszusammenfassung | Microsoft Docs
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
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 08a9f6ba0f81c1818125bd38d5c66097c21971de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ado-connection-and-recordset-events"></a>ADO-Verbindung und Recordsetereignisse
ADO-Objekten, die zwei Ereignisse auslösen können: der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt und die [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt. Die **ConnectionEvent** Familie bezieht sich auf Vorgänge auf die **Verbindung** -Objekt, und die **RecordsetEvent** Familie bezieht sich auf Vorgänge auf die  **Recordset** Objekt.

-   **Verbindungsereignisse**: Ereignisse werden ausgegeben, wenn eine Transaktion für eine Verbindung beginnt, wird ein Commit ausgeführt wurde oder ein Rollback, zurück, wenn ausgeführt wird eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) führt; beim Auftreten einer Warnung während einem **Verbindungsereignis**Operation; oder wenn eine **Verbindung** beginnt bzw. endet.

-   **Recordset-Ereignisse**: Ereignisse werden ausgegeben, um asynchrone Abrufvorgänge sowie beim Navigieren durch die Zeilen einer **Recordset** Objekt, das Ändern eines Felds in einer Zeile eine **Recordset**, Ändern Sie eine Zeile in einer **Recordset**öffnen eine **Recordset** mit einem serverseitigen Cursor zu schließen eine **Recordset**, oder ändern, ist in der  **Recordset**.

 In den folgenden Tabellen werden die Ereignisse und deren Beschreibungen zusammengefasst.

|ConnectionEvent|Description|
|---------------------|-----------------|
|[BeginTransComplete-CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Transaktionsverwaltung** – Benachrichtigungen, die für die Verbindung die aktuelle Transaktion gestartet wurde, ein Commit oder Rollback.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, trennen](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Verbindungsverwaltung** – Benachrichtigung, dass die aktuelle Verbindung gestartet wird, wurde gestartet oder beendet wurde.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Befehl Ausführung Management** – Benachrichtigung, dass die Ausführung des aktuellen Befehls für die Verbindung wird gestartet oder beendet wurde.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Nur zu Informationszwecken** – Benachrichtigung, dass zusätzliche Informationen zu den aktuellen Vorgang vorhanden ist.|

|RecordsetEvent|Description|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Status abrufen** – Benachrichtigung über den Fortschritt von einem Vorgang zum Abrufen von Daten, oder dass der Vorgang abgeschlossen wurde. Diese Ereignisse sind nur verfügbar wenn die **Recordset** mit einem clientseitigen Cursor geöffnet wurde.|
|[WillChangeField FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Feld Change Management** – Benachrichtigung, dass der Wert des aktuellen Felds ändert oder geändert hat.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Verwaltung der Navigation** – Benachrichtigung, die die aktuelle Zeile zu positionieren, in einer **Recordset** geändert wird, hat sich geändert oder das Ende erreicht hat die **Recordset**.|
|[WillChangeRecord RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Change Management Zeile** – Benachrichtigung, dass in der aktuellen Zeile der **Recordset** geändert wird oder wurde geändert.|
|[WillChangeRecordset RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Recordset Change Management** – Benachrichtigung, dass etwas im aktuellen **Recordset** geändert wird oder wurde geändert.|

## <a name="see-also"></a>Siehe auch
 [ADO-Ereignisinstanziierung von Sprache](../../../ado/guide/data/ado-event-instantiation-by-language.md) [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md) [Ereignisparameter](../../../ado/guide/data/event-parameters.md) [Zusammenwirken der Ereignishandler](../../../ado/guide/data/how-event-handlers-work-together.md) [Ereignistypen](../../../ado/guide/data/types-of-events.md)
