---
title: ActiveConnection-Eigenschaft (ADO) | Microsoft Docs
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
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords: ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9722834bb3a5edb7abdb1ecf7b0235a069d60f09
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="activeconnection-property-ado"></a>ActiveConnection-Eigenschaft (ADO)
Gibt an, zu dem [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt das angegebene [Befehl](../../../ado/reference/ado-api/command-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), oder [Datensatz](../../../ado/reference/ado-api/record-object-ado.md) Objekt derzeit gehört.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert, der eine Definition für eine Verbindung enthält, wenn die Verbindung geschlossen wird, bzw. einen **Variant** , enthält die aktuelle **Verbindung** Objekt, wenn die Verbindung ist geöffnet. Standardwert ist ein null-Objekt-Verweis. Finden Sie unter der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **ActiveConnection** -Eigenschaft zum Bestimmen der **Verbindung** Objekt über den angegebenen **Befehl** Objekt ausgeführt wird oder das angegebene  **Recordset** wird geöffnet.  
  
## <a name="command"></a>Befehl  
 Für **Befehl** Objekte, die **ActiveConnection** Eigenschaft gilt Lese-/Schreibzugriff.  
  
 Wenn Sie versuchen, rufen Sie die [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode auf eine **Befehl** Objekt vor dem Festlegen dieser Eigenschaft auf ein offenes **Verbindung** Objekt oder eine gültige Verbindungszeichenfolge, ein Fehler auftritt.  
  
 Wenn eine **Verbindung** Objekt zugewiesen ist die **ActiveConnection** -Eigenschaft, das Objekt muss geöffnet sein. Zuweisen einer geschlossenen Verbindungsobjekt verursacht einen Fehler.  
  
### <a name="note"></a>Hinweis  
 **Microsoft Visual Basic** Einstellung der **ActiveConnection** Eigenschaft *nichts* hebt die Zuordnung der **Befehl** Objekt aus dem aktuellen **Verbindung** und bewirkt, dass den Anbieter für die Datenquelle zugehörigen Ressourcen freizugeben. Verknüpfen Sie dann die **Befehl** Objekt mit der gleichen oder einem anderen **Verbindung** Objekt. Einige Anbieter ermöglichen es Ihnen, ändern Sie die Einstellung der Eigenschaft von einem **Verbindung** in eine andere, ohne zuerst die Eigenschaft auf festgelegt *nichts*.  
  
 Wenn die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung von der **Befehl** Objekt enthält Parameter, die vom Anbieter bereitgestellten, die Auflistung wird gelöscht, wenn Sie festlegen, die **ActiveConnection** Eigenschaft, um *nichts* oder einem anderen **Verbindung** Objekt. Wenn Sie manuell erstellen [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekte und verwenden sie zum Füllen der **Parameter** Auflistung von der **Befehl** Objekt, und legen die **ActiveConnection**  Eigenschaft *nichts* oder einem anderen **Verbindung** -Objekt bewirkt, dass die **Parameter** Auflistung intakt.  
  
 Schließen der **Verbindung** Objekt, mit dem eine **Befehl** Objekt wird verknüpft legt die **ActiveConnection** Eigenschaft *nichts*. Wenn diese Eigenschaft auf ein geschlossenes **Verbindung** Objekt wird ein Fehler generiert.  
  
## <a name="recordset"></a>Recordset  
 Für offene **Recordset** Objekte oder für **Recordset** -Objekte, deren [Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md) Eigenschaftensatz wird eine gültige **Befehl** -Objekt, das **ActiveConnection** Eigenschaft ist schreibgeschützt. Andernfalls ist er Lese-/Schreibzugriff.  
  
 Legen Sie diese Eigenschaft auf einen gültigen **Verbindung** Objekt oder eine gültige Verbindungszeichenfolge. In diesem Fall erstellt der Anbieter eine neue **Verbindung** -Objekt unter Verwendung dieser Definition und öffnet die Verbindung. Darüber hinaus kann der Anbieter diese Eigenschaft festlegen, mit dem neuen **Verbindung** Objekt bieten eine Möglichkeit zum Zugriff auf die **Verbindung** -Objekt für erweiterte Fehlerinformationen oder andere Befehle ausführen.  
  
 Bei Verwendung von der *ActiveConnection* Argument der [öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md) Methode zum Öffnen einer **Recordset** -Objekt, der **ActiveConnection** Eigenschaft wird Übernehmen Sie den Wert des Arguments.  
  
 Wenn Sie festlegen der **Quelle** Eigenschaft der **Recordset** Objekt auf eine gültige **Befehl** Object-Variablen, die **ActiveConnection** Eigenschaft die **Recordset** erbt von der Einstellung der **Befehl** des Objekts **ActiveConnection** Eigenschaft.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Recordset** -Objekt, diese Eigenschaft kann nur für eine Verbindungszeichenfolge oder (in Microsoft Visual Basic oder Visual Basic Scripting Edition) festgelegt werden *nichts* .  
  
## <a name="record"></a>Aufzeichnung (Record)  
 Diese Eigenschaft ist für Lese-/Schreibzugriff bei der **Datensatz** Objekt ist geschlossen, und enthalten möglicherweise eine Verbindungszeichenfolge oder der Verweis auf ein offenes **Verbindung** Objekt. Diese Eigenschaft ist schreibgeschützt sind und wenn die **Datensatz** Objekt geöffnet ist, und enthält einen Verweis auf ein offenes **Verbindung** Objekt.  
  
 Ein **Verbindung** Objekt wird implizit erstellt, wenn die **Datensatz** Objekt über eine URL geöffnet wird. Öffnen Sie die **Datensatz** öffnen Sie mit einem vorhandenen **Verbindung** Objekt durch Zuweisen der **Verbindung** -Objekts auf diese Eigenschaft oder mithilfe der **Verbindung** Objekt als Parameter in der [öffnen](../../../ado/reference/ado-api/open-method-ado-record.md) -Methodenaufruf. Wenn die **Datensatz** wird geöffnet, aus einer vorhandenen **Datensatz** oder [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), ist es automatisch zugeordnet **Datensatz** oder  **Recordset** des Objekts **Verbindung** Objekt.  
  
> [!NOTE]
>  URLs, die mit dem HTTP-Schema werden automatisch aufgerufen. der [Microsoft OLE DB-Anbieter für Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Weitere Informationen finden Sie unter [absoluten und relativen URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Gilt für  
  
||||  
|-|-|-|  
|[Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Record-Objekt (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Richtung Eigenschaften (VC++-Beispiel)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText CommandTimeout, Befehlstyp (CommandType), Größe und Eigenschaften Beispiel für die Richtung (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString-Eigenschaft (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
