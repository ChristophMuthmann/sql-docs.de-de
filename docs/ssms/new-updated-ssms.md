---
title: "Aktualisiert: Dokumentation zu SSMS für SQL Server | Microsoft-Dokumentation"
description: "Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation zu SQL Server Management Studio (SSMS) für Microsoft SQL Server"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: de-de
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Neu und kürzlich aktualisiert: SQL Server Management Studio (SSMS) für SQL Server



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich der Updates*: &nbsp; **18.7.2017** &nbsp; bis &nbsp; **11.9.2017**
- *Themenbereich:* &nbsp; **SQL Server Management Studio (SSMS)**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu neuen Artikeln weiter, die kürzlich erstellt wurden.


1. [Das Ausgabefenster in SQL Server Management Studio](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu allen aktualisierten Artikeln, die im Abschnitt mit Auszügen aufgeführt sind.

1. [Herunterladen von SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [Herstellen einer Verbindung mit einer SQL Server- oder Azure SQL-Datenbank](#TitleNum_2)
3. [SQL Server Management Studio – Änderungsprotokoll (SSMS)](#TitleNum_3)
4. [Erstellen und Aktualisieren von Datenbanktabellen](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [Herunterladen von SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Aktualisiert: 07.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



SSMS 17.2 ist die neueste Version von SQL Server Management Studio. Die Generation 17.X von SSMS bietet Support für beinahe alle Featurebereiche unter SQL Server 2008 bis SQL Server 2017. Version 17.X unterstützt auch SQL Analysis Service-PaaS.

Version 17.2 enthält Folgendes:

- Multi-Factor Authentication (MFA)
  - Azure AD-Authentifizierung für mehrere Benutzer für eine universelle Authentifizierung mit Multi-Factor Authentication (UA mit MFA)
  - Ein neues Eingabefeld für Benutzeranmeldeinformationen wurde der universellen Authentifizierung mit MFA hinzugefügt, um die Authentifizierung für mehrere Benutzer zu unterstützen.
- Das Dialogfeld „Verbindung“ unterstützt nun die folgenden fünf Authentifizierungsmethoden:
  - Windows-Authentifizierung
  - SQL Server-Authentifizierung
  - Active Directory: Universell mit MFA-Unterstützung
  - Active Directory: Kennwort
  - Active Directory: Integriert

- Der Assistent für Datenbankimport und -export für DacFx kann nun die universelle Authentifizierung mit MFA verwenden.
- Informationen zur API-Unterstützung finden Sie unter [IUniversalAuthProvider-Schnittstelle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Die von ADAL verwaltete Bibliothek, die von der universellen Authentifizierung mit MFA in Azure AD verwendet wird, wurde auf Version 3.13.9 aktualisiert.
- Eine neue CLI-Schnittstelle, die Azure AD-Administratoreinstellungen für SQL Datenbank und SQL Data Warehouse unterstützt.

 Weitere Informationen zu den Authentifizierungsmethoden in Active Directory finden Sie unter [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA) (Universelle Authentifizierung mit SQL-Datenbank und SQL Data Warehouse (SSMS-Unterstützung für MFA))](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) und [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio (Konfigurieren der mehrstufigen Authentifizierung in Azure SQL-Datenbank für SQL Server Management Studio)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- Das Ausgabefenster enthält Einträge für Abfragen, die während der Erweiterung der Objekt-Explorer-Knoten ausgeführt wurden
- Aktivierter Sicht-Designer für Azure SQL-Datenbanken
- Die Standardoptionen für die Skripterstellung für Skripterstellungsobjekte aus dem Objekt-Explorer in SSMS haben sich geändert:



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2. &nbsp; [Herstellen einer Verbindung mit einer SQL Server- oder Azure SQL-Datenbank](object/connect-to-an-instance-from-object-explorer.md)

*Aktualisiert: 25.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_1) | [Weiter](#TitleNum_3))

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![Firewall--../media/connect-to-server/new-firewall-rule.png)

1. Um eine Firewallregel zu erstellen und eine Verbindung zum Server herzustellen, klicken Sie auf **OK**.

1. Nach der Verbindungsherstellung wird der Server im **Objekt-Explorer** angezeigt:

   ![Verbunden--../media/connect-to-server/connected.png)

**Nächste Schritte**


[Entwerfen, Erstellen und Aktualisieren von Tabellen--../visual-db-tools/design-tables-visual-database-tools.md)

**Siehe auch**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [Herunterladen von SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3. &nbsp; [SQL Server Management Studio – Änderungsprotokoll (SSMS)](sql-server-management-studio-changelog-ssms.md)

*Aktualisiert: 07.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_2) | [Weiter](#TitleNum_4))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



Dieser Artikel enthält Details zu Updates, Verbesserungen und Fehlerbehebungen für die aktuellen und früheren Versionen von SSMS. Laden Sie [unten SSMS-Vorgängerversionen herunter--#previous-ssms-releases).

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


Allgemein verfügbar | Buildnummer: 14.0.17177.0

**Erweiterungen**


- Multi-Factor Authentication (MFA)
  - Azure AD-Authentifizierung für mehrere Benutzer für eine universelle Authentifizierung mit Multi-Factor Authentication (UA mit MFA)
  - Ein neues Eingabefeld für Benutzeranmeldeinformationen wurde der universellen Authentifizierung mit MFA hinzugefügt, um die Authentifizierung für mehrere Benutzer zu unterstützen.
- Das Dialogfeld „Verbindung“ unterstützt nun die folgenden fünf Authentifizierungsmethoden:
  - Windows-Authentifizierung
  - SQL Server-Authentifizierung
  - Active Directory: Universell mit MFA-Unterstützung
  - Active Directory: Kennwort
  - Active Directory: Integriert

- Verwenden der universellen Authentifizierung mit MFA durch den Assistenten für Datenbankimport und -export für DacFx.
- Informationen zur API-Unterstützung finden Sie unter [IUniversalAuthProvider-Schnittstelle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx).
- Die von ADAL verwaltete Bibliothek, die von der universellen Authentifizierung mit MFA in Azure AD verwendet wird, wurde auf Version 3.13.9 aktualisiert.
- Zusätzlich wurde eine neue CLI-Schnittstelle erstellt, die Azure AD-Administratoreinstellungen für SQL Datenbank und SQL Data Warehouse unterstützt.

 Weitere Informationen zu den Authentifizierungsmethoden in Active Directory finden Sie unter [Universal Authentication with SQL Database and SQL Data Warehouse (SSMS support for MFA) (Universelle Authentifizierung mit SQL-Datenbank und SQL Data Warehouse (SSMS-Unterstützung für MFA))](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) und [Configure Azure SQL Database multi-factor authentication for SQL Server Management Studio (Konfigurieren der mehrstufigen Authentifizierung in Azure SQL-Datenbank für SQL Server Management Studio)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- Das Ausgabefenster enthält Einträge für Abfragen, die während der Erweiterung der Objekt-Explorer-Knoten ausgeführt wurden



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4. &nbsp; [Erstellen und Aktualisieren von Datenbanktabellen](visual-db-tools/design-tables-visual-database-tools.md)

*Aktualisiert: 25.08.2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Zurück](#TitleNum_3))

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**Erstellen einer Tabelle**


1. Klicken Sie mit der rechten Maustaste in der Datenbank auf den Knoten **Tabellen**, und klicken Sie auf **Neu** > **Tabelle**:

    ![Neue Tabelle--../media/design-tables/new-table.png)

1. Fügen Sie Ihrer Tabelle [Spalten--column-properties-visual-database-tools.md) hinzu:

    ![Entwurfstabelle--../media/design-tables/new-table2.png)

1. Schließen Sie den Designer, und speichern Sie die Änderungen.

**Aktualisieren einer Tabelle**


1. Klicken Sie mit der rechten Maustaste auf die Tabelle unter dem Knoten **Tabellen** Ihrer Datenbank, und klicken Sie auf **Entwerfen**:

   ![Aktualisieren einer Tabelle--../media/design-tables/update-table.png)

1. Aktualisieren Sie die gewünschten Tabelleneinstellungen:

   ![--../media/design-tables/update-table2.png)

1. Schließen Sie den Designer, und speichern Sie die Änderungen.

**Siehe auch**


[Tabellen](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [Tabelleneigenschaften &#40;Visual Database Tools&#41;--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [Spalteneigenschaften--column-properties-visual-database-tools.md) [Hinzufügen von Spalten zu einer Tabelle--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [Primär- und Fremdschlüssel--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Indizes--../../relational-databases/indexes/indexes.md) [Datentypen (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [Herunterladen von SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







## <a name="similar-articles"></a>Ähnliche Artikel

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

Dieser Abschnitt enthält sehr ähnliche Artikel für kürzlich aktualisierte Artikel in anderen Themenbereichen innerhalb unseres öffentlichen GitHub.com-Repositorys: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die über neue oder kürzlich aktualisierte Artikel verfügen

- [Neu und aktualisiert (3+12): **Advanced Analytics für SQL** – Dokumentation](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (5+0): **Herstellen einer Verbindung mit SQL** – Dokumentation](../connect/new-updated-connect.md)
- [Neu und aktualisiert (5+1): **Datenbankmodul für SQL** – Dokumentation](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (19+82): **Integration Services für SQL** – Dokumentation](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (1+8): **Linux für SQL** – Dokumentation](../linux/new-updated-linux.md)
- [Neu und aktualisiert (12+1): **Relationale Datenbanken für SQL** – Dokumentation](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (0+1): **Reporting Services für SQL** – Dokumentation](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (7+1): **Microsoft SQL Server** – Dokumentation](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (1+1): **SQL Server Data Tools (SSDT)** – Dokumentation](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (0+2): **SQL Server Migration Assistant (SSMA)** – Dokumentation](../ssma/new-updated-ssma.md)
- [Neu und aktualisiert (1+4): **SQL Server Management Studio (SSMS)** – Dokumentation](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (4+1): **Transact-SQL** – Dokumentation](../t-sql/new-updated-t-sql.md)
- [Neu und aktualisiert (0+1): **Tools für SQL** – Dokumentation](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Themenbereiche, die über keine neuen oder kürzlich aktualisierten Artikel verfügen

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs (Neu + Aktualisiert (0+0): ActiveX Data Objects (ADO) für SQL-Dokumente)](../ado/new-updated-ado.md)
- [Neu und aktualisiert (0+0): **Analysis Services für SQL** – Dokumentation](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs (Neu + Aktualisiert (0+0): Data Quality Services für SQL-Dokumente)](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs (Neu + Aktualisiert (0+0): Data Mining-Erweiterungen (DMX) für SQL)](../dmx/new-updated-dmx.md)
- [Neu und aktualisiert (0+0): **Master Data Services (MDS) für SQL** – Dokumentation](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs (Neu + Aktualisiert (0+0): Mehrdimensionale Ausdrücke für SQL)](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs (Neu + Aktualisiert (0+0): Open Database Connectivity für SQL-Dokumente)](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs (Neu + Aktualisiert (0+0): PowerShell für SQL-Dokumente)](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs (Neu + Aktualisiert (0+0): Beispiele für SQL-Dokumente)](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs (Neu + Aktualisiert (0+0): XQuery für SQL-Dokumente)](../xquery/new-updated-xquery.md)



