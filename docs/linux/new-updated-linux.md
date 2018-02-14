---
title: "Aktualisiert – SQL Server on Linux Docs | Microsoft Docs"
description: "Aktualisierter Inhalt in zuletzt geänderten Dokumentation für Microsoft SQL Server on Linux Codeausschnitte anzeigen"
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: sql-linux,UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: 
ms.date: 02/03/2018
ms.openlocfilehash: 827399587a8147c59caf6bf31bf8b10f10c83211
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="new-and-recently-updated-sql-server-on-linux-docs"></a>Neue und zuletzt aktualisiert: SQL Server on Linux Docs



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-12-03** &nbsp; - zu - &nbsp; **2018-02-03**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## <a name="new-articles-created-recently"></a>Neue Artikel, die vor kurzem erstellt

Die folgenden Links leiten Sie zu den neuen Artikeln weiter, die erst kürzlich erstellt wurden.


1. [Konfigurieren von mehreren Subnetzen AlwaysOn-Verfügbarkeitsgruppen und Failoverclusterinstanzen](sql-server-linux-configure-multiple-subnet.md)
2. [Erstellen und Konfigurieren einer verfügbarkeitsgruppe für SQL Server on Linux](sql-server-linux-create-availability-group.md)
3. [Bereitstellen eines Clusters Schrittmacher für SQL Server on Linux](sql-server-linux-deploy-pacemaker-cluster.md)
4. [Häufig gestellte Fragen (FAQS) SQLServer on Linux](sql-server-linux-faq.md)
5. [Grundlagen der SQL Server-Verfügbarkeit für Linux-Bereitstellungen](sql-server-linux-ha-basics.md)
6. [Konfigurieren Sie einen SQL Server-Container in Kubernetes für hohe Verfügbarkeit](tutorial-sql-server-containers-kubernetes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

In diesem Abschnitt werden die Auszüge der Updates aus den Artikeln dargestellt, die vor Kurzem umfassend aktualisiert wurden.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese kompakte Liste enthält Links zu den aktualisierten Artikeln, die im Abschnitt Auszüge aufgeführt sind.

1. [Always On-Verfügbarkeitsgruppen unter Linux](#TitleNum_1)
2. [Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-always-on-availability-groups-on-linuxsql-server-linux-availability-group-overviewmd"></a>1. &nbsp;[Always On-Verfügbarkeitsgruppen unter Linux](sql-server-linux-availability-group-overview.md)

*Aktualisiert: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Weiter](#TitleNum_2))

<!-- Source markdown line 85.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 85685bc8ad3528aa26ca3f2bba7b0112808ad6f9 51aff6e55104c8f775d2b4f4461e44f689a9ee6b  (PR=4768  ,  Filename=sql-server-linux-availability-group-overview.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



Automatisches Failover einer Verfügbarkeitsgruppe ist möglich, wenn die folgenden Bedingungen erfüllt sind:

-   Das primäre und das sekundäre Replikat werden auf synchrone datenverschiebung festgelegt.
-   Die sekundäre Datenbank dem Status synchronisiert (nicht synchronisiert), was bedeutet, dass die beiden am selben Datenpunkt sind.
-   Der Typ des Clusters wird auf externen festgelegt. Automatisches Failover ist nicht möglich, mit einem Clustertyp ' None '.
-   Die `sequence_number` des sekundären Replikats zu der primären hat die höchste Sequenznummer – das heißt, des sekundären Replikats des `sequence_number` vom ursprünglichen primären Replikat entspricht.

Wenn diese Bedingungen erfüllt sind, und der Server, die das primäre Replikat hostet fehlschlägt, wird in die Verfügbarkeitsgruppe auf ein synchrones Replikat Besitz geändert werden. Das Verhalten für synchrone Replikate (von denen es drei kann insgesamt: ein primäres und zwei sekundäre Replikate) können weitere gesteuert werden, indem `required_synchronized_secondaries_to_commit`. Dies funktioniert mit Testreihen unter Windows und Linux jedoch vollständig anders konfiguriert ist. Unter Linux wird der Wert automatisch vom Cluster für die AG-Ressource selbst konfiguriert werden.

**Nur Configuration-Replikat und quorum**


Außerdem ist neu in SQL Server-2017 ab CU1 ein Replikat nur Konfiguration. Da Schrittmacher eines WSFC unterscheidet, besonders bei der Quorum- und erfordern STONITH, funktioniert müssen nur eine Konfiguration mit zwei Knoten nicht bei einer AG. Für eine FCI können die Quorum-Mechanismen von Schrittmacher Ordnung, sein, da alle Vermittlung der FCI-Failover auf den Cluster-Schicht passiert. Für eine AG erfolgt die Vermittlung unter Linux in SQL Server, in dem alle Metadaten gespeichert ist. Hier kommt das Replikat nur Konfiguration ins Spiel.

Ohne etwas anderes wäre eine dritte Knoten und mindestens ein synchronisiertes Replikat erforderlich. Dies funktioniert nicht für SQL Server Standard, da es nur zwei Replikate in einer Verfügbarkeitsgruppe teilnehmen aufweisen kann. Das Replikat nur Konfiguration speichert AG-Ebenenkonfiguration in der master-Datenbank identisch mit den anderen Replikaten in der verfügbarkeitsgruppenkonfiguration an. Das Replikat Konfiguration nur die Benutzerdatenbanken auf Einbeziehung in die AG keinen. Die Konfigurationsdaten werden von der primären synchron gesendet. Konfigurationsdaten werden anschließend während Failover ausgeführt werden, wird, ob sie automatisch oder manuell eingestellt sind.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-extract-transform-and-load-data-on-linux-with-ssissql-server-linux-migrate-ssismd"></a>2. &nbsp;[Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](sql-server-linux-migrate-ssis.md)

*Aktualisiert: 2018-01-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([vorherigen](#TitleNum_1))

<!-- Source markdown line 50.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9bba002ae3955ebb8376c7c85b7ec1ac8c706073 1533a8e0bfe553e5404de79129119b3f93185ee9  (PR=4768  ,  Filename=sql-server-linux-migrate-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=d4d880dd9c247d1e7fb7a728d5231bc9ac61c989) -->



    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Geben Sie die `/de[crypt]` Option aus, um das Kennwort eingeben, interaktiv, wie im folgenden Beispiel gezeigt:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de

    Enter decryption password:
    ```

3.  Geben Sie die `/de` Option aus, um das Kennwort in der Befehlszeile angeben, wie im folgenden Beispiel gezeigt. Diese Methode wird nicht empfohlen, da das Kennwort für die Entschlüsselung mit dem Befehl im Befehlsverlauf gespeichert.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test

    Warning: Using /De[crypt] <password> may store decryption password in command history.

    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

**Entwerfen von Paketen**


**Herstellen einer Verbindung mit der ODBC-Datenquellen**. Mit SSIS unter Linux CTP-Version 2.1 aktualisiert und höher können SSIS-Pakete auf Linux ODBC-Verbindungen. Diese Funktion wurde mit SQL Server und die MySQL-ODBC-Treiber getestet, aber auch mit jeder Unicode-ODBC-Treiber arbeiten, die die ODBC-Spezifikation berücksichtigt werden sollen. Zur Entwurfszeit können Sie entweder einen DSN oder eine Verbindungszeichenfolge in die ODBC-Verbindung angeben; Sie können auch Windows-Authentifizierung verwenden. Weitere Informationen finden Sie unter der [Blogbeitrag Ankündigung ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).







## <a name="similar-articles-about-new-or-updated-articles"></a>Ähnliche Artikel Informationen zu neuen oder aktualisierten Artikeln

Dieser Abschnitt enthält sehr ähnliche Artikel für zuletzt aktualisierte Artikel in anderen Themenbereichen innerhalb des gleichen GitHub-Repositorys: [MicrosoftDocs/sql-docs-pr](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Bereiche für die Themenbereichsdatenbank, *führen* wurden neue oder vor kurzem aktualisiert Artikel


- [Neue und aktualisierte (1 + 3):&nbsp; **Advanced Analytics für SQL** Docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Analyseplattformsystem für SQL** Docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **Herstellen einer Verbindung mit SQL** Docs](../connect/new-updated-connect.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **für SQL-Datenbank-Engine** Docs](../database-engine/new-updated-database-engine.md)
- [Neue und aktualisierte (12 + 1): **Integration Services für SQL** Docs](../integration-services/new-updated-integration-services.md)
- [Neue und aktualisierte (6 + 2):&nbsp; **Linux für SQL** Docs](../linux/new-updated-linux.md)
- [Neue und aktualisierte (15 + 0): **PowerShell für SQL** Docs](../powershell/new-updated-powershell.md)
- [Neue und aktualisierte (2 + 9):&nbsp; **relationale Datenbanken für SQL** Docs](../relational-databases/new-updated-relational-databases.md)
- [Neue und aktualisierte (1 + 0):&nbsp; **Reporting Services für SQL** Docs](../reporting-services/new-updated-reporting-services.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **SQL Operations Studio** Docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Neue und aktualisierte (1 + 1):&nbsp; **Microsoft SQL Server** Docs](../sql-server/new-updated-sql-server.md)
- [Neue und aktualisierte (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** Docs](../ssdt/new-updated-ssdt.md)
- [Neue und aktualisierte (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** Docs](../ssms/new-updated-ssms.md)
- [Neue und aktualisierte (0 + 2):&nbsp; **Transact-SQL** Docs](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Bereiche, die für die Themenbereichsdatenbank *nicht* haben eine neue oder vor kurzem aktualisiert Artikel


- [Neu + Aktualisiert (0+0): Dokumente zu **Data Migration Assistant (DMA) für SQL**](../dma/new-updated-dma.md)
- [Neue und aktualisierte (0 + 0): **ActiveX Data Objects (ADO) für SQL** Docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Analysis Services für SQL)](../analysis-services/new-updated-analysis-services.md)
- [Neue und aktualisierte (0 + 0): **Data Quality Services für SQL** Docs](../data-quality-services/new-updated-data-quality-services.md)
- [Neue und aktualisierte (0 + 0): **Data Mining Extensions (DMX) für SQL** Docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs (Neu + Aktualisiert (0+0): Dokumentation zu Master Data Services (MDS) für SQL)](../master-data-services/new-updated-master-data-services.md)
- [Neue und aktualisierte (0 + 0): **MDX (Multidimensional Expressions) für SQL** Docs](../mdx/new-updated-mdx.md)
- [Neue und aktualisierte (0 + 0): **ODBC (Open Database Connectivity) für SQL** Docs](../odbc/new-updated-odbc.md)
- [Neue und aktualisierte (0 + 0): **Samples for SQL** Docs](../sample/new-updated-sample.md)
- [Neue und aktualisierte (0 + 0): **SQL Server Migration Assistant (SSMA)** Docs](../ssma/new-updated-ssma.md)
- [Neu + Aktualisiert (0+0): Dokumentation zu **Tools für SQL**](../tools/new-updated-tools.md)
- [Neue und aktualisierte (0 + 0): **XQuery für SQL** Docs](../xquery/new-updated-xquery.md)


