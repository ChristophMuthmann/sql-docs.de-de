---
title: ActiveConnection-Eigenschaft (ADO MD) | Microsoft Docs
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
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae0ad910a0535599d7e134d3314030537068ab25
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection-Eigenschaft (ADO MD)
Gibt an, welche ADO [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt das aktuellen Cellset oder Katalog derzeit gehört.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Variant** , enthält eine Zeichenfolge, die eine Verbindung oder **Verbindung** Objekt. Die Standardeinstellung ist leer.  
  
## <a name="remarks"></a>Hinweise  
 Sie können diese Eigenschaft festlegen, um eine gültige ADO **Verbindung** Objekt oder eine gültige Verbindungszeichenfolge. Wenn diese Eigenschaft auf eine Verbindungszeichenfolge festgelegt ist, erstellt der Anbieter einen neuen **Verbindung** -Objekt unter Verwendung dieser Definition und öffnet die Verbindung.  
  
 Bei Verwendung von der *ActiveConnection* Argument der [öffnen](../../../ado/reference/ado-md-api/open-method-ado-md.md) Methode zum Öffnen einer [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) -Objekt, der **ActiveConnection** Eigenschaft wird Übernehmen Sie den Wert des Arguments.  
  
 Festlegen der **ActiveConnection** Eigenschaft eine [Katalog](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) -Objekt **nichts** frei von der zugehörigen Daten, einschließlich Daten in die [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) Auflistung und allen verknüpften [Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [Hierarchie](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md), und [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte. Schließen einer **Verbindung** -Objekt, das verwendet wurde, öffnen eine **Katalog** hat dieselbe Wirkung wie das Festlegen der **ActiveConnection** Eigenschaft **nichts**.  
  
 Ändern die Standarddatenbank für die Verbindung verweist die **ActiveConnection** Eigenschaft eine **Katalog** Objekt erklärt den Inhalt der **Katalog**.  
  
 Es wird eine Fehlermeldung angezeigt, wenn Sie versuchen, Sie ändern die **ActiveConnection** Eigenschaft für eine offene **Cellset** Objekt.  
  
> [!NOTE]
>  In Visual Basic, denken Sie daran, verwenden Sie die **festgelegt** Schlüsselwort beim Festlegen der **ActiveConnection** Eigenschaft, um eine **Verbindung** Objekt. Wenn Sie weglassen der **festgelegt** -Schlüsselwort, Sie tatsächlich Festlegen der **ActiveConnection** Eigenschaft gleich der **Verbindung** Standardeigenschaft des Objekts, ** "ConnectionString"**. Der Code funktioniert. Sie werden jedoch eine zusätzliche Verbindung zu der Datenquelle erstellen, die negativ auf die Leistung auswirken kann.  
  
 Wenn Sie den MSOLAP-Datenanbieter verwenden, legen Sie die Datenquelle in einer Verbindungszeichenfolge auf einen Servernamen und Anfangskatalog auf den Namen des Katalogs aus der Datenquelle festgelegt. Zur Verbindung mit einer Cubedatei, die von einem Server getrennt ist, legen Sie den Speicherort auf den vollständigen Pfad zu der. CUB-Datei. In beiden Fällen wird den Anbieter auf den Anbieternamen festgelegt. Die folgende Zeichenfolge verwendet beispielsweise den MSOLAP-Anbieter für die Verbindung mit einem Katalog mit dem Namen Bobs Video Store auf einem Server mit dem Namen **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 Die folgende Zeichenfolge eine Verbindung mit einer lokalen Cubedatei an der Position C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub her:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>Gilt für  
  
|||  
|-|-|  
|[Katalogobjekt (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Cellset-Objekt (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Cellset-Beispiel (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open-Methode (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)

