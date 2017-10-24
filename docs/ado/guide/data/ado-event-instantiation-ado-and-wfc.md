---
title: 'ADO-Ereignis-Instanziierung: ADO und WFC | Microsoft Docs'
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4d46ec3bdad80879ddc4a931d8668a5298972e58
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO-Ereignis-Instanziierung: ADO- und WFC
ADO für Windows Foundation Classes (ADO/WFC) baut auf das ADO-Ereignismodell und stellt eine vereinfachte Application programming Interface. Im allgemeinen ADO/WFC fängt ADO Ereignisse konsolidiert die Ereignisparameter in einer einzelnen Ereignisklasse und ruft dann den Ereignishandler.  
  
### <a name="to-use-ado-events-in-adowfc"></a>ADO-Ereignisse in ADO/WFC verwenden  
  
1.  Definieren Sie einen eigenen Ereignishandler, um ein Ereignis zu verarbeiten. Beispielsweise mussten Sie zum Verarbeiten der **ConnectComplete** Ereignis in der **ConnectionEvent** Familie ist Sie möglicherweise verwenden Sie diesen Code:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Definieren Sie ein Handler, das den Ereignishandler darstellt. Das Handlerobjekt muss der Datentyp **ConnectEventHandler** für ein Ereignis vom Typ **ConnectionEvent**, oder ein Datentyp **RecordsetEventHandler** für ein Ereignis vom Typ ** RecordsetEvent**. Z. B. den folgenden code für Ihre **ConnectComplete** Ereignishandler:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     Das erste Argument der **ConnectionEventHandler** Konstruktor ist ein Verweis auf die Klasse, die den Ereignishandler mit dem Namen in das zweite Argument enthält.  
  
3.  Fügen Sie einen Ereignishandler auf eine Liste der Handler vorgesehen, um eine bestimmte Art von Ereignis zu verarbeiten. Verwenden Sie die Methode mit einem Namen, z. B. **AddOn***EventName*(*Handler*).  
  
4.  ADO/WFC implementiert intern die ADO-Ereignishandler. Aus diesem Grund, ein Ereignis ausgelöst wurde, indem eine **Verbindung** oder **Recordset** Vorgang von einem ADO/WFC-Ereignishandler abgefangen wird.  
  
     Der ADO/WFC-Ereignishandler übergibt ADO **ConnectionEvent** Parameter in einer Instanz von der ADO/WFC **ConnectionEvent** Klasse oder ADO **RecordsetEvent** Parameter in einer Instanz von der ADO/WFC **RecordsetEvent** Klasse. Diese ADO/WFC-Klassen konsolidieren die ADO-Ereignisparameter; d. h., jede ADO/WFC-Klasse enthält einen Datenmember für jeden eindeutigen Parameter in allen ADO **ConnectionEvent** oder **RecordsetEvent** Methoden.  
  
5.  ADO/WFC ruft dann den Ereignishandler mit dem ADO/WFC-Ereignis-Objekt. Angenommen, Ihre **OnConnectComplete** Ereignishandler hat eine Signatur wie folgt:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     Das erste Argument ist der Typ des Objekts, das das Ereignis gesendet ([Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) oder [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)), und das zweite Argument ist das ADO/WFC-Ereignisobjekt (**ConnectionEvent** oder **RecordsetEvent**).  
  
     Die Signatur der Ereignishandler ist einfacher als ein ADO-Ereignis. Allerdings müssen Sie dennoch kennen das ADO-Ereignismodell wissen, welche Parameter für ein Ereignis gelten und wie reagiert.  
  
6.  Zurückgeben von Ihrem Ereignishandler an den ADO/WFC-Handler für das ADO-Ereignis. ADO/WFC kopiert relevante ADO/WFC-Ereignis-Datenmember zurück an den ADO-Ereignisparameter, und klicken Sie dann der ADO-Ereignishandler zurückgegeben.  
  
7.  Wenn Sie fertig sind verarbeiten, entfernen Sie den Handler aus der Liste der ADO/WFC-Ereignishandler. Verwenden Sie die Methode mit einem Namen, z. B. **RemoveOn***EventName*(*Handler*).  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignis-Handler-Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - WFC Syntaxindex](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Ereignisparameter](../../../ado/guide/data/event-parameters.md)   
 [Zusammenwirken der Ereignishandler](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Typen von Ereignissen](../../../ado/guide/data/types-of-events.md)

