---
title: RDS-Lernprogramm | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO]
ms.assetid: 6e3305a0-7bc7-40d1-9122-235c15d23ab2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6cfb12781ca9e7387ea8016de581217ddf95f9c1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="rds-tutorial"></a>RDS-Lernprogramm
Dieses Lernprogramm veranschaulicht das Verwenden der RDS-Programmiermodell zum Abfragen und Aktualisieren einer Datenquelle. Zunächst wird hier beschrieben, die zur Ausführung dieser Aufgabe erforderlichen Schritte. Das Lernprogramm wird dann in Microsoft® Visual Basic Scripting Edition (mit ADO für Windows Foundation Classes (ADO/WFC)) wiederholt.  
  
 In diesem Lernprogramm wird aus zwei Gründen in verschiedenen Sprachen codiert:  
  
-   Die Dokumentation für RDS setzt den Reader-Codes in Visual Basic. Dadurch wird die Dokumentation für Visual Basic-Programmierer praktisch, aber weniger nützlich für Programmierer, die andere Sprachen verwenden.  
  
-   Wenn Sie eine bestimmte Funktion von RDS unsicher sind, und Sie, etwas wissen von einer anderen Sprache können Sie möglicherweise auf Ihre Frage zu beheben, indem Sie die Suche nach der gleichen Funktion in einer anderen Sprache ausgedrückt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="how-the-tutorial-is-presented"></a>Die Darstellung des Lernprogramms  
 Dieses Lernprogramm basiert auf dem RDS-Programmiermodell. Es wird jedes Schritts das Programmiermodell einzeln erläutert. Darüber hinaus veranschaulicht er jeden Schritt mit einem Visual Basic-Code-Fragment.  
  
 Im Codebeispiel wird in anderen Sprachen mit minimalen Diskussion wiederholt. Jeder Schritt in einem Lernprogramm einer bestimmten Sprache wird mit dem entsprechenden Schritt im Programmiermodell und beschreibenden Lernprogramm markiert. Verwenden Sie die Nummer des Schritts zur Diskussion im Lernprogramm beschreibenden verweisen.  
  
 Die RDS-Programmiermodell wird im folgenden Abschnitt angegeben. Verwenden Sie es als eine Übersicht über die, wie Sie das Lernprogramm ausführen.  
  
## <a name="rds-programming-model-with-objects"></a>RDS-Programmiermodell mit Objekten  
  
-   Geben Sie das Programm, auf dem Server aufgerufen werden soll, und rufen Sie eine Möglichkeit (Proxy) vom Client darauf verweisen.  
  
-   Rufen Sie die Server-Anwendung. Übergeben Sie Parameter an die Server-Anwendung, die die Datenquelle und den Befehl zum Ausstellen identifiziert.  
  
-   Die Server-Anwendung erhält einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt aus der Datenquelle, in der Regel mithilfe von ADO. Optional, die **Recordset** Objekt auf dem Server verarbeitet wird.  
  
-   Des Programms gibt den endgültigen **Recordset** Objekt an die Clientanwendung.  
  
-   Auf dem Client die **Recordset** optional versetzen Objekts in ein Formular, das einfach durch visuelle Steuerelemente verwendet werden kann.  
  
-   Änderungen an der **Recordset** Objekt an den Server gesendet und zum Aktualisieren der Datenquelle verwendet werden.  
  
 Dieses Lernprogramm enthält die folgenden Themen.  
  
-   [Schritt 1: Serverprogramm angeben (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)  
  
-   [Schritt 2: Serverprogramm aufrufen (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)  
  
-   [Schritt 3: Server erhält ein Recordset (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)  
  
-   [Schritt 4: Server gibt das Recordset zurück (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)  
  
-   [Schritt 5: DataControl wird nutzbar gemacht (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)  
  
-   [Schritt 6: Änderungen werden an den Server gesendet (RDS-Tutorial)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)  
  
-   [RDS-Tutorial (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Schritt 1: Geben Sie ein Serverprogramm (RDS-Lernprogramm)](../../../ado/guide/remote-data-service/step-1-specify-a-server-program-rds-tutorial.md)   
 [RDS-Tutorial (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

