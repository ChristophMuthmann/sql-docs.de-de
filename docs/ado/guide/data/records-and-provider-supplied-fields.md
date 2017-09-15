---
title: "Datensätze und Felder Anbieter bereitgestellte | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93b97bce2562604a01c564a376bd093abb9b1b7c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="records-and-provider-supplied-fields"></a>Datensätze und Felder Anbieter bereitgestellte
Wenn eine [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt geöffnet ist, werden seine Quelle kann die aktuelle Zeile eines geöffneten [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), eine absolute URL oder eine relative URL in Verbindung mit einem geöffneten [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt .  
  
 Wenn die **Datensatz** geöffnet wird eine **Recordset**, **Datensatz** Objekt [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) -Auflistung enthält alle Felder aus der ** Recordset**, sowie alle Felder, die vom zugrunde liegenden Anbieter hinzugefügt wurden.  
  
 Der Anbieter kann weitere Felder, die als ergänzende Merkmale des dienen Einfügen der **Datensatz**. Folglich eine **Datensatz** möglicherweise eindeutige Felder nicht in der **Recordset** als Ganzes oder any **Datensatz** abgeleitet aus einer anderen Zeile die **Recordset**.  
  
 Z. B. alle Zeilen von einer **Recordset** in einer E-mail-Datenquelle z. B., um Spalten verfügen, und für die Themenbereichsdatenbank abgeleitet. Ein **Datensatz** abgeleitet, **Recordset** müssen die gleichen Felder. Allerdings die **Datensatz** möglicherweise auch andere Felder nur für die Meldung durch, die dargestellt **Datensatz**, z. B. Anlage und Cc (Cc).  
  
 Obwohl die **Datensatz** -Objekt und der aktuellen Zeile der **Recordset** haben die gleichen Felder sind sie unterschiedlich da **Datensatz** und **Recordset**Objekte verfügen über verschiedene Methoden und Eigenschaften.  
  
 Ein Feld frei, die gemeinsam die **Datensatz** und **Recordset** auf entweder Objekt geändert werden kann. Allerdings kann nicht das Feld gelöscht werden, auf die **Datensatz** -Objekt, obwohl die zugrunde liegenden Anbieter unterstützen, ist das Feld auf null setzen.  
  
 Nach der **Datensatz** wird geöffnet, Sie können programmgesteuert Felder hinzufügen. Sie können auch Felder, die Sie hinzugefügt haben, löschen, aber Löschen von Feldern kann nicht aus dem ursprünglichen **Recordset**.  
  
 Sie können auch öffnen, die **Datensatz** Objekt direkt über eine URL. In diesem Fall die Felder hinzugefügt, um die **Datensatz** hängen von den zugrunde liegenden Anbieter. Derzeit die meisten Anbieter hinzufügen einen Satz von Feldern, die beschreiben, die Entität, dargestellt durch die **Datensatz**. Wenn die Entität einen Datenstrom von Bytes, z. B. eine einfache Datei besteht eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt kann in der Regel aus geöffnet werden die **Datensatz**.  
  
## <a name="special-fields-for-document-source-providers"></a>Spezielle Felder für Datenquelle Anbieter  
 Eine Sonderklasse von Anbietern aufgerufen *dokumentieren Anbietern*, verwaltet Ordner und Dokumente. Wenn eine **Datensatz** Objekt stellt ein Dokument oder eine **Recordset** Objekt stellt einen Ordner von Dokumenten dar, der Dokumentquellenanbieter füllt diese Objekte mit einem eindeutigen Satz von Feldern, die beschreiben Eigenschaften des Dokuments dokumentieren Sie stattdessen den tatsächlichen selbst. In der Regel ein Feld enthält einen Verweis auf die **Stream** , die das Dokument darstellt.  
  
 Diese Felder bilden eine Ressource **Datensatz** oder **Recordset** und für die Anbieter, die sie in unterstützen aufgelisteten [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Zwei Konstanten Index die **Felder** Auflistung einer Ressource **Datensatz** oder **Recordset** zum Abrufen von ein Paar von häufig verwendeten Felder. Die **Feld** Objekt [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft gibt den gewünschten Inhalt zurück.  
  
-   Das Feld mit Zugriff auf die **AdDefaultStream** Konstante enthält einen Standarddatenstrom zugeordnet der **Datensatz** oder **Recordset** Objekt. Der Anbieter weist einen Standarddatenstrom auf ein Objekt.  
  
-   Das Feld mit Zugriff auf die **AdRecordURL** Konstante enthält die absolute URL, die das Dokument kennzeichnet.  
  
 Ein Anbieter unterstützt nicht die [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung von **Datensatz** und **Feld** Objekte. Der Inhalt der **Eigenschaften** Auflistung ist null für diese Objekte.  
  
 Ein Anbieter kann eine anbieterspezifische Eigenschaft hinzufügen, z. B. **Datenquellentyp** herausfinden, ob es sich um ein Anbieter ist. Weitere Informationen zum Bestimmen des Typs des Anbieters finden in der Dokumentation Ihres Anbieters.  
  
## <a name="resource-recordset-columns"></a>Ressource Recordsetspalten  
 Ein *Ressourcenrecordset* besteht aus den folgenden Spalten.  
  
|Spaltenname|Typ|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Schreibgeschützt. Gibt die URL der Ressource an.|  
|RESOURCE_PARENTNAME|AdVarWChar|Schreibgeschützt. Gibt die absolute URL des übergeordneten Datensatzes an.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Schreibgeschützt. Gibt die absolute URL der Ressource, also die Verkettung von PARENTNAME und PARSENAME an.|  
|RESOURCE_ISHIDDEN|AdBoolean|"True", wenn die Ressource ausgeblendet ist. Wenn der Befehl, der das Rowset explizit erstellt Auswahl der Zeilen, in denen RESOURCE_ISHIDDEN "true" ist, werden keine Zeilen zurückgegeben.|  
|RESOURCE_ISREADONLY|AdBoolean|"True", wenn die Ressource schreibgeschützt ist. Versuche zum Öffnen dieser Ressource mit DBBINDFLAG_WRITE wird ein Fehler auf, mit schlägt der Vorgang fehl. Diese Eigenschaft kann bearbeitet werden, selbst wenn die Ressource nur zum Lesen geöffnet wurde.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Zeigt die häufige Verwendung des Dokuments an – beispielsweise einen Anwalt kurze des. Dies kann die Office-Projektvorlage entsprechen, der verwendet wurde, um das Dokument zu erstellen.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Gibt den MIME-Typ des Dokuments, der angibt, wie z. B. auf des Formats "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Gibt die Sprache, in der der Inhalt gespeichert wird.|  
|RESOURCE_CREATIONTIME|adFileTime|Schreibgeschützt. Gibt eine FILETIME-Struktur, die den Zeitpunkt enthält, an den die Ressource erstellt wurde. Die Zeit wird im Format der koordinierten Weltzeit (Coordinated Universal Time, UTC) gemeldet.|  
|RESOURCE_LASTACCESSTIME|AdFileTime|Schreibgeschützt. Gibt eine FILETIME-Struktur, die den Zeitpunkt enthält, den die Ressource zuletzt zugegriffen wurde. Die Uhrzeit wird im UTC-Format. FILETIME-Elemente sind 0 (null), wenn der Anbieter diese Zeitelement nicht unterstützt.|  
|RESOURCE_LASTWRITETIME|AdFileTime|Schreibgeschützt. Gibt eine FILETIME-Struktur, die den Zeitpunkt enthält, den die Ressource des letzten Schreibvorgangs an. Die Uhrzeit wird im UTC-Format. FILETIME-Elemente sind 0 (null), wenn der Anbieter diese Zeitelement nicht unterstützt.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Schreibgeschützt. Gibt die Größe des Ressource-Standard-Streams in Bytes an.|  
|RESOURCE_ISCOLLECTION|AdBoolean|Schreibgeschützt. "True", wenn die Ressource eine Auflistung, z. B. ein Verzeichnis ist. "False", wenn die Ressource eine einfache Datei ist.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|"True", wenn die Ressource ein strukturiertes Dokument ist. "False", wenn die Ressource nicht mit einem strukturierten Dokument ist. Es kann es sich um eine Auflistung oder eine einfache Datei sein.|  
|DEFAULT_DOCUMENT|AdVarWChar|Schreibgeschützt. Gibt an, dass diese Ressource eine URL für das einfache Standarddokument eines Ordners oder eines strukturierten Dokuments enthält. Verwendet, wenn der Standarddatenstrom aus einer Ressource angefordert wird. Diese Eigenschaft ist für eine einfache Datei leer.|  
|CHAPTERED_CHILDREN|AdChapter|Schreibgeschützt. Optional. Gibt an, im Kapitel über das Rowset, das die untergeordneten Elemente der Ressource enthält. (Die *OLE DB-Anbieter für Internet Publishing* diese Spalte nicht verwendet.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Schreibgeschützt. Gibt den Anzeigenamen der Ressource an.|  
|RESOURCE_ISROOT|AdBoolean|Schreibgeschützt. "True", wenn die Ressource der Stamm einer Auflistung oder strukturierte Dokument ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
