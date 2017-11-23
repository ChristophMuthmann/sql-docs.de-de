---
title: Stream-Objekt (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Stream
helpviewer_keywords: Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 05f40c6060440d1f8535ec4d79b18a6438b766ec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="stream-object-ado"></a>Streamobjekt (ADO)
Stellt einen Datenstrom von Binärdaten oder Text dar.  
  
 In Hierarchien Strukturbaums, z. B. ein Dateisystem oder eine e-Mail-System eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) möglicherweise standardmäßig Binärdatenstrom Bits zugeordnet, die den Inhalt der Datei oder die e-Mail-Nachricht enthält. Ein **Stream** Objekt kann verwendet werden, um Felder oder Datensätze, enthält diese Datenströme zu bearbeiten. Ein **Stream** Objekt kann auf folgende Weise abgerufen werden:  
  
-   Von einer URL verweist auf ein Objekt (i. d. r. eine Datei), Binär oder Text-Daten enthält. Diesem Objekt kann es sich um ein einfaches Dokument eine **Datensatz** Objekt, das ein strukturiertes Dokument bzw. in einem Ordner darstellt.  
  
-   Durch Öffnen des **Stream** mit einem **Datensatz** Objekt. Sie erhalten den Standarddatenstrom zugeordnet eine **Datensatz** Objekt bei der **Datensatz** geöffnet wird, um einen Roundtrip zum Öffnen des Datenstroms zu vermeiden.  
  
-   Durch Instanziieren einer **Stream** Objekt. Diese **Stream** Objekte können zum Speichern von Daten im Rahmen Ihrer Anwendung verwendet werden. Im Gegensatz zu einer **Stream** eine URL oder den Standardwert zugeordnet **Stream** von einer **Datensatz**, instanziierten **Stream** weist keine Zuordnung mit ein zugrunde liegende Datenquelle standardmäßig.  
  
 Mit den Methoden und Eigenschaften einer **Stream** Objekt ist, können Sie wie folgt vorgehen:  
  
-   Öffnen einer **Stream** -Objekt aus einer **Datensatz** oder URL mit der [öffnen](../../../ado/reference/ado-api/open-method-ado-stream.md) Methode.  
  
-   Schließen einer **Stream** mit der [schließen](../../../ado/reference/ado-api/close-method-ado.md) Methode.  
  
-   Eingeben von Bytes oder Text, der eine **Stream** mit der [schreiben](../../../ado/reference/ado-api/write-method.md) und [WriteText](../../../ado/reference/ado-api/writetext-method.md) Methoden.  
  
-   Liest Bytes aus dem **Stream** mit der [lesen](../../../ado/reference/ado-api/read-method.md) und [ReadText](../../../ado/reference/ado-api/readtext-method.md) Methoden.  
  
-   Schreiben Sie alle **Stream** Daten immer noch in der ADO-Puffer auf die zugrunde liegende Objekt mit der [leeren](../../../ado/reference/ado-api/flush-method-ado.md) Methode.  
  
-   Kopieren Sie den Inhalt von einer **Stream** in eine andere **Stream** mit der [' CopyTo ' für](../../../ado/reference/ado-api/copyto-method-ado.md) Methode.  
  
-   Steuern, wie Zeilen gelesen werden, aus der Quelldatei mit der [SkipLine](../../../ado/reference/ado-api/skipline-method.md)Methode und die [Zeilentrennzeichen](../../../ado/reference/ado-api/lineseparator-property-ado.md) Eigenschaft.  
  
-   Bestimmen Sie das Ende des Streamposition mit dem [EOS](../../../ado/reference/ado-api/eos-property.md)Eigenschaft und [SetEOS](../../../ado/reference/ado-api/seteos-method.md) Methode.  
  
-   Speichern und Wiederherstellen von Daten in Dateien mit der [SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)und [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md) Methoden.  
  
-   Geben Sie den Zeichensatz für das Speichern der **Stream** mit der [Charset](../../../ado/reference/ado-api/charset-property-ado.md) Eigenschaft.  
  
-   Anhalten eines asynchronen **Stream** Vorgang mit der ["Abbrechen"](../../../ado/reference/ado-api/cancel-method-ado.md) Methode.  
  
-   Bestimmen Sie die Anzahl der Bytes in einem **Stream** mit der [Größe](../../../ado/reference/ado-api/size-property-ado-stream.md) Eigenschaft.  
  
-   Steuern Sie die aktuelle Position innerhalb einer **Stream** mit der [Position](../../../ado/reference/ado-api/position-property-ado.md) Eigenschaft.  
  
-   Bestimmen Sie den Typ der Daten in einem **Stream** mit der [Typ](../../../ado/reference/ado-api/type-property-ado-stream.md) Eigenschaft.  
  
-   Bestimmen des aktuellen Status des der **Stream** ("geschlossen", öffnen oder ausführen) mit der [Zustand](../../../ado/reference/ado-api/state-property-ado.md) Eigenschaft.  
  
-   Geben Sie den Zugriffsmodus für die **Stream** mit der [Modus](../../../ado/reference/ado-api/mode-property-ado.md) Eigenschaft.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Die **Stream** Objekt für die Skripterstellung sicher ist.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Stream-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datensätze und Datenströme](../../../ado/guide/data/records-and-streams.md)
