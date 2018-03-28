---
title: Mitwirken an der SQL Server-Dokumentation | Microsoft-Dokumentation
ms.date: 03/19/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1885c57cfcf21dcdb877fc4c59b229636b74c137
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/19/2018
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>Mitwirken an der SQL Server-Dokumentation

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

An der SQL Server-Dokumentation kann jeder mitwirken. Beispielsweise können Rechtschreibfehler korrigiert, genauere Erklärungen vorgeschlagen und die technische Richtigkeit geprüft werden. In diesem Artikel werden die ersten Schritte hierfür beschrieben.

Wenn Sie zur Dokumentation beitragen möchten, stehen Ihnen zwei Hauptworkflows zur Verfügung:

|||
|---|---|
| [Bearbeiten von Inhalten im Browser](#githubui) | Geeignet für kleinere Bearbeitungen eines Artikels |
| [Lokales Bearbeiten von Inhalten mit Tools](#tools) | Geeignet für komplexere Bearbeitungen in mehreren Artikeln und bei häufigen Beiträgen für docs.microsoft.com |

## <a id="githubui"></a> Bearbeiten von Inhalten im Browser

Die folgenden Schritte bieten einen Überblick über einfache Bearbeitungen von SQL Server-Inhalten im Browser. Der vollständige Prozess ist im Artikel [GitHub-Beitragsworkflow für geringfügige oder selten vorkommende Änderungen](https://docs.microsoft.com/contribute/contribute/light-workflow) dokumentiert.

1. In jedem Artikel und auch im vorliegenden Beitrag befindet sich rechts auf der Seite die Schaltfläche **Bearbeiten**. Suchen Sie zunächst einen Artikel, den Sie ändern möchten, und klicken Sie anschließend auf **Bearbeiten**.

   ![Schaltfläche „Bearbeiten“ für SQL-Artikel](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   Alle Inhalte auf docs.microsoft.com werden in verschiedenen GitHub-Repositorys verwaltet. Nach dem Klick auf die Schaltfläche werden Sie zum entsprechenden Artikel im **sql-docs**-Repository weitergeleitet. Wenn Sie stattdessen einen SQL-Artikel der Azure-Dokumentation bearbeiten, werden Sie zum **azure-docs**-Repository weitergeleitet. 

1. Klicken Sie anschließend auf GitHub im Artikel oben rechts auf das Bleistiftsymbol.

   ![Schaltfläche „Bearbeiten“](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > Sie müssen bei GitHub angemeldet sein, um einen Artikel zu bearbeiten. Wenn Sie kein GitHub-Konto besitzen, finden Sie unter [Einrichten eines GitHub-Kontos](https://docs.microsoft.com/contribute/contribute/get-started-setup-github) weitere Informationen. Nachdem Sie ein neues Konto erstellt haben, müssen Sie Ihre E-Mail-Adresse bei GitHub bestätigen, damit Sie Bearbeitungen vornehmen können.

1. Bearbeiten Sie nun den Artikel im Browser. Alle Artikel sind in Markdown geschrieben. Weitere Informationen zu dieser Auszeichnungssprache finden Sie bei Bedarf im Artikel zu [Markdown-Grundlagen](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/). Außerdem können Sie sich in bereits veröffentlichten Artikeln ansehen, wie vorhandene Markdown-Elemente gerendert werden.

1. Scrollen Sie im Bearbeitungsfenster nach unten, geben Sie eine Bezeichnung für die Änderung ein, und klicken Sie anschließend auf die Schaltfläche **Propose file change** (Dateiänderung vorschlagen).

   ![Pull Request vorschlagen](./media/sql-server-docs-contribute/propose-file-change.png)

1. Klicken Sie auf der nächsten Seite auf **Create pull request** (Pull Request erstellen).

   ![Pull Request erstellen](./media/sql-server-docs-contribute/create-pull-request.png)

1. Geben Sie eine Bezeichnung und eine Beschreibung für den Pull Request ein. Klicken Sie anschließend noch einmal auf **Create pull request** (Pull Request erstellen).

   ![Pull Request erstellen](./media/sql-server-docs-contribute/create-pull-request2.png)

Nun werden Sie in den Kommentaren des Pull Requests durch die verbleibenden Prozessschritte geführt. Den vollständigen Prozess und weitere Informationen finden Sie im [Leitfaden für Mitwirkende an der Dokumentation](https://docs.microsoft.com/contribute/contribute/light-workflow).

## <a id="tools"></a> Lokales Bearbeiten von Inhalten mit Tools

Eine weitere Bearbeitungsoption besteht darin, das **sql-docs**- oder **azure-docs**-Repository zu forken und es lokal auf dem Computer zu klonen. Anschließend können Sie mithilfe eines Markdown-Editors und eines Git-Clients die Änderungen übermitteln. Dieser Workflow eignet sich für Bearbeitungen, die komplexer sind oder mehrere Dateien betreffen. Außerdem ist er gut für Mitwirkende geeignet, die häufig Beiträge bei docs.microsoft.com einreichen.

Weitere Informationen zu dieser Bearbeitungsoption finden Sie in den folgenden Artikeln:

- [Einrichten eines GitHub-Kontos](https://docs.microsoft.com/contribute/contribute/get-started-setup-github)
- [Install content authoring tools (Installieren von Erstellungstools für Inhalte)](https://docs.microsoft.com/contribute/contribute/get-started-setup-tools)
- [Lokales Einrichten von Git für die Dokumentation](https://docs.microsoft.com/contribute/contribute/get-started-setup-local)
- [Verwenden von Tools zum Einreichen von Änderungen](https://docs.microsoft.com/contribute/contribute/full-workflow)

Wenn Sie einen Pull Request mit umfassenden Änderungen an der Dokumentation einreichen, wird in GitHub ein Kommentar angezeigt, in dem Sie aufgefordert werden, online eine **Lizenzvereinbarung für Mitwirkende** zu übermitteln. Sie müssen dieses Onlineformular ausfüllen, damit Ihr Pull Request akzeptiert wird.

## <a name="recognition"></a>Nennung als Mitwirkender

Nachdem Ihre Änderungen akzeptiert wurden, werden Sie am Anfang des Artikels als Mitwirkender genannt.

![Nennung als Mitwirkender bei Einreichung von Inhaltsänderungen](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>Übersicht über sql-docs

Dieser Abschnitt enthält zusätzliche Hinweise zur Arbeit mit dem **sql-docs**-Repository.

> [!IMPORTANT]
> Diese beziehen sich ausschließlich auf **sql-docs**. Wenn Sie stattdessen einen SQL-Artikel der Azure-Dokumentation bearbeiten, finden Sie auf [GitHub in der Infodatei des azure-docs-Repositorys](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md) weitere Informationen.

Zur Organisation von Inhalten werden im [sql-docs](https://github.com/MicrosoftDocs/sql-docs)-Repository die folgenden Standardordner verwendet:

| Ordner | Description |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | Enthält alle veröffentlichten SQL Server-Inhalte. In Unterordnern werden verschiedene Inhaltsbereiche organisiert. |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | Enthält Includedateien. Diese Dateien bestehen aus Inhaltsblöcken, die in ein oder mehrere Artikel aufgenommen werden können. |
| **./media** | Jeder Ordner kann über einen **media**-Unterordner für Artikelbilder verfügen. Der **media**-Ordner enthält wiederum Unterordner mit denselben Namen der Artikel, in denen die Bilder angezeigt werden. Bei den Bildern sollte es sich um PNG-Dateien handeln, deren Dateinamen aus Kleinbuchstaben bestehen und keine Leerzeichen enthalten. |
| **TOC.MD** | Eine Inhaltsverzeichnisdatei. In jedem Unterordner kann eine TOC.MD-Datei verwendet werden. |

#### <a name="applies-to-includes"></a>applies-to-Includedateien

In jedem SQL Server-Artikel befindet sich nach dem Titel ein Verweis auf die **applies-to**-Includedatei. Damit wird angegeben, auf welche Bereiche oder Versionen von SQL Server sich der Artikel bezieht.

Im folgenden Markdown-Beispiel wird die Includedatei **appliesto-ss-asdb-asdw-pdw-md.md** abgerufen.

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

Dadurch wird der folgende Text am Anfang des Artikels angezeigt:

![applies-to-Text](./media/sql-server-docs-contribute/applies-to.png)

Mit den folgenden Tipps finden Sie die richtigen applies-to-Includedateien:

- Suchen Sie nach anderen Artikeln, in denen es um dasselbe Feature oder um eine vergleichbare Aufgabe geht. Wenn Sie diese Artikel bearbeiten, können Sie das Markdown-Element für den Link zur applies-to-Includedatei kopieren. Dabei können Sie die Bearbeitung abbrechen, ohne die Änderungen zu senden.
- Durchsuchen Sie das Verzeichnis [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) nach Dateien, die den Text „applies-to“ enthalten. Über die Schaltfläche **Find** (Suchen) können Sie in GitHub die Ergebnisse schnell filtern. Klicken Sie auf die Datei, um festzustellen, wie diese gerendert wird.
- Beachten Sie die Namenskonvention. Wenn der Name mehrmals den Buchstaben „x“ enthält, ist dieser vermutlich ein Platzhalter, der darauf hinweist, dass ein bestimmter Dienst nicht unterstützt wird. Durch **appliesto-xx-xxxx-asdw-xxx-md.md** wird beispielsweise angegeben, dass ausschließlich Azure SQL Data Warehouse unterstützt wird, da nur die Zeichenfolge **asdw** vorhanden ist. Die anderen Felder enthalten hingegen nur den Buchstaben „x“.
- In einigen Includedateien werden Versionsnummern wie **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md** angegeben. Verwenden Sie diese Includedateien nur, wenn Sie wissen, dass dieses Feature mit einer bestimmten Version von SQL Server eingeführt wurde. 

## <a name="contributor-resources"></a>Ressourcen für Mitwirkende

- [Leitfaden für Mitwirkende an der Dokumentation auf docs.microsoft.com](https://docs.microsoft.com/en-us/contribute/)
- [Microsoft-Styleguide](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Markdown-Grundlagen](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> Wenn Sie nicht Feedback zur Dokumentation, sondern zu einem SQL Server-Produkt geben möchten, können Sie die [hierfür eingerichtete Seite](https://feedback.azure.com/forums/908035-sql-server) nutzen.

## <a name="next-steps"></a>Nächste Schritte

Auf GitHub können Sie einen genaueren Blick auf das [sql-docs-Repository](https://github.com/MicrosoftDocs/sql-docs) werfen.

Außerdem haben Sie die Möglichkeit, Artikel zu suchen, Änderungen einzureichen und die SQL Server-Community zu unterstützen. 

Wir bedanken uns für Ihre Hilfe.


