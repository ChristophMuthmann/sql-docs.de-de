---
title: Record-Objekt (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Record
helpviewer_keywords: Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1246dfe943ae415f7777e5924c14580fe05afbe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="record-object-ado"></a>Das Datensatzobjekt (ADO)
Stellt eine Zeile aus einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oder der Datenanbieter oder ein Objekt, das von einem Anbieter von teilweise strukturierten Daten, z. B. einer Datei oder eines Verzeichnisses zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Ein **Datensatz** -Objekt stellt eine Zeile mit Daten und verfügt über einige grundlegende ähnlichkeiten mit einer Zeile **Recordset**. Abhängig von den Funktionen Ihres Anbieters **Datensatz** Objekte können direkt von Ihrem Anbieter statt einzelne Zeilen zurückgegeben werden **Recordset**, z. B. bei einer SQL-Abfrage, die nur eine Zeile auswählt. ausgeführt. Oder, eine **Datensatz** -Objekt abgerufen werden kann, direkt aus einer **Recordset** Objekt. Oder, eine **Datensatz** direkt von einem Anbieter, die teilweise strukturierten Daten, z. B. Microsoft Exchange-OLE DB-Anbieter zurückgegeben werden kann.  
  
 Sehen Sie die zugeordneten Feldern der **Datensatz** Objekt über die [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung auf der **Datensatz** Objekt. ADO ermöglicht, einschließlich Spalten mit Objektwerten **Recordset**, **SafeArray**, und Skalare Werte in der **Felder** Auflistung von **Datensatz** -Objekte.  
  
 Wenn die **Datensatz** Objekt stellt eine Zeile in einer **Recordset**, es ist möglich, auf das ursprüngliche zurückgeben **Recordset** mit der [Quelle](../../../ado/reference/ado-api/source-property-ado-record.md) Diese Eigenschaft.  
  
 Die **Datensatz** Objekt kann auch verwendet werden von Anbietern teilweise strukturierten Daten z. B. die [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), um strukturierten Namespaces zu modellieren. Jeder Knoten in der Struktur ist eine **Datensatz** Objekt mit der zugeordneten Spalten. Die Spalten können die Attribute des Knotens und andere relevante Informationen darstellen. Die **Datensatz** Objekt kann ein Blattknoten und einen inneren Knoten in der Struktur darstellen. Nicht-Blattknoten weisen die anderen Knoten als die Inhalte allerdings Blattknoten keine solchen Inhalte. Blattknoten enthalten i. d. r. binäre Datenströme und innerer Knoten möglicherweise außerdem einen binäre Standarddatenstrom zugeordnet. Eigenschaften für die **Datensatz** Objekt zu identifizieren, den Typ des Knotens.  
  
 Die **Datensatz** Objekt stellt auch eine alternative Möglichkeit, für die Daten navigieren hierarchisch organisiert werden. Ein **Datensatz** Objekt möglicherweise zur Darstellung des Stamm einer bestimmten Unterstruktur in einer großen Struktur erstellt und neuen **Datensatz** Objekte möglicherweise geöffnet sein, um die untergeordneten Knoten darstellen.  
  
 Eine Ressource (z. B. eine Datei oder ein Verzeichnis) kann durch eine absolute URL eindeutig identifiziert werden. Ein [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt implizit erstellt und zum Festlegen der **Datensatz** Objekt bei der **Datensatz** mit eine absolute URL geöffnet wird. Ein **Verbindung** -Objekts kann explizit festgelegt werden, um die **Datensatz** Objekt über die [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft. Die Dateien und Verzeichnisse, die mithilfe von zugegriffen werden können die **Verbindung** Objekt definieren die *Kontext* in der **Datensatz** Vorgänge auftreten.  
  
 Datenmethoden Änderung und die Navigation auf die **Datensatz** Objekt akzeptieren, sondern auch eine relative URL, die eine Ressource, die über eine absolute URL sucht oder **Verbindung** Objektkontext als Ausgangspunkt.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Ein **Verbindung** Objekt bezieht sich auf jede **Datensatz** Objekt. Aus diesem Grund **Datensatz** Objektvorgänge kann Teil einer Transaktion durch den Aufruf **Verbindung** Transaktionsmethoden-Objekt.  
  
 Die **Datensatz** Objekt unterstützt keine ADO-Ereignissen und wird daher nicht auf Benachrichtigungen reagiert.  
  
 Mit den Methoden und Eigenschaften einer **Datensatz** Objekt ist, können Sie wie folgt vorgehen:  
  
-   Festlegen oder Zurückgeben des zugeordneten **Verbindung** -Objekt mit den [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft.  
  
-   Angeben der Zugriffsberechtigungen mit der [Modus](../../../ado/reference/ado-api/mode-property-ado.md) Eigenschaft.  
  
-   Die URL des Verzeichnisses, zurück, sofern vorhanden, mit der Ressource dargestellt wird, indem Sie die **Datensatz** mit der [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) Eigenschaft.  
  
-   Die absolute URL, die relative URL anzugeben oder **Recordset** aus dem die **Datensatz** wird abgeleitet, mit der [Quelle](../../../ado/reference/ado-api/source-property-ado-record.md) Eigenschaft.  
  
-   Geben Sie den aktuellen Status des der **Datensatz** mit der [Zustand](../../../ado/reference/ado-api/state-property-ado.md) Eigenschaft.  
  
-   Geben Sie den Typ des **Datensatz** – *einfache*, *Auflistung*, oder *strukturierte Dokument* – mit der [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)Eigenschaft.  
  
-   Beendet einen asynchronen Vorgang mit der ["Abbrechen"](../../../ado/reference/ado-api/cancel-method-ado.md) Methode.  
  
-   Heben Sie die Zuordnung der **Datensatz** aus einer Datenquelle mit dem [schließen](../../../ado/reference/ado-api/close-method-ado.md) Methode.  
  
-   Kopieren Sie die Datei oder das Verzeichnis dargestellt durch eine **Datensatz** an einen anderen Speicherort mit der [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) Methode.  
  
-   Löschen Sie die Datei oder das Verzeichnis und die Unterverzeichnisse, dargestellt durch eine **Datensatz** mit der [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) Methode.  
  
-   Öffnen einer **Recordset** enthält Zeilen, die die Unterverzeichnisse und Dateien der dargestellte Entität darstellen der **Datensatz** mit der [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) Methode.  
  
-   Verschieben (Umbenennen) die Datei oder Verzeichnis und Unterverzeichnisse, dargestellt durch eine **Datensatz** an einen anderen Speicherort mit der [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) Methode.  
  
-   Ordnen Sie die **Datensatz** mit einer vorhandenen Datenquelle-Datenquelle aus, oder erstellen Sie eine neue Datei oder ein Verzeichnis mit der [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md) Methode.  
  
 Die **Datensatz** Objekt für die Skripterstellung sicher ist.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Record-Objekt – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Fields-Auflistung (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Datensätze und Datenströme](../../../ado/guide/data/records-and-streams.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
