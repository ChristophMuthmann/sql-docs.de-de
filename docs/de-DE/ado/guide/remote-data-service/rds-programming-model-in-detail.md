---
title: RDS-Programmiermodell detailliert | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1bb1d8aef9f96a2e0ecabcd6c4ee6771452f3ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="rds-programming-model-in-detail"></a>RDS-Programmiermodell im Detail
Im folgenden sind wichtige Elemente, die RDS-Programmiermodell:  
  
-   RDS.DataSpace  
  
-   RDSServer.DataFactory  
  
-   RDS.DataControl  
  
-   Ereignis  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS.DataSpace  
 Ihre Clientanwendung muss den Server und des aufzurufenden Programms angeben. Die Anwendung wird im Gegenzug empfängt einen Verweis auf die Server-Anwendung und kann den Verweis behandeln, als handele es sich um die Server-Anwendung selbst.  
  
 Die RDS-Objektmodell stellt diese Funktionalität mit dem [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) Objekt.  
  
 Ein Programmbezeichner des Programms angegeben wird oder *ProgID*. Der Server verwendet die *ProgID* und dem Servercomputer Registrierung so suchen Informationen über das Programm tatsächlich zu initiieren.  
  
 RDS wird unterschieden intern je nachdem, ob die Server-Anwendung auf einem Remoteserver über das Internet oder Intranet; ein Server in einem lokalen Netzwerk; oder nicht auf einem Server alle sondern auf einer lokalen Dynamic Link Library (DLL). Diese Unterscheidung bestimmt, wie Informationen zwischen dem Client und dem Server ausgetauscht wird, ist entscheidend dafür konkrete der Typ des Verweises an die Clientanwendung zurückgegeben. Allerdings hat diese Unterscheidung aus der Sicht keine besondere Bedeutung. Wichtig ist, dass Sie einen Programmverweis für nutzbare erhalten.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS bietet ein Standardserverprogramm, die entweder eine SQL-Abfrage für die Datenquelle und Rückgabe ausführen kann ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt oder Ausführen einer **Recordset** Objekt und aktualisiert die Datenquelle.  
  
 Die RDS-Objektmodell stellt diese Funktionalität mit dem [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt.  
  
 Darüber hinaus weist diesem Objekt eine Methode zum Erstellen einer leeres **Recordset** -Objekt, das programmgesteuert gefüllt werden kann ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)), und eine andere Methode zum Konvertieren einer **Recordset**  Objekt in eine Zeichenfolge zum Erstellen einer Webseite ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Mit ADO, können Sie einige der standard-Verbindung und Befehlsverhalten von überschreiben die **RDSServer.DataFactory** mit eine **DataFactory** Befehl Handler und eine Anpassungsdatei, die Verbindung enthält. und Sicherheitsparametern.  
  
 Die Server-Anwendung bezeichnet eine *Geschäftsobjekt*. Sie können eigene benutzerdefinierte Geschäftsobjekt schreiben, das komplexe Daten zugreifen, Gültigkeit überprüft usw. ausführen können. Auch wenn Sie ein benutzerdefiniertes Geschäftsobjekt zu schreiben, erstellen Sie eine Instanz von einer **RDSServer.DataFactory** -Objekts und die Verwendung einiger ihrer Methoden für Ihre eigenen Aufgaben.  
  
## <a name="rdsdatacontrol"></a>RDS.DataControl  
 RDS bietet die Möglichkeit, die Funktionalität Kombinieren der **RDS. DataSpace** und **RDSServer.DataFactory**, und aktivieren Sie visuelle Steuerelemente auf einfache Weise verwendet auch die **Recordset** Objekt, das von einer Abfrage aus einer Datenquelle zurückgegeben. RDS versucht der häufigste Fall ist, möchten Sie so weit wie möglich automatisch Zugriff auf Informationen auf einem Server und in einem visuellen Steuerelement anzeigt.  
  
 Die RDS-Objektmodell stellt diese Funktionalität mit dem [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt.  
  
 Die **RDS. DataControl** hat zwei Aspekte. Ein Aspekt bezieht sich auf die Datenquelle. Wenn Sie festlegen, dass der Befehl und die Verbindung mit der **verbinden** und **SQL** Eigenschaften der **RDS. DataControl**, er verwendet automatisch die **RDS. DataSpace** , erstellen Sie einen Verweis auf den Standardwert **RDSServer.DataFactory** Objekt. Die **RDSServer.DataFactory** verwendet die **verbinden** Eigenschaftswert zum Herstellen einer Verbindung mit der Datenquelle die **SQL** Eigenschaftswert Abrufen einer  **Recordset** aus der Datenquelle und der Rückgabewert der **Recordset** -Objekt an die **RDS. DataControl**.  
  
 Der zweite Aspekt bezieht sich auf die Anzeige der zurückgegebenen **Recordset** Informationen in einem visuellen Steuerelement. Sie können ein visuelles Steuerelement mit Zuordnen der **RDS. DataControl** (in einem Prozess, der als Bindung bezeichnet wird) und den Zugriff auf die Informationen in der zugeordneten **Recordset** -Objekt, das Anzeigen von Abfrageergebnissen auf einer Webseite in Microsoft® Internet Explorer. Jede **RDS. DataControl** Objekts bindet einen **Recordset** Objekt, das die Ergebnisse einer einzelnen Abfrage für eine oder mehrere visual-Steuerelemente (z. B. ein Textfeld, Kombinationsfeld, Rastersteuerelement usw.) darstellt. Es kann nicht mehr als eine **RDS. DataControl** Objekt auf jeder Seite. Jede **RDS. DataControl** Objekt kann mit einer anderen Datenquelle verbunden und enthalten die Ergebnisse einer separaten Abfrage.  
  
 Die **RDS. DataControl** -Objekt verfügt außerdem über einen eigenen Methoden zum Navigieren, Sortieren und Filtern der Zeilen des zugehörigen **Recordset** Objekt. Diese Methoden ähneln sich, aber nicht identisch mit den Methoden für das ADO **Recordset** Objekt.  
  
## <a name="events"></a>Ereignisse  
 RDS unterstützt zwei seine eigenen Ereignisse, die das ADO-Ereignismodell unabhängig sind. Die ["onreadystatechange"](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) Ereignis wird aufgerufen, wenn die **RDS. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) eigenschaftsänderungen, daher benachrichtigt werden, wenn ein asynchroner Vorgang erfolgreich abgeschlossen wurde, beendet oder ist ein Fehler aufgetreten. Die [OnError](../../../ado/reference/rds-api/onerror-event-rds.md) Ereignis wird aufgerufen, wenn ein Fehler auftritt, selbst wenn der Fehler während eines asynchronen Vorgangs auftritt.  
  
> [!NOTE]
>  Microsoft Internet Explorer werden zwei zusätzliche Ereignisse an RDS: **OnDataSetChanged**, gibt an, dass die **Recordset** ist voll funktionsfähiges und zugleich noch Abrufen von Zeilen, und  **OnDataSetComplete**, gibt an, dass die **Recordset** wurde das Abrufen von Zeilen.  
  
## <a name="see-also"></a>Siehe auch  
 [RDS-Programmiermodell mit Objekten](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace-Objekt (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS-Szenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Verwendung und Sicherheit von RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



