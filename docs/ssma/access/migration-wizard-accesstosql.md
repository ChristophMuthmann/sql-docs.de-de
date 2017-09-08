---
title: Migrations-Assistent (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e6b2024b8ba34bd4f71abc6030ae86dcc03faebd
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="migration-wizard-accesstosql"></a>Migrations-Assistent (AccessToSQL)
Der Migrations-Assistent führt Sie durch die Migration von einer oder mehreren Datenbanken aus Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Mithilfe des Assistenten zum Erstellen eines Projekts, fügen Sie Datenbanken auf das Projekt, wählen Sie Objekte zu migrieren, und Verbinden mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie werden auch konvertieren, laden und Migrieren von Access-Schemas und Daten. Optional können Sie den Zugriff auf Tabellen zu verknüpfen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen.  
  
Die meisten Seiten Migrations-Assistenten enthalten die gleichen Optionen wie vorhandene SSMA-Dialogfelder. Aus diesem Grund die Seiten des Assistenten werden hier beschrieben, und klicken Sie dann Links bereitgestellt werden, sodass Sie mehr zu den einzelnen Optionen erfahren. Wenn eine Seite eindeutige Optionen enthält, werden sie hier dokumentiert.  
  
## <a name="starting-the-migration-wizard"></a>Starten Sie den Paketmigrations-Assistent  
Standardmäßig wird der Migrations-Assistent angezeigt, starten Sie SSMA. Sie können den Assistenten auch starten, auf die **Datei** Menü dazu **Paketmigrations-Assistent**.  
  
## <a name="welcome-page"></a>Willkommensseite  
Die Seite "Willkommen" führt den Migrations-Assistenten und bietet die folgende Option zum Starten des Assistenten.  
  
**Starten Sie die Assistenten bei Systemstart.**  
Standardmäßig wird SSMA der Migrations-Assistent gestartet, starten Sie SSMA. Um den automatischen Start des Assistenten zu verhindern, deaktivieren Sie dieses Kontrollkästchen.  
  
## <a name="create-new-project-page"></a>Erstellen Sie die Seite "Neues Projekt"  
Die Seite "Neues Projekt erstellen" ist, in dem Sie die Datei Name, Speicherort und Migration Projekt Projekttyp (die Version des Ziels für die Migration verwendete SQL Server) eingeben. Weitere Informationen finden Sie unter [neues Projekt (SSMA)](http://msdn.microsoft.com/en-us/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Access-Datenbanken hinzufügen  
Die Seite "Access-Datenbanken hinzufügen" ist, in dem Sie eine oder mehrere Access-Datenbanken zum Projekt hinzufügen. Sie können einzelne Datenbanken hinzufügen, indem Sie auf **Datenbanken hinzufügen**, und wählen Sie dann auf die Datenbanken aus der **öffnen** Fenster. Oder suchen Sie Datenbanken mithilfe der **Datenbanken suchen** Schaltfläche. Weitere Informationen finden Sie in folgenden Themen:  
  
-   [Hinzufügen und Entfernen von Access-Datenbankdateien](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [Datenbanken-Assistent (Wählen Sie Speicherorte) suchen](http://msdn.microsoft.com/en-us/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Datenbanken-Assistent (Select-Dateien) suchen](http://msdn.microsoft.com/en-us/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Suchen von Datenbanken (Auswahl überprüfen)](http://msdn.microsoft.com/en-us/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Wählen Sie Objekte auf der Seite zu migrieren  
Die Objekte wählen Sie auf der Seite des Clustermigrations-wählen Sie die Objekte zu konvertieren. Sie können alle Objekte, Gruppen von Objekten oder einzelne Objekte auswählen.  
  
**Objekte auswählen**  
  
1.  Erweitern Sie **Zugriff Metabasis**, und erweitern Sie dann **Datenbanken**.  
  
2.  Führen Sie eine oder mehrere der folgenden:  
  
    -   Um alle Datenbanken zu konvertieren, aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Datenbanken, wählen Sie aus, oder deaktivieren Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zum konvertieren, oder lassen Sie Abfragen, erweitern Sie die Datenbank, und aktivieren bzw. Deaktivieren der **Abfragen** Kontrollkästchen.  
  
    -   Zum konvertieren, oder lassen Sie einzelne Tabellen, erweitern Sie die Datenbank und **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
Wenn Sie viele Objekte haben, sollten Sie verwenden die **Objektauswahl erweiterte** -Datenbankobjekte auf Optionen im rechten Bereich, um Zugriff zu filtern. Wenn Sie auswählen, z. B. **Tabellen** im linken Bereich können Sie dann die Liste der Tabellen durch Eingeben von Zeichenfolgen in Filtern die **Filter** Feld. Sie können dann aktivieren oder deaktivieren die gefilterte Tabellen für die Migration, mithilfe der Schaltflächen am oberen Rand des Bereichs.  
  
Weitere Informationen zum Filtern finden Sie unter "Optionen" des [Objektauswahl erweiterte (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Herstellen einer Verbindung mit SQL Server-Seite  
Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Seite, Sie geben Sie die Verbindungseigenschaften, und verbinden Sie dann mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server](http://msdn.microsoft.com/en-us/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> Sobald die Verbindung erfolgreich ist, treten **Linktabellen** Seite, in dem Sie eine Option zum Verknüpfen der Tabellen haben. Klicken Sie auf **Weiter** und die Migration startet.  
  
## <a name="connect-to-sql-azure-page"></a>Herstellen einer Verbindung mit SQL Azure-Seite  
Auf der Seite Connect to SQL Azure Geben Sie die Verbindungseigenschaften, und dann eine Verbindung zu SQL Azure herstellen. Um einen neuen Azure-Datenbank zu erstellen, können Sie dies mit tun **Azure-Datenbank erstellen** Optionen, die auf einem Klick auf angezeigt **Durchsuchen** Schaltfläche. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Azure](http://msdn.microsoft.com/en-us/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> Sobald die Verbindung erfolgreich ist, treten **Linktabellen** Seite, in dem Sie eine Option zum Verknüpfen der Tabellen haben. Klicken Sie auf **Weiter** Schaltfläche auf der Seite "Verknüpfungen", um die Migration zu starten.  
  
## <a name="link-tables-page"></a>Link-Seite "Tabellen"  
Die Seite "Tabellen verknüpfen" können Sie die Verknüpfen der ursprünglichen Access-Tabellen mit den migrierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen. Verknüpfen von Tabellen die Access-Datenbank ändert, sodass Ihre Abfragen, Formulare, Berichte und Datenzugriffsseiten die Daten im Verwenden der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank nicht die Daten in der Access-Datenbank.  
  
**Verknüpfungstabellen**  
Wählen Sie die **verknüpfen Sie Tabellen** Kontrollkästchen, um den Zugriff auf Tabellen mit den migrierten verknüpfen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Tabellen. Um die Migration zu starten, klicken Sie auf **Weiter** Schaltfläche.  
  
## <a name="migration-status-page"></a>Status-Seite-Migration  
Die Migrations-Statusseite wird der Fortschritt der Schemata Zugriff zu konvertieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Schemas, laden die konvertierte Schemas in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und klicken Sie dann die Daten migriert.  
  
Weitere Informationen zu dieser Seite finden Sie unter [konvertieren, laden und migrieren](http://msdn.microsoft.com/en-us/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit SQL Server Migration Assistant für Access &#40; AccessToSQL &#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Benutzer-Schnittstelle Reference(Access)](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  

