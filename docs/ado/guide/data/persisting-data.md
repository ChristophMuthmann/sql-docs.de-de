---
title: Beibehalten von Daten | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9862fc9f45674d3995b857eec222d8f560870a6
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-data"></a>Beibehalten von Daten
Tragbare Computer (z. B. mit Laptops) hat die Notwendigkeit von Anwendungen generiert, die in einem verbundenen und nicht verbundenen Zustand ausgeführt werden kann. ADO hat Unterstützung für diese hinzugefügt, durch die Vergabe des Entwicklers der Möglichkeit zum Speichern eines Clientcursors **Recordset** auf den Datenträger, und Laden Sie es später erneut.  
  
 Es gibt mehrere Szenarien, in denen Sie diese Art von Funktion, einschließlich der folgenden verwenden:  
  
-   **Wegstrecke:** bei die Anwendung unterwegs geschaltet wurde, ist es ausschlaggebend, geben Sie die Möglichkeit, um Änderungen vorzunehmen, und fügen Sie neue Datensätze, die später auf die Datenbank wiederhergestellt und ein Commit ausgeführt werden können.  
  
-   **Suchvorgänge selten aktualisiert:** häufig in einer Anwendung Tabellen als Suchvorgänge verwendet werden – z. B. Steuertabellen. Sie werden selten aktualisiert und sind schreibgeschützt. Anstelle einer dieser Daten vom Server bei jedem der Anwendung Start, die Anwendung kann einfach Laden von Daten aus einer lokal persistenten **Recordset**.  
  
 In ADO, zum Speichern und Laden von **Recordsets**, verwenden Sie die **Recordset.Save** und **Recordset.Open(,,,adCmdFile)** Methoden für das ADO **Recordset**Objekt.  
  
 Können Sie die **Recordset speichern** Methode zum Beibehalten von Ihrem ADO **Recordset** in eine Datei auf einem Datenträger. (Sie können auch Speichern einer **Recordset** ein ADO **Stream** Objekt. **Streamen** Objekte werden weiter unten in der Anleitung.) Später können Sie die **öffnen** Methode zum erneuten Öffnen der **Recordset** Wenn Sie bereit sind, verwenden sie. Standardmäßig speichert ADO die **Recordset** in proprietären Format von Microsoft Advanced Data TableGram (ADTG). Diese Binärformat wird angegeben, mit der **AdPersistADTG PersistFormatEnum** Wert. Alternativ können Sie auch zum Speichern Ihrer **Recordset** Out als XML verwenden stattdessen **AdPersistXML**. Weitere Informationen zum Speichern von Recordsets im XML-Format finden Sie unter [beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 Die Syntax der **speichern** Methode lautet wie folgt:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 Beim ersten Sie speichern die **Recordset**, ist er optional an *Ziel*. Wenn Sie weglassen *Ziel*, erstellt eine neue Datei mit einem Namen, legen Sie auf den Wert des der [Quelle](../../../ado/reference/ado-api/source-property-ado-recordset.md) Eigenschaft von der **Recordset**.  
  
 Weglassen *Ziel* beim anschließend aufrufen **speichern** nach der ersten Speichern "oder" ein Laufzeitfehler auftritt. Wenn anschließend Sie rufen **speichern** mit einem neuen *Ziel*, die **Recordset** in das neue Ziel gespeichert wird. Allerdings wird das neue Ziel des ursprünglichen Zieles beide geöffnet werden.  
  
 **Speichern** schließt nicht die **Recordset** oder *Ziel*, damit Sie fortfahren können, mit der **Recordset** und die neuesten Änderungen zu speichern. *Ziel* bleibt geöffnet, bis die **Recordset** geschlossen wird, während dieses Zeitraums andere Anwendungen lesen können, aber nicht hineinschreiben *Ziel*.  
  
 Aus Gründen der Sicherheit die **speichern** Methode erlaubt nur die Verwendung von Sicherheit niedrig und benutzerdefinierte Einstellungen aus einem Skript, das von Microsoft Internet Explorer ausgeführt.  
  
 Wenn die **speichern** Methode wird aufgerufen, während eines asynchronen **Recordset** abzurufen, ausführen oder Aktualisieren der Vorgang wird ausgeführt, **speichern** wartet, bis der asynchrone Vorgang ist abgeschlossen Sie werden.  
  
 Datensätze gespeichert werden, beginnend mit der ersten Zeile der **Recordset**. Wenn die **speichern** Methode abgeschlossen ist, wird die aktuelle Zeilenposition in der ersten Zeile der verschoben der **Recordset**.  
  
 Legen Sie für optimale Ergebnisse die [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) Eigenschaft **AdUseClient** mit **speichern**. Wenn Ihr Anbieter nicht alle Funktionen, die zum Speichern erforderlichen unterstützt **Recordset** Objekte aufweist, der Cursor-Dienst stellt diese Funktionalität bereit.  
  
 Wenn eine **Recordset** wird beibehalten, mit der **CursorLocation** -Eigenschaftensatz auf **AdUseServer**, die Update-Funktion für die **Recordset**ist beschränkt. In der Regel nur einzelne Tabelle Updates, einfügungen und löschungen (abhängig von Anbieterfunktionen) zulässig sind. Die [Resync](../../../ado/reference/ado-api/resync-method.md) Methode ist auch in dieser Konfiguration nicht verfügbar.  
  
 Da die *Ziel* Parameter akzeptiert jedes Objekt, das die OLE DB unterstützt **IStream** -Schnittstelle, die Sie speichern eine **Recordset** direkt an die ASP  **Antwort** Objekt.  
  
 Im folgenden Beispiel die **speichern** und **öffnen** Methoden zum Beibehalten einer **Recordset** und es später erneut öffnen:  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Hinweise  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Weitere Informationen zum Recordset Persistenz](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Beibehalten von gefiltert und hierarchische Recordsets](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)

