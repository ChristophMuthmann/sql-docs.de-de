---
title: Command-Objekt (ADO) | Microsoft Docs
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
- Command
helpviewer_keywords:
- Command object [ADO]
ms.assetid: a02c22fb-542d-465e-a629-30fd59dcbebf
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 863c922dce68f5e3108136baf90ebc5a3d0b697a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="command-object-ado"></a>Command-Objekt (ADO)
Definiert einen bestimmten Befehl, den Sie für eine Datenquelle ausführen möchten.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden einer **Befehl** Objekt um eine Datenbank abzufragen und Zurückgeben von Datensätzen in einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt, um einen Massenvorgang ausführen oder die Struktur einer Datenbank zu bearbeiten. Abhängig von den Funktionen des Anbieters, einige **Befehl** Auflistungen, Methoden oder Eigenschaften möglicherweise einen Fehler generieren, wenn auf sie verwiesen werden.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Befehl** -Objekts können Sie folgende Möglichkeiten:  
  
-   Definieren Sie die ausführbare Datei Text des Befehls (z. B. eine SQL-Anweisung) mit der [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft. Alternativ können Sie für Befehl oder Abfrage außer einfachen Strukturen Zeichenfolgen (z. B. XML-Vorlageabfragen) definieren, den Befehl mit der [CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md) Eigenschaft.  
  
-   Optional, Angeben der Befehlsdialekt verwendet der **CommandText** oder **CommandStream** mit der [Dialekt](../../../ado/reference/ado-api/dialect-property.md) Eigenschaft.  
  
-   Definieren Sie parametrisierte Abfragen oder gespeicherten Prozedur Argumente mit [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekte und die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung.  
  
-   Gibt an, ob Parameternamen an den Anbieter übergeben werden sollen die [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) Eigenschaft.  
  
-   Ausführen ein Befehls und zum Zurückgeben einer **Recordset** Objekt bei Bedarf mit der [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode.  
  
-   Geben Sie den Befehl mit der [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) Eigenschaft vor der Ausführung, um die Leistung zu optimieren.  
  
-   Steuern, ob der Anbieter eine vorbereitete (oder kompilierte) Version des Befehls vor der Ausführung mit speichert die [Prepared](../../../ado/reference/ado-api/prepared-property-ado.md) Eigenschaft.  
  
-   Legen Sie die Anzahl der Sekunden, die ein Anbieter für einen Befehl zum Ausführen von mit wartet der [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) Eigenschaft.  
  
-   Ordnen Sie eine offene Verbindung mit einer **Befehl** Objekt durch Festlegen seiner [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) Eigenschaft.  
  
-   Legen Sie die [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft zum Identifizieren der **Befehl** als Methode für das zugeordnete Objekt [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt.  
  
-   Übergeben einer **Befehl** -Objekt an die [Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md) Eigenschaft eine **Recordset** zum Abrufen von Daten.  
  
-   Zugreifen auf anbieterspezifische Attribute mit den [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
> [!NOTE]
>  Zum Ausführen einer Abfrage ohne Verwendung einer **Befehl** Objekt, und übergeben Sie eine Abfragezeichenfolge enthält, die die [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) Methode eine **Verbindung** Objekt oder auf die [Öffnen](../../../ado/reference/ado-api/open-method-ado-recordset.md)Methode von einer **Recordset** Objekt. Allerdings eine **Befehl** Objekt ist erforderlich, wenn den Befehlstext beibehalten und erneut ausgeführt wird, oder verwenden Sie Abfrageparameter werden sollen.  
  
 Zum Erstellen einer **Befehl** Objekt unabhängig von einem zuvor definierten **Verbindung** -Objekt, legen Sie seine **ActiveConnection** Eigenschaft, um eine gültige Verbindungszeichenfolge. ADO erstellt dennoch ein **Verbindung** -Objekt, aber sie weist keinen dieses Objekt zu einer Object-Variablen. Jedoch wenn Sie mehrere zuordnen **Befehl** Objekte mit derselben Verbindung, sollten Sie explizit erstellen und öffnen Sie eine **Verbindung** Objekt; dieser weist den **Verbindung** Objekt, das eine Objektvariable. Stellen Sie sicher, dass die **Verbindung** Objekt wurde erfolgreich geöffnet, bevor Sie sie zum Zuweisen der **ActiveConnection** Eigenschaft von der **Befehl** Objekt, da zuweisen eine geschlossen **Verbindung** Objekt verursacht einen Fehler. Wenn Sie nicht Festlegen der **ActiveConnection** Eigenschaft von der **Befehl** -Objekt an diese Objektvariable ADO erstellt ein neues **Verbindung** -Objekt für jedes ** Befehl** -Objekt, auch wenn Sie dieselbe Verbindungszeichenfolge verwenden.  
  
 Zum Ausführen einer **Befehl**, rufen sie seine [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft auf dem zugeordneten **Verbindung** Objekt. Die **Befehl** benötigen ihre **ActiveConnection** -Eigenschaftensatz auf die **Verbindung** Objekt. Wenn die **Befehl** verfügt über Parameter, deren Werte als Argumente an die Methode übergeben.  
  
 Wenn zwei oder mehr **Befehl** Objekte ausgeführt werden, auf die gleiche Verbindung und entweder **Befehl** Objekt ist eine gespeicherte Prozedur mit Output-Parameter ein Fehler auftritt. Jede auszuführende **Befehl** -Objekt, separate Verbindungen verwenden, oder trennen Sie alle anderen **Befehl** Objekte aus der Verbindung.  
  
 Die **Parameter** Auflistung ist das Standardelement der **Befehl** Objekt. Dies hat zur Folge, dass der Code für die folgenden beiden Anweisungen äquivalent.  
  
```  
objCmd.Parameters.Item(0)  
objCmd(0)  
```  
  
-   Die **Befehl** Objekt ist nicht sicher für Skripting.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Befehl-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/command-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Verbindungsobjekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md)

