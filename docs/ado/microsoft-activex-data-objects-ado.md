---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3dda017a73829525f94863302156266beac3797f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

ADO ist in C++-Programmen für die Verbindung mit SQL Server verwendet. Natürlich funktioniert auch zur Verbindung mit Azure SQL-Datenbank in der Cloud.

Jeder Abschnitt in diesem Artikel wird beschrieben, eine Komponente von ADO.

> [!NOTE]
> ADO.NET ist anders als ADO. ADO.NET und viele andere SQL-Verbindung-Treiber und deren Sprachen werden erläutert beginnenden [SQL Server-Treiber](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) aktivieren Sie Ihren Clientanwendungen an zugreifen und diese Bearbeiten von Daten aus einer Vielzahl von Quellen über einen OLE DB-Anbieter. Die wichtigsten Vorteile sind einfache verwenden, die hohe Geschwindigkeit, geringer Arbeitsspeicher- und Speicherplatzbedarf. ADO unterstützt die wichtige Funktionen zum Erstellen von Client-Server und webbasierte Anwendungen.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (Multidimensional) (ADO MD) bietet einen einfachen Zugriff auf mehrdimensionale Daten aus Sprachen, z. B. Microsoft Visual Basic und Microsoft Visual C++. ADO MD erweitert Microsoft ActiveX Data Objects (ADO) Objekte spezifisch für mehrdimensionale Daten verwendet, z. B. die CubeDef und Cellset-Objekte. Mit ADO MD können Sie mehrdimensionales Schema durchsuchen, einen Cube Abfragen und Abrufen der Ergebnisse.  
  
 ADO MD verwendet wie ADO einen zugrunde liegenden OLE DB-Anbieter für den Zugriff auf Daten. Um mit ADO MD arbeiten, muss der Anbieter ein multidimensionaler Datenanbieter (MDP) sein, gemäß der Definition von der OLE DB-Spezifikation für OLAP. MDPs Daten in multidimensionalen Sichten im Gegensatz zu tabellarischen Datenanbietern (TDPs) diese Darstellung der Daten in tabellarische Ansichten. Finden Sie in der Dokumentation für den OLAP-OLE DB-Anbieter für ausführlichere Informationen zur spezifischen Syntax und Verhalten von Ihrem Anbieter unterstützt.  
  
## <a name="rds"></a>RDS  
 Remote Data Service (RDS) ist ein Feature von ADO, mit dem Verschieben von Daten von einem Server in einer Clientanwendung oder die Webseite, die Daten auf dem Client und Updates in einem einzigen Roundtrip an den Server zurückgegeben.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX Data Objects Extensions, Data Definition Language und Sicherheit (ADOX) ist eine Erweiterung der ADO-Objekten und das Programmiermodell. ADOX enthält Objekte für Schema-Erstellung und Änderung als auch Sicherheit. Da es sich um ein Objekt basierenden Ansatz zum schemabearbeitung handelt, können Sie Code schreiben, die für verschiedene Datenquellen unabhängig von sortierungsunterschieden in deren systemeigenen Syntax funktioniert.  
  
 ADOX ist eine Begleit-Bibliothek in der wichtigsten Objekte im ADO. Er stellt zusätzliche Objekte zum Erstellen, ändern und Löschen von Schemaobjekten, z. B. Tabellen und Prozeduren bereit. Darüber hinaus Sicherheitsobjekte, um Benutzer und Gruppen verwalten und zu erteilen und Widerrufen von Berechtigungen für Objekte.  
  
## <a name="documentation"></a>Dokumentation  
 [ADO Security Design Issues (Entwurfsaspekte für die ADO-Sicherheit)](../ado/guide/ado-security-design-issues.md)  
  
 [ADO Programmer's Guide (Programmierhandbuch zu ADO)](../ado/guide/ado-programmer-s-guide.md)  
  
 Eine Einführung zur Verwendung von ADO, RDS, ADO MD und ADOX.  
  
 [ADO-Programmierreferenz](../ado/reference/ado-programmer-s-reference.md)  
  
 Dieser Abschnitt der ADO-Dokumentation enthält Themen, die für jede ADO, RDS, ADO MD und ADOX-Objekt, Sammlung, Eigenschaft, dynamische Eigenschaft, Methode, Ereignis, und Enumeration.  
  
 [ADO-Glossar](../ado/ado-glossary.md)  
  
## <a name="support"></a>Support  
 Kostenlos mit ADO Probleme helfen, versuchen Sie es bereitstellen für die öffentliche ADO-Newsgroup. Diese Newsgroup wird überwacht, indem Microsoft Product Support Services (PSS) Supportspezialisten, die ADO abdecken und andere erfahrenen Entwicklern von ADO.  
  
 Weitere Informationen zu Supportoptionen finden Sie auf der Website Microsoft Help und unterstützen.


