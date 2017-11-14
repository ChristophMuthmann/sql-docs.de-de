---
title: "Adresse Buch Befehlsschaltflächen | Microsoft Docs"
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
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 31b0bb389b188c39b4590a774ac453a9de17fd56
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="address-book-command-buttons"></a>Behandeln von Buch Befehlsschaltflächen
Die Adressbuch-Anwendung enthält die folgenden Schaltflächen:  
  
-   Ein **suchen** Schaltfläche, um eine Abfrage mit der Datenbank zu übermitteln.  
  
-   Ein **deaktivieren** Schaltfläche, um Textfelder zu deaktivieren, bevor Sie eine neue Suche zu starten.  
  
-   Ein **Profil aktualisieren** Schaltfläche, um Änderungen in einem Mitarbeiterdatensatz zu speichern.  
  
-   Ein **Änderungen Abbrechen** Schaltfläche, um die Änderungen zu verwerfen.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Schaltfläche "Suchen"  
 Klicken auf die **suchen** Schaltfläche aktiviert das VBScript Find_OnClick Sub-Prozedur, die erstellt und sendet die SQL-Abfrage. Auf diese Schaltfläche klicken, wird das Datenraster aufgefüllt.  
  
## <a name="building-the-sql-query"></a>Erstellen die SQL-Abfrage  
 Der erste Teil der Find_OnClick Sub-Prozedur erstellt die SQL-Abfrage, einem Ausdruck zu einem Zeitpunkt durch Anfügen von Textzeichenfolgen zu einer globalen SQL SELECT-Anweisung. Zunächst wird die Variable `myQuery` auf eine SQL SELECT-Anweisung, die alle Zeilen mit Daten aus der Tabelle der Datenquelle anfordert. Als Nächstes überprüft der Unterprozedur jede der vier Eingabefelder auf der Seite.  
  
 Da das Programm das Wort verwendet `like` bei der Erstellung der SQL-Anweisungen, die Abfragen sind Suchmethode statt genaue Übereinstimmungen.  
  
 Z. B. wenn die **Nachname** Feld enthalten den Eintrag "Berge" und die **Titel** Feld enthalten den Eintrag "Program Manager", die SQL-Anweisung (Wert des `myQuery`) würde folgendermaßen lauten:  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Wenn die Abfrage erfolgreich war, werden alle Personen, die einen Nachnamen enthalten, die mit dem Text "Berge" (z. B. Berge und Berger) und mit einem Titel, die die Wörter "Program Manager" (z. B. Programmmanager, erweiterter Technologien) im HTML-Raster angezeigt.  
  
## <a name="preparing-and-sending-the-query"></a>Vorbereiten und senden die Abfrage  
 Der letzte Teil der Find_OnClick Sub-Prozedur besteht aus zwei Anweisungen. Die erste Anweisung weist die [SQL](../../../ado/reference/rds-api/sql-property.md) Eigenschaft von der [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekt gleich dem dynamisch erstellte SQL-Abfrage. Die zweite Anweisung bewirkt, dass die **RDS. DataControl** Objekt (`DC1`) auf die Datenbank abzufragen, und klicken Sie dann die neuen Ergebnisse der Abfrage im Raster anzuzeigen.  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Profil-Schaltfläche "Aktualisieren"  
 Klicken auf die **Profil aktualisieren** Schaltfläche aktiviert das VBScript Update_OnClick Sub-Prozedur, die ausgeführt wird die [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) des Objekts (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) und [aktualisieren](../../../ado/reference/rds-api/refresh-method-rds.md) Methoden.  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Wenn `DC1.SubmitChanges` ausgeführt wird, Remote Data Service verpackt die Updateinformationen und sendet sie an den Server über HTTP. Das Update ist nichts; Wenn ein Teil der Aktualisierung nicht erfolgreich ist, wird keine der Änderungen vorgenommen, und eine Statusmeldung wird zurückgegeben. `DC1.Refresh`ist nicht erforderlich, nach dem **SubmitChanges** mit Remote Data Service, aber es wird sichergestellt, dass neue Daten.  
  
## <a name="cancel-changes-button"></a>Änderungen-Schaltfläche "Abbrechen"  
 Auf **Änderungen Abbrechen** aktiviert die VBScript Cancel_OnClick Sub-Prozedur, die ausführt der [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) des Objekts (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) Methode.  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Wenn `DC1.CancelUpdate` ausgeführt wird, werden alle Änderungen, die ein Benutzer an einem Mitarbeiterdatensatz auf das Datenraster seit der letzten Abfrage oder Aktualisierung vorgenommen wurde verworfen. Die ursprünglichen Werte werden wiederhergestellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Behandeln von Buch Navigationsschaltflächen](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)



