---
title: ConnectionString-Eigenschaft (ADO) | Microsoft Docs
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
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34db69d25ff835de4f8c81d252c99017ae4acbb5
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connectionstring-property-ado"></a>ConnectionString-Eigenschaft (ADO)
Gibt an, die Informationen zum Herstellen einer Verbindung mit einer Datenquelle verwendet.  
  
## <a name="settings-and-return-values"></a>Einstellungen und Rückgabewerte  
 Legt fest oder gibt einen **Zeichenfolge** Wert.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **"ConnectionString"** Eigenschaft, um eine Datenquelle zu geben, indem Sie eine detaillierte Verbindungszeichenfolge mit einer Reihe von *Argument* *= Value* Anweisungen durch getrennt ein Semikolon.  
  
 ADO unterstützt fünf Argumente für die **"ConnectionString"** Eigenschaft; alle anderen Argumente übergeben direkt an den Anbieter ohne Verarbeitung von ADO. Die Argumente ADO unterstützt lauten wie folgt aus.  
  
|Argument|Description|  
|--------------|-----------------|  
|*Provider =*|Gibt den Namen eines Anbieters für die Verbindung verwenden.|  
|*Dateiname =*|Gibt den Namen einer anbieterspezifischen-Datei (z. B. eine persistente Datenquellenobjekt), die voreingestellte Verbindungsinformationen enthält.|  
|*Remoteanbieter =*|Gibt den Namen eines Anbieters beim Öffnen einer clientseitigen Verbindung verwenden. (Nur remote Data Service.)|  
|*Remoteserver =*|Gibt den Pfadnamen des Servers, der beim Öffnen einer clientseitigen Verbindung verwenden. (Nur remote Data Service.)|  
|*URL =*|Gibt die Verbindungszeichenfolge als eine absolute URL identifiziert eine Ressource, z. B. eine Datei oder ein Verzeichnis an.|  
  
 Nach dem Festlegen der **"ConnectionString"** -Eigenschaft, und Öffnen der [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) -Objekt, den Anbieter möglicherweise zu ändern den Inhalt der Eigenschaft, z. B. durch Zuordnen von ADO definierten Argumentnamen auf ihre Entsprechung für den bestimmten Anbieter.  
  
 Die **"ConnectionString"** -Eigenschaft erbt automatisch den Wert für die *"ConnectionString"* Argument der [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) Methode, sodass Sie die aktuelle überschreibenkönnen** "ConnectionString"** Eigenschaft während der **öffnen** -Methodenaufruf.  
  
 Da die *Dateiname* Argument bewirkt, dass ADO zugeordneten Anbieter zu laden, kann nicht übergeben werden, sowohl die *Anbieter* und *Dateiname* Argumente.  
  
 Die **"ConnectionString"** Eigenschaft ist Lese-/Schreibzugriff auf, wenn die Verbindung ist geschlossen und Read-only, wenn er geöffnet ist.  
  
 Duplikate eines Arguments in den **"ConnectionString"** Eigenschaft werden ignoriert. Die letzte Instanz von einem Argument wird verwendet.  
  
> [!NOTE]
>  **Remote Datendienstnutzung** bei Verwendung für eine clientseitige **Verbindung** -Objekt, das **"ConnectionString"** Eigenschaft enthalten kann, nur die *Remoteanbieter*und *Remoteserver* Parameter.  
  
 Die folgende Tabelle enthält die Standard-ADO-Anbieter für jedes Windows-Betriebssystem:  
  
|Standard-ADO-Anbieter|Windows-Betriebssystem|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Um die Lesbarkeit des Quellcodes zu verbessern, explizit angeben der Name des Anbieters in der Verbindungszeichenfolge angegeben.)|Windows 2000 (32-Bit)<br /><br /> Windows XP (32-Bit)<br /><br /> Windows Server 2003 (32-Bit)<br /><br /> Windows Vista (32-Bit)<br /><br /> Windows Vista Service Pack 1 oder höher (32 Bit und 64-Bit)<br /><br /> Windows-Versionen nach Windows Vista (32-Bit und 64-Bit)|  
|Keinen Standardwert.<br /><br /> Wenn eine ADO-Anwendung auf die folgenden Betriebssysteme ausgeführt wird und den Anbieter nicht explizit angegeben, ADO folgender Fehler zurückgegeben: "ADODB. Verbindung: Anbieter nicht angegeben ist und es ist keine festgelegten Standardanbieter "|Windows 2000 (64-Bit)<br /><br /> Windows XP (64-Bit)<br /><br /> WindowsServer 2003 (64-Bit)<br /><br /> Windows Vista (64-Bit)|  
  
## <a name="applies-to"></a>Gilt für  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 ["ConnectionString" ConnectionTimeout und State-Eigenschaft (Beispiel) (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 ["ConnectionString" ConnectionTimeout und State-Eigenschaft (VC++-Beispiel)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md)

