---
title: Open-Methode (ADO-Verbindung) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c61284bb59c01e22ef4f2cb46664fe7d7f7bbd2f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-connection"></a>Open-Methode (ADO-Verbindung)
Öffnet eine Verbindung mit einer Datenquelle.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parameter  
 *"ConnectionString"*  
 Optional. Ein **Zeichenfolge** Wert, der Verbindungsinformationen enthält. Finden Sie unter der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft Weitere Informationen zu gültigen Einstellungen.  
  
 *Benutzer-ID*  
 Optional. Ein **Zeichenfolge** Wert, der einen Benutzernamen ein, verwenden Sie beim Herstellen der Verbindung enthält.  
  
 *Kennwort*  
 Optional. Ein **Zeichenfolge** Wert, der ein Kennwort verwenden, beim Herstellen der Verbindung enthält.  
  
 *Optionen*  
 Optional. Ein [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md) Wert, der bestimmt, ob diese Methode nach dem zurückgeben soll (synchron) oder bevor (asynchron) die Verbindung hergestellt wird.  
  
## <a name="remarks"></a>Hinweise  
 Mithilfe der **öffnen** Methode auf eine [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt stellt die physische Verbindung mit einer Datenquelle her. Nach dem erfolgreichen dieser Methode Abschluss wird die Verbindung live ist, und Sie können gegenüber diesem-Befehle und die Ergebnisse verarbeiten.  
  
 Verwenden Sie das optionale *"ConnectionString"* Argument, um entweder eine Verbindungszeichenfolge mit einer Reihe von anzugeben *Argument* *= Value* Anweisungen, die durch Semikolons getrennt ein, oder ein Datei oder ein Verzeichnis mit einer URL bezeichnete Ressource. Die **"ConnectionString"** -Eigenschaft erbt automatisch den Wert für die *"ConnectionString"* Argument. Aus diesem Grund können Sie entweder die **"ConnectionString"** Eigenschaft von der **Verbindung** Objekt vor dem Öffnen, oder verwenden Sie die *"ConnectionString"* Argument festlegen oder überschreiben die aktuelle Verbindungsparameter während der **öffnen** -Methodenaufruf.  
  
 Wenn Sie Benutzer und Kennwort sowohl Weitergabe von Informationen an die *"ConnectionString"* Argument und der optionalen *UserID* und *Kennwort* Argumente, die *UserID*  und *Kennwort* Argumente werden im angegebenen Werte überschrieben *"ConnectionString"*.  
  
 Wenn Sie Ihre Vorgänge über ein offenes geschlossen haben **Verbindung**, verwenden Sie die [schließen](../../../ado/reference/ado-api/close-method-ado.md) -Methode freizugeben zugeordnete Systemressourcen verfügbar sind. Schließen ein Objekt entfernt diesen nicht aus dem Arbeitsspeicher; Sie können die eigenschafteneinstellungen ändern und die **öffnen** Methode, um sie später erneut öffnen. Um ein Objekt aus dem Arbeitsspeicher vollständig zu vermeiden, legen Sie die Objektvariable auf *nichts*.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Verbindung** -Objekt, das **öffnen** Methode nicht tatsächlich stellen eine Verbindung mit dem Server, bis eine [Recordset ](../../../ado/reference/ado-api/recordset-object-ado.md) wird geöffnet, auf die **Verbindung** Objekt.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Beispiel für Eröffnungs- und Methoden (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Öffnen Sie und schließen Sie die Methoden-Beispiel (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Öffnen Sie und schließen Sie die Methoden (VC++-Beispiel)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open-Methode (ADO-Datensatz)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open-Methode (ADO-Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open-Methode (ADO-Datenstrom)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema-Methode](../../../ado/reference/ado-api/openschema-method.md)

