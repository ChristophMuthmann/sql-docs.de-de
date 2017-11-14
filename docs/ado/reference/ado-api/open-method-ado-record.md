---
title: Open-Methode (ADO-Datensatz) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7e7f1c5e35ced700818954056b380a44c75570c
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-record"></a>Open-Methode (ADO-Datensatz)
Öffnet ein vorhandenes [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) -Objekt oder erstellt ein neues Element, dargestellt durch die **Datensatz**, z. B. eine Datei oder ein Verzeichnis.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>Parameter  
 *Quelle*  
 Optional. Ein **Variant** , kann die URL der Entität, die von diesem dargestellt werden darstellen **Datensatz** -Objekt, eine **Befehl**, ein offenes [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oder eine andere **Datensatz** -Objekt, das eine Zeichenfolge, die eine SQL SELECT-Anweisung oder einen Tabellennamen enthält.  
  
 *ActiveConnection*  
 Optional. Ein **Variant** , darstellt, der die Verbindungszeichenfolge oder öffnen [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
 *Mode*  
 Optional. Ein [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) Wert, der angibt, den Zugriffsmodus für die resultierenden **Datensatz** Objekt. Standardwert ist **AdModeUnknown**.  
  
 *CreateOptions*  
 Optional. Ein [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md) Wert, der angibt, ob eine vorhandene Datei oder das Verzeichnis geöffnet werden soll, oder eine neue Datei oder ein Verzeichnis erstellt werden soll. Standardwert ist **AdFailIfNotExists**. Wenn auf den Standardwert festgelegt, der Zugriffsmodus aus abgerufen wird die [Modus](../../../ado/reference/ado-api/mode-property-ado.md) Eigenschaft. Dieser Parameter wird ignoriert, wenn die *Quelle* Parameter enthält keine URL.  
  
 *Optionen*  
 Optional. Ein [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md) Wert, der angibt, die Optionen zum Öffnen der **Datensatz**. Standardwert ist **AdOpenRecordUnspecified**. Diese Werte können kombiniert werden.  
  
 *UserName*  
 Optional. Ein **Zeichenfolge** Wert, der die Benutzer-ID, die enthält bei Bedarf, gewährt Zugriff auf *Quelle*.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** Wert, der das Kennwort, die enthält bei Bedarf, überprüft *Benutzername*.  
  
## <a name="remarks"></a>Hinweise  
 *Quelle* werden kann:  
  
-   EINE URL. Wenn das Protokoll für die URL über http ist, wird standardmäßig der Internetanbieter aufgerufen. Wenn die URL zu einem Knoten verweist, der ein ausführbares Skript enthält (z. B. ein. ASP-Seite), eine **Datensatz** , enthält die Quelle, anstelle der ausgeführten Inhalt standardmäßig geöffnet ist. Verwenden der *Optionen* Argument, um dieses Verhalten zu ändern.  
  
-   Ein **Datensatz** Objekt. Ein **Datensatz** -Objekt geöffnet, von einem anderen **Datensatz** wird die ursprüngliche Klonen **Datensatz** Objekt.  
  
-   Ein **Befehl** Objekt. Die geöffnete **Datensatz** Objekt darstellt, die einzelne Zeile zurückgegeben, die durch das Ausführen der **Befehl**. Wenn die Ergebnisse mehr als eine einzelne Zeile enthalten, den Inhalt der ersten Zeile im Datensatz platziert werden und ein Fehler zur hinzugefügt werden, die **Fehler** Auflistung.  
  
-   Eine SQL SELECT-Anweisung. Die geöffnete **Datensatz** Objekt darstellt, die einzelne Zeile, die durch Ausführen der Inhalt der Zeichenfolge zurückgegeben. Wenn die Ergebnisse mehr als eine einzelne Zeile enthalten, den Inhalt der ersten Zeile im Datensatz platziert werden und ein Fehler zur hinzugefügt werden, die **Fehler** Auflistung.  
  
-   Einen Tabellennamen an.  
  
 Wenn die **Datensatz** Objekt stellt eine Entität, die mit einer URL zugegriffen werden kann (z. B. eine Zeile mit einem **Recordset** abgeleitet aus einer Datenbank), die Werte von der [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)-Eigenschaft und das Feld mit Zugriff auf die **AdRecordURL** Konstante null sind.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Das Datensatzobjekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Open-Methode (ADO-Verbindung)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema-Methode](../../../ado/reference/ado-api/openschema-method.md)

