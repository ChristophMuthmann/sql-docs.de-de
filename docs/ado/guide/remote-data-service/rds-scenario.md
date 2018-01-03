---
title: RDS-Szenario | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10c9ee41428ab7a43beae2269060618f7d6e296b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="rds-scenario"></a>RDS-Szenario
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Die Adressbuch Anwendung ist ein Szenario, die Ihnen zeigt, wie Remote Data Service (RDS) verwenden, um eine einfache, Daten-aware Webanwendung zu erstellen – ein Buch online Anschrift. Dieses Szenario eignet sich für Microsoft Visual Basic Scripting Edition (VBScript) und COM-Programmierer, die zu erfahren, wie datenbezogene ActiveX-Steuerelemente mit RDS, und für Software von erfahrenen Entwickler möchten datenorientierte Webanwendungen erstellen.  
  
 Dieses Szenario wird davon ausgegangen, dass Sie wissen, wie grundlegende HTML Layouttags, Techniken verwenden DHTML-Datenbindung und Programm mit ActiveX-Steuerelementen verwenden.  
  
 Wenn Sie das SDK installiert haben, kann der vollständigen Quellcode für die beispielanwendung Adressbuch im SDK-Verzeichnis am samples\dataaccess\rds\AddressBook\AddressBook.asp gefunden werden. In Internet Explorer 4.0 oder höher, geben Sie zum Anzeigen des Szenarios Adressbuch  **http://*Webserver*/RDS/AddressBook/AddressBook.asp**, in denen *Webserver* ist der Name zugewiesen zu Ihrem Server Windows NT 4.0 oder Windows 2000-Webserver, auf denen Internet Information Services (IIS) und ASP ausgeführt wird.  
  
## <a name="introduction-to-address-book"></a>Einführung in das Adressbuch  
 Die beispielanwendung Adressbuch bietet ein einfaches online Adressbuch, die mit einem Suchverzeichnis über ein Intranet veröffentlicht werden können. Das Adressbuch ist so konzipiert, dass ein Benutzer eine Suchzeichenfolge in einem oder mehreren Feldern zum Anfordern von Informationen über Mitarbeiter eingeben kann. Wenn Sie die Basisfunktionen von Remote Data Service anzeigen möchten, wird die beispielanwendung absichtlich "klein", mit einer Mindestanzahl von Objekten und Suchfelder beibehalten.  
  
 Die Anwendungsschnittstelle besteht aus den folgenden Teilen:  
  
-   Eine nicht visuelle **RDS. DataControl** Datenbindungsfunktionen-Objekt, das vom Client für die Verbindung mit der Datenbank verwendet wird.  
  
-   HTML-Textfelder, die als Eingabefelder für Mitarbeiter Attribut Suchkriterien fungieren.  
  
-   Befehlsschaltflächen HTML, um Abfragen zu erstellen Suchfelder deaktivieren, Aktualisieren der Datenbank mit Informationen zu Mitarbeitern, ausstehende Änderungen abzubrechen und die Datenzeilen, die im Raster angezeigten navigieren.  
  
-   DHTML-Datenbindung zum Anzeigen von Daten von Abfragen für einen Back-End-Datenbank zurückgegeben (über die **RDS. DataControl** Data Binding-Objekt) in einer Tabelle.  
  
-   VBScript-Routinen, die verbinden Sie alle Elemente, die bereits erwähnt wurden, und ermöglicht es ihnen, zu interagieren. VBScript-Code wird auch zum Initialisieren der **RDS. DataControl** Objekt, und erstellen Sie dynamisch die Spaltenüberschriften in der HTML-Tabelle aus den Namen der der **RDS. DataControl** Recordsetfelder.  
  
 Folgen Sie den Links aus Schritt zum Schritt einrichten, und führen Sie das Szenario, und erfahren, wie das Szenario funktioniert.  
  
 Dieses Szenario umfasst die folgenden Themen.  
  
-   [Systemanforderungen für die Adress Book-Anwendung](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Ausführen des Adress Book-SQL-Skripts](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Ausführen der Adress Book-Beispielanwendung](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Adress Book-Datenbindungsobjekt](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Adress Book-Befehlsschaltflächen](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Adress Book-Navigationsschaltflächen](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Systemanforderungen für die Adresse Book-Anwendung](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [RDS-Grundlagen](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS-Tutorial](../../../ado/guide/remote-data-service/rds-tutorial.md)


