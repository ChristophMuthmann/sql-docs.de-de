---
title: "Aktualisiert: Dokumentation zu SSMS für SQL Server | Microsoft-Dokumentation"
description: "Anzeigen von Codeausschnitten für aktualisierten Inhalt für kürzliche Änderungen in der Dokumentation zu SQL Server Management Studio (SSMS) für Microsoft SQL Server"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: d69c32f2159c133d7c8042359b7d65885aac39d3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Neu und kürzlich aktualisiert: SQL Server Management Studio (SSMS) für SQL Server



Beinahe jeden Tag aktualisiert Microsoft einige der vorhandenen Artikel auf der Dokumentationswebsite [Docs.Microsoft.com](http://docs.microsoft.com/). In diesem Artikel werden Auszüge aus den zuletzt aktualisierten Artikeln wiedergegeben. Links zu den neuen Artikel werden ggf. ebenfalls aufgeführt.

Dieser Artikel wurde im Rahmen eines Programms erstellt, das in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug mit falscher Formatierung oder als Markdown aus dem Quellartikel angezeigt werden. Bilder werden hier nie wiedergegeben.

Neueste Updates werden für den folgenden Datumsbereich und Themenbereich gemeldet:



- *Datumsbereich des Updates:* &nbsp; **3.12.2017** &nbsp; bis &nbsp; **3.2.2018**
- *Themenbereich:* &nbsp; **SQL Server Management Studio (SSMS)**




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt wurden

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Installieren von nicht englischsprachigen Versionen von SQL Server Management Studio (SSMS)](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszügen

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die Auszüge hier werden getrennt vom richtigen semantischen Kontext angezeigt. Darüber hinaus wird ein Auszug manchmal getrennt von der wichtigen Markdownsyntax wiedergegeben, die ihn im ursprünglichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Anhand dieser Auszüge sollen Sie nur entscheiden können, ob Sie sich die Zeit nehmen und den eigentlichen Artikel besuchen möchten.

Kopieren Sie aus diesem und anderen Gründen auf gar keinen Fall Code aus diesen Auszügen, und gehen Sie bei keinem Textauszug von einer 100-prozentigen Richtigkeit der Informationen aus. Besuchen Sie stattdessen den eigentlichen Artikel.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Kompakte Liste der Artikel, die vor Kurzem aktualisiert wurden

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Herunterladen von SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio – Änderungsprotokoll (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [Herunterladen von SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Aktualisiert: 18.01.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Nächster](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



SSMS 17.4 ist die neueste Version von SQL Server Management Studio. Die Generation 17.X von SSMS bietet Support für beinahe alle Featurebereiche unter SQL Server 2008 bis SQL Server 2017. Version 17.X unterstützt auch SQL Analysis Service-PaaS.

Version 17.4 enthält Folgendes:

Sicherheitsrisikobewertung:
- Es wurde ein neuer SQL-Risikoanalysedienst hinzugefügt, der Ihre Datenbanken auf potentielle Sicherheitsrisiken und Abweichungen von bewährten Methoden untersuchen kann, wie etwa Fehlkonfigurationen, übermäßige Berechtigungen und unzureichend geschützte vertrauliche Daten.
- Zu den Ergebnissen der Bewertung zählen Aktionsschritte zum Beheben der jeweiligen Probleme und ggf. benutzerdefinierte Skripts zur Wiederherstellung. Der Bewertungsbericht kann für die verschiedenen Umgebungen und an spezifische Anforderungen angepasst werden. Weitere Informationen finden Sie unter [SQL-Sicherheitsrisikobewertung](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Das Problem, bei dem *HasMemoryOptimizedObjects* unter Azure eine Ausnahme auslöste, wurde behoben.
- Unterstützung für die neue CATALOG_COLLATION-Funktion wurde hinzugefügt.

AlwaysOn-Dashboard:
- Verbesserungen an der Latenzanalyse in Verfügbarkeitsgruppen.
- Zwei neue Berichte: *AlwaysOn\_Latenz\_primär* und *AlwaysOn\_Latenz\_sekundär*.

Showplan:
- Aktualisierte Links verweisen auf die korrekte Dokumentation.
- Die Analyse von Einzelplänen ist direkt aus dem generierten eigentlichen Plan heraus möglich.
- Neuer Symbolsatz.
- Unterstützung für die Erkennung von „Logische Operatoren anwenden“, wie GbApply, InnerApply.

XE-Profiler:
- In XEvent Profiler umbenannt.
- Die Menübefehle „Stopp“/„Start“ führen jetzt standardmäßig zum Beenden/Starten der Sitzung.
- Aktivierte Tastenkombinationen (z. B. STRG-F zum Suchen).
- Hinzugefügte Aktionen ‚database\_name‘ und ‚client\_hostname‘ zu den entsprechenden Ereignissen in XEvent Profiler-Sitzungen. Damit die Änderung wirksam wird, müssen Sie möglicherweise vorhandene QuickSessionStandard- oder QuickSessionTSQL-Instanzen auf den Servern löschen – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2. &nbsp; [SQL Server Management Studio – Änderungsprotokoll (SSMS)](sql-server-management-studio-changelog-ssms.md)

*Aktualisiert: 29.01.2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Vorheriger](#TitleNum_1))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

Allgemein verfügbar | Buildnummer: 14.0.17213.0

**Neuigkeiten**


**SSMS Allgemein**

Sicherheitsrisikobewertung:
- Es wurde ein neuer SQL-Risikoanalysedienst hinzugefügt, der Ihre Datenbanken auf potentielle Sicherheitsrisiken und Abweichungen von bewährten Methoden untersuchen kann, wie etwa Fehlkonfigurationen, übermäßige Berechtigungen und unzureichend geschützte vertrauliche Daten.
- Zu den Ergebnissen der Bewertung zählen Aktionsschritte zum Beheben der jeweiligen Probleme und ggf. benutzerdefinierte Skripts zur Wiederherstellung. Der Bewertungsbericht kann für die verschiedenen Umgebungen und an spezifische Anforderungen angepasst werden. Weitere Informationen finden Sie unter [SQL-Sicherheitsrisikobewertung](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Das Problem, bei dem *HasMemoryOptimizedObjects* unter Azure eine Ausnahme auslöste, wurde behoben.
- Unterstützung für die neue CATALOG_COLLATION-Funktion wurde hinzugefügt.

AlwaysOn-Dashboard:
- Verbesserungen an der Latenzanalyse in Verfügbarkeitsgruppen.
- Zwei neue Berichte: *AlwaysOn\_Latenz\_primär* und *AlwaysOn\_Latenz\_sekundär*.

Showplan:
- Aktualisierte Links verweisen auf die korrekte Dokumentation.
- Die Analyse von Einzelplänen ist direkt aus dem generierten eigentlichen Plan heraus möglich.
- Neuer Symbolsatz.
- Unterstützung für die Erkennung von „Logische Operatoren anwenden“, wie GbApply, InnerApply.

XE-Profiler:
- In XEvent Profiler umbenannt.
- Die Menübefehle „Stopp“/„Start“ führen jetzt standardmäßig zum Beenden/Starten der Sitzung.
- Aktivierte Tastenkombinationen (z. B. STRG-F zum Suchen).
- Hinzugefügte Aktionen ‚database\_name‘ und ‚client\_hostname‘ zu den entsprechenden Ereignissen in XEvent Profiler-Sitzungen. Damit die Änderung wirksam wird, müssen Sie möglicherweise vorhandene QuickSessionStandard- oder QuickSessionTSQL-Instanzen auf den Servern löschen – [Connect 3142981](https://connect.microsoft.com/SQLServer/feedback/details/3142981)

Befehlszeile:
- Neue Befehlszeilenoption („-G“), die verwendet werden kann, um SSMS automatisch eine Verbindung mit einem Server/einer Datenbank mithilfe von Active Directory-Authentifizierung (wahlweise ‚Integrated‘ oder ‚Password‘) herstellen zu lassen. Weitere Informationen finden Sie unter [Ssms-Hilfsprogramm](ssms-utility.md).







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Themenbereiche, die *über* neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (1+3):&nbsp;Dokumente zu **Advanced Analytics für SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Analytics Platform System für SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zum **Herstellen einer Verbindung mit SQL**](../connect/new-updated-connect.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zur **Datenbank-Engine für SQL**](../database-engine/new-updated-database-engine.md)
- [Neu und aktualisiert (12+1): Dokumente zu **Integration Services für SQL**](../integration-services/new-updated-integration-services.md)
- [Neu und aktualisiert (6+2):&nbsp;Dokumente zu **Linux für SQL**](../linux/new-updated-linux.md)
- [Neu und aktualisiert (15+0): Dokumente zu **PowerShell für SQL**](../powershell/new-updated-powershell.md)
- [Neu und aktualisiert (2+9):&nbsp;Dokumente zu **relationalen Datenbanken für SQL**](../relational-databases/new-updated-relational-databases.md)
- [Neu und aktualisiert (1+0):&nbsp;Dokumente zu **Reporting Services für SQL**](../reporting-services/new-updated-reporting-services.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neu und aktualisiert (1+1):&nbsp;Dokumente zu **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Neu und aktualisiert (0+1):&nbsp;Dokumente zu **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Neu und aktualisiert (1+2):&nbsp;Dokumente zu **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Neu und aktualisiert (0+2):&nbsp;Dokumente zu **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Themenbereiche, die *nicht* über neue oder kürzlich aktualisierte Artikel verfügen


- [Neu und aktualisiert (0+0): Dokumente zum **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neu und aktualisiert (0+0): Dokumente zu **ActiveX Data Objects (ADO) für SQL**](../ado/new-updated-ado.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Analysis Services für SQL**](../analysis-services/new-updated-analysis-services.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Data Quality Services für SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Data Mining-Erweiterungen (DMX) für SQL**](../dmx/new-updated-dmx.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Master Data Services (MDS) für SQL**](../master-data-services/new-updated-master-data-services.md)
- [Neu und aktualisiert (0+0): Dokumente zu **mehrdimensionalen Ausdrücken (MDX) für SQL**](../mdx/new-updated-mdx.md)
- [Neu und aktualisiert (0+0): Dokumente zu **ODBC (Open Database Connectivity) für SQL**](../odbc/new-updated-odbc.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Beispielen für SQL**](../sample/new-updated-sample.md)
- [Neu und aktualisiert (0+0): Dokumente zum **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Neu und aktualisiert (0+0): Dokumente zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neu und aktualisiert (0+0): Dokumente zu **XQuery für SQL**](../xquery/new-updated-xquery.md)


