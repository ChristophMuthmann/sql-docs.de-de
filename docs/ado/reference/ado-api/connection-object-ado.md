---
title: Verbindungsobjekt (ADO) | Microsoft Docs
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
- Connection
helpviewer_keywords:
- Connection object [ADO]
ms.assetid: ef6b1824-5b12-43db-89d7-8f3d13896d4d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7beb64b0620b1a5b603c02cb36904e3a42f5b3f7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="connection-object-ado"></a>Verbindungsobjekt (ADO)
Stellt eine offene Verbindung mit einer Datenquelle dar.  
  
## <a name="remarks"></a>Hinweise  
 Ein **Verbindung** -Objekt stellt eine eindeutige Sitzung mit einer Datenquelle dar. In einem Client/Server-Datenbanksystem kann es entspricht eine tatsächliche Netzwerk-Verbindung mit dem Server sein. Abhängig von den Funktionen, die vom Anbieter, einige Auflistungen, Methoden oder Eigenschaften des unterstützt eine **Verbindung** Objekt möglicherweise nicht zur Verfügung.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Verbindung** -Objekts können Sie folgende Möglichkeiten:  
  
-   Konfigurieren Sie die Verbindung vor dem Öffnen mit der ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md), [ConnectionTimeout](../../../ado/reference/ado-api/connectiontimeout-property-ado.md), und [Modus](../../../ado/reference/ado-api/mode-property-ado.md) Eigenschaften. **"ConnectionString"** ist die Standardeigenschaft eines der **Verbindung** Objekt.  
  
-   Legen Sie die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft an Client zum Aufrufen der [Microsoft Cursor Service für OLE DB-](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md), welche unterstützt Batchaktualisierungen.  
  
-   Legen Sie die Standarddatenbank für die Verbindung mit der [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) Eigenschaft.  
  
-   Gruppe, die das Maß an Isolation für die Transaktionen geöffnet wird, für die Verbindung mit der [IsolationLevel](../../../ado/reference/ado-api/isolationlevel-property.md) Eigenschaft.  
  
-   Geben Sie einen OLE DB-Anbieter mit der [Anbieter](../../../ado/reference/ado-api/provider-property-ado.md) Eigenschaft.  
  
-   Herstellen und später zu unterbrechen, die physische Verbindung mit der Datenquelle mit dem [öffnen](../../../ado/reference/ado-api/open-method-ado-connection.md) und [schließen](../../../ado/reference/ado-api/close-method-ado.md) Methoden.  
  
-   Führen Sie einen Befehl für die Verbindung mit der [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) Methode und konfigurieren Sie die Ausführung mit der [CommandTimeout](../../../ado/reference/ado-api/commandtimeout-property-ado.md) Eigenschaft.  
  
    > [!NOTE]
    >  Übergeben Sie eine Abfragezeichenfolge enthält, die zum Ausführen einer Abfrage, ohne ein Command-Objekt, das **Execute** Methode eine **Verbindung** Objekt. Allerdings eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt ist erforderlich, wenn den Befehlstext beibehalten und erneut ausgeführt wird, oder verwenden Sie Abfrageparameter werden sollen.  
  
-   Verwalten von Transaktionen auf die offene Verbindung, einschließlich geschachtelter Transaktionen aus, wenn der Anbieter unterstützt werden, mit der [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md), und [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) Methoden und die [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md) Eigenschaft.  
  
-   Untersuchen Sie Fehler, die zurückgegeben werden, aus der Datenquelle mit dem [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung.  
  
-   Lesen die Version von der ADO-Implementierung verwendet, mit der [Version](../../../ado/reference/ado-api/version-property-ado.md) Eigenschaft.  
  
-   Abrufen von Schemainformationen über die Datenbank mit der [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) Methode.  
  
 Sie können erstellen **Verbindung** Objekte unabhängig von der zuvor definierten Objekten.  
  
 Sie können benannte Befehle oder gespeicherte Prozeduren ausführen, als wären sie systemeigenen Methoden auf einen **Verbindung** -Objekts, wie im nächsten Abschnitt gezeigt. Wenn Sie den gleichen Namen wie ein einer gespeicherten Prozedur über einen benannten Befehl verfügt, rufen Sie "systemeigenen Aufruf der Methode" auf einem **Verbindung** Objekt immer den genannte Befehl anstelle der gespeicherten Prozedur ausgeführt.  
  
> [!NOTE]
>  Diese Funktion nicht verwenden (einen benannten Befehl oder gespeicherte Prozedur aufrufen, als wäre er einer nativen Methode auf die **Verbindung** Objekt) in einer Microsoft® .NET Framework-Anwendung, da die zugrunde liegende Implementierung der Funktion Konflikte ist das mit der Funktionsweise der .NET Framework mit COM.  
  
## <a name="execute-a-command-as-a-native-method-of-a-connection-object"></a>Ausführen eines Befehls als systemeigene Methode eines Verbindungsobjekts  
 Benennen Sie zum Ausführen eines Befehls dem Befehl mit der **Befehl** Objekt [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft. Legen Sie die **ActiveConnection** Eigenschaft von der **Befehl** Objekt, das die Verbindung. Geben Sie eine Anweisung, in dem Namen des Befehls verwendet wird, als wäre er eine Methode auf, die **Verbindung** Objekts, gefolgt von beliebigen Parametern und einem **Recordset** Objekt, wenn keine Zeilen zurückgegeben werden. Legen Sie die **Recordset** Eigenschaften zum Anpassen der resultierende **Recordset**. Beispiel:  
  
```  
Dim cnn As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
...  
cnn.Open "..."  
cmd.Name = "yourCommandName"  
cmd.ActiveConnection = cnn  
...  
'Your command name, any parameters, and an optional Recordset.  
cnn. "parameter", rst  
```  
  
## <a name="execute-a-stored-procedure-as-a-native-method-of-a-connection-object"></a>Ausführen einer gespeicherten Prozedur als systemeigene Methode eines Verbindungsobjekts  
 Geben Sie zum Ausführen einer gespeicherten Prozedur eine Anweisung aus, in dem Namen der gespeicherten Prozedur verwendet wird, als wäre er eine Methode auf, die **Verbindung** Objekts, gefolgt von beliebigen Parametern. ADO stellen eine "Schätzung" der Parametertypen. Beispiel:  
  
```  
Dim cnn As New ADODB.Connection  
...  
'Your stored procedure name and any parameters.  
cnn. "parameter"  
```  
  
 Die **Verbindung** Objekt für die Skripterstellung sicher ist.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Verbindungs-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Errors-Auflistung (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Properties-Auflistung (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Anhang A: Daten und Dienstanbieter](../../../ado/guide/appendixes/appendix-a-providers.md)
