---
title: Open-Methode (ADO-Datenstrom) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b104e04c81fce3fce5cb25d175602f1b339e9ac1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="open-method-ado-stream"></a>Open-Methode (ADO-Datenstrom)
Öffnet eine [Stream](../../../ado/reference/ado-api/stream-object-ado.md) Objekt Datenströme Binär oder Text zu bearbeiten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Variant** Wert, der angibt, die Quelle der Daten für die **Stream**. *Quelle* darf eine absolute URL-Zeichenfolge, die auf einen vorhandenen Knoten in einer bekannten Baumstruktur, z. B. eine e-Mail- oder Dateisystem verweist. Sollte eine URL mithilfe des URL-Schlüsselworts angegeben werden ("URL =*Schema*://*Server*/*Ordner*"). Alternativ können Sie *Quelle* möglicherweise enthalten einen Verweis auf ein bereits geöffnetes [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) -Objekt, das die zugeordneten Standarddatenstrom öffnet die **Datensatz**. Wenn *Quelle* nicht angegeben wird, eine **Stream** instanziiert und geöffnet, keine zugrunde liegenden Quelle standardmäßig zugeordnet ist. Weitere Informationen zu URL-Schemas und zugeordneten Anbietern finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Mode*  
 Optional. Ein [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) Wert, der angibt, den Zugriffsmodus für die resultierenden **Stream** (z. B. Lese-/Schreibzugriff oder schreibgeschützt). Standardwert ist **AdModeUnknown**. Finden Sie unter der [Modus](../../../ado/reference/ado-api/mode-property-ado.md) -Eigenschaft für Weitere Informationen zu Access-Modi. Wenn *Modus* nicht angegeben ist, wird es von dem Quellobjekt geerbt. Beispielsweise, wenn die Quelle **Datensatz** im Nur-Lese Modus geöffnet wird die **Stream** wird standardmäßig auch im schreibgeschützten Modus geöffnet werden.  
  
 *OpenOptions*  
 Optional. Ein [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) Wert. Standardwert ist **AdOpenStreamUnspecified**.  
  
 *UserName*  
 Optional. Ein **Zeichenfolge** Wert, der die Benutzer-IDs, die enthält, wenn es benötigt wird, greift auf, die **Stream** Objekt.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** Wert, der das Kennwort, die enthält, wenn es benötigt wird, greift auf, die **Stream** Objekt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine **Datensatz** Objekt wird als der Quellparameter übergeben der *UserID* und *Kennwort* Parameter werden nicht verwendet werden, da der Zugriff auf die **Datensatz** Objekt bereits verfügbar ist. Auf ähnliche Weise die [Modus](../../../ado/reference/ado-api/mode-property-ado.md) von der **Datensatz** Objekt wird zum Übertragen der **Stream** Objekt. Wenn *Quelle* nicht angegeben wird, die **Stream** geöffnet keine Daten enthält, und verfügt über eine [Größe](../../../ado/reference/ado-api/size-property-ado-stream.md) null (0). Um zu vermeiden, Verlust von Daten, die in diese geschrieben werden **Stream** bei der **Stream** ist "geschlossen", speichern die **Stream** mit der [' CopyTo ' für](../../../ado/reference/ado-api/copyto-method-ado.md) oder [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) Methoden, oder an einen anderen Speicherort zu speichern.  
  
 Ein *OpenOptions* Wert **AdOpenStreamFromRecord** identifiziert den Inhalt des der *Quelle* Parameter bereits geöffnet sein **Datensatz**Objekt. Das Standardverhalten besteht, behandeln *Quelle* als eine URL, die direkt mit einem Knoten in einer Baumstruktur, z. B. eine Datei verweist. Der diesem Knoten zugeordnete Standarddatenstrom wird geöffnet.  
  
 Während der **Stream** ist nicht geöffnet ist, ist es möglich, alle schreibgeschützten Eigenschaften des Lesen der **Stream**. Wenn eine **Stream** wird asynchron ausgeführt wird, alle nachfolgenden Vorgänge geöffnet (außer Überprüfen der [Status](../../../ado/reference/ado-api/state-property-ado.md) und andere Eigenschaften schreibgeschützt) werden blockiert, bis die **öffnen** Vorgang ist abgeschlossen.  
  
 Zusätzlich zu den Optionen, die oben besprochen wurden, indem angegeben *Quelle*, können Sie eine Instanz des erstellen eine **Stream** Objekt im Arbeitsspeicher ohne Zuordnung zu einer zugrunde liegenden Datenquelle. Sie können Daten in den Stream dynamisch hinzufügen, durch Schreiben von Binär oder Text-Daten auf den **Stream** mit [schreiben](../../../ado/reference/ado-api/write-method.md) oder [WriteText](../../../ado/reference/ado-api/writetext-method.md), oder Laden von Daten aus einer Datei mit [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Stream-Objekt (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO-Datensatz)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema-Methode](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile-Methode](../../../ado/reference/ado-api/savetofile-method.md)
