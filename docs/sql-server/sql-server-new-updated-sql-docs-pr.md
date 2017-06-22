---
title: "Aktualisiert – SQL Server-Dokumentation | Microsoft Docs"
description: "Codeausschnitte anzeigen aktualisierter Inhalt in zuletzt geänderten Dokumentation für SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>Neue und zuletzt aktualisiert: SQL Server-Dokumentation



Beinahe jeden Tag Microsoft updates einige vorhandene Artikel auf dessen [Docs.Microsoft.com](http://docs.microsoft.com/) Dokumentationswebsite. Dieser Artikel zeigt Auszüge aus den zuletzt aktualisierten Artikel. Links zu den neuen Artikel, möglicherweise ebenfalls aufgeführt.

In diesem Artikel wird von einem Programm generiert, die in regelmäßigen Abständen erneut ausgeführt wird. Gelegentlich kann ein Auszug aus dem Quellartikel mit sich Formatierung oder als Markdown angezeigt. Bilder werden hier nicht angezeigt.

Neueste Updates werden für folgenden Datumsbereich und Betreff gemeldet:



- *Datumsbereich des Updates:* &nbsp; **2017-05-01** &nbsp; - zu - &nbsp; **2017-05-23**
- *Bereich für die Themenbereichsdatenbank:* &nbsp; **SQL Server**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Aktualisierte Artikel mit Auszüge

Dieser Abschnitt zeigt die Auszüge von Updates, die vom Artikel, die vor kurzem eine große Aktualisierung aufgetreten sind.

Die hier angezeigten Auszüge werden getrennt vom richtigen semantische kontextabhängig angezeigt. Darüber hinaus wird manchmal ein Auszug vom wichtige Markdown-Syntax getrennt, die sie in den tatsächlichen Artikel umgibt. Aus diesem Grund sind diese Auszüge nur allgemeine Anleitungen. Die Auszüge können nur Sie wissen, ob Ihre Interessen dauert rechtfertigen, klicken Sie auf, und besuchen den tatsächlichen Artikel.

Kopieren Sie für diese und andere Gründe Code nicht von diesen verwendet, und nehmen Sie nicht als genaue Wahrheit alle Textauszug. Besuchen Sie stattdessen den tatsächlichen Artikel aus.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp;[Versionsanmerkungen zu SQL Server 2017](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**2.1 (Mai 2017) 2017 CTP für SQL Server**

**Die Dokumentation (CTP-Version 2.1)**

- **Problem und kundenbeeinträchtigung:** Dokumentation [! INCLUDE [ssSQLv14_md--... /Includes/sssqlv14-MD.MD)] ist beschränkt und Inhalt ist im Lieferumfang der [! INCLUDE [ssSQL15_md--... Dokumentationssatz /Includes/sssql15-MD.MD)].  Inhalt in Artikeln, die für spezifische [! INCLUDE [ssSQLv14_md--... /Includes/sssqlv14-MD.MD)] mit vermerkt **gilt für**. 
- **Problem und kundenbeeinträchtigung:** keine Offlineinhalt steht für die [! INCLUDE [ssSQLv14_md--... /Includes/sssqlv14-MD.MD)].

**SQL Server Reporting Services (CTP-Version 2.1)**


- **Problem und kundenbeeinträchtigung:** , wenn Sie SQL Server Reporting Services und Power BI Berichtsserver auf demselben Computer aus, und Deinstallieren eines davon haben, Sie werden nicht mehr auf dem verbleibenden Berichtsserver mit Berichtsserver Konfigurations-Manager eine Verbindung herstellen können.
- **Problemumgehung** um dieses Problem zu umgehen, müssen Sie nach der Deinstallation von einem der Server die folgenden Vorgänge ausführen.

    1. Starten Sie eine Eingabeaufforderung im Administratormodus.
    2. Wechseln Sie zu dem Verzeichnis, in dem die verbleibenden Berichtsserver installiert ist.

        *Standardspeicherort für Power BI-Berichtsserver: C:\Program Files\Microsoft Power BI-Berichtsserver*

        *Standardspeicherort für SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. Wechseln Sie dann zu dem Ordner. Diese werden entweder *SSRS* oder *PBIRS* je nachdem, welche verfügbare Spannung anzeigt.
    4. Wechseln Sie zu den WMI-Ordner.
    5. Führen Sie den folgenden Befehl aus:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Wenn es angezeigt wird, können Sie den folgenden Fehler ignorieren.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP-Version 2.1)**


- **Problem und kundenbeeinträchtigung:** nach der Installation auf einem Computer mit einer Version von 2016 *TSqlLanguageService.msi* (entweder über SQL-Setup oder als eigenständige verteilbare) v13.* (SQL 2016)-Versionen installiert *Microsoft.SqlServer.Management.SqlParser.dll* und *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* werden entfernt. Jede Anwendung, die eine Abhängigkeit für die 2016 Versionen dieser Assemblys verfügen werden dann nicht mehr ordnungsgemäß, wodurch eine Fehlermeldung ähnlich: *Fehler: konnten nicht geladen werden, Datei oder Assembly ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = Neutral, PublicKeyToken = 89845dcd8080cc91 "oder eine ihrer Abhängigkeiten. Die angegebene Datei wurde nicht gefunden.*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2. &nbsp;[Was &#39; s neu in SQLServer 2017](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**Was ist neu in CTP für SQL Server 2017 2.1 (Mai 2017)**

** SQL Server-Datenbankmodul **

- Eine neue DMF [sys.dm_db_log_stats--... / relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), wurde eingeführt, um die Attribute der Zusammenfassung auf und Informationen zu den Transaktionsprotokolldateien; verfügbar zu machen für die Überwachung der Integritäts des Transaktionsprotokolls hilfreich.  
- Dieser CTP-Version enthält Fehlerbehebungen und leistungsverbesserungen für das Datenbankmodul.
- Eine ausführliche Liste der 2017 CTP-Verbesserungen in der vorherigen CTP-Versionen finden Sie unter [SQL Server 2017 (Datenbankmodul) – Neuigkeiten in... / database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

**SQLServer Reporting Services (SSRS)**

- SQL Server Reporting Services ist nicht mehr verfügbar ist, mithilfe von SQL Server Setup zum Zeitpunkt der CTP-Version 2.1 installiert.
- Kommentare sind jetzt für Berichte verfügbar. Kommentare können Sie Perspektive an, was in einem Bericht hinzufügen und die Zusammenarbeit mit anderen Personen in Ihrer Organisation. Sie können auch die Anlagen mit Ihren Kommentar einschließen.
- Für eine ausführlichere SSRS was neue Informationen, einschließlich Details aus früheren Versionen ist, finden Sie unter [in Reporting Services – Neuigkeiten... / reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Weitere Informationen zu Power BI-Berichtsserver, finden Sie unter [erste Schritte mit Power BI-Berichtsserver](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

**SQL Server-Machine Learning-Dienste**

- Es sind keine neuen Machine Learning-Services-Funktionen in dieser CTP-Version.
- Für ausführlichere Machine Learning Services Funktionen neue Informationen, einschließlich Details aus vorherigen CTPs, finden Sie unter [Neuigkeiten in SQL Server Machine Learning Services –... / advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

**SQL Server Analysis Services (SSAS)**

- Diese CTP enthält keine neuen SSAS-Funktionen.  
- Weitere Informationen zu Verbesserungen und Fehlerbehebungen in dieser Version finden Sie unter [in SQL Server 2017 Analysis Services – Neuigkeiten... / analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact Liste von Artikeln, die vor kurzem aktualisiert

Diese compact Liste enthält Links zu den aktualisierten Artikeln, die im vorherigen Abschnitt aufgeführt sind.

1. [Versionsanmerkungen zu SQLServer 2017](#TitleNum_1)
2. [Was &#39; s neu in SQLServer 2017](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Schwester Artikel

Dieser Abschnitt enthält sehr ähnlichen Artikel für zuletzt aktualisierten Artikel in anderen Themenbereichen, innerhalb der gleichen GitHub-Repository.


&nbsp;

[Microsoft /**Sql-Docs-Pr** ](https://github.com/microsoftdocs/sql-docs-pr/) -Repository auf "github.com":

- [Zuletzt aktualisiert: **relationale Datenbanken und Microsoft SQL Server** Docs](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Zuletzt aktualisiert: **Microsoft SQL Server** Docs](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Zuletzt aktualisiert: **Transact-SQL in SQL Server** Docs](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



