---
title: Öffnen eines Editors (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5d654a60-d205-49d2-a831-b3d986d60024
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a97be4e5f33e387f2046cf2674b5a57cda7cf0e6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="open-an-editor-sql-server-management-studio"></a>Öffnen eines Editors (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  In diesem Thema wird beschrieben, wie die [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-, MDX-, DMX- oder XML/A-Editoren in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]geöffnet werden. Nach dem Öffnen werden alle Editor-Fenster als Registerkarte im zentralen Bereich von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]angezeigt.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] unterstützt vier Editoren: [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor zum Bearbeiten von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts, DMX- und MDX-Editoren zum Bearbeiten von Skripts mit diesen Sprachen und XML/A-Editor zum Bearbeiten von XML/A-Skripts oder XML-Dateien. Diese Editoren können alle auch zum Bearbeiten von Textdateien verwendet werden.  
  
### <a name="limitations-and-restrictions"></a>Einschränkungen  
 Falls Sie Dateien mit Benutzern an anderen Standorten gemeinsam nutzen, an denen andere Codepages verwendet werden, sollten Sie die Datei mit der entsprechenden Unicode-Codepage speichern, um Fehler beim Lesen der Datei zu vermeiden. Auch wenn Sie Dateien für UNIX oder Macintosh speichern, sollten Sie darauf achten, die Dateien im geeigneten Dokumentformat zu speichern. Klicken Sie im Menü **Datei** auf **Speichern unter**, klicken Sie auf den Pfeil neben der Schaltfläche **Speichern** , klicken Sie auf **Mit Codierung speichern** , und wählen Sie dann unter **Zeilenenden** entweder **Unix** oder **Macintosh**aus.  
  
### <a name="permissions"></a>Berechtigungen  
 Vorgänge, die Sie in einem Code-Editor ausführen, unterliegen den dem für die Anmeldung verwendeten Authentifizierungskonto erteilten Berechtigungen. Wenn Sie beispielsweise mit der Windows-Authentifizierung ein Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors öffnen, können Sie keine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen ausführen, die auf Objekte verweisen, für die dem Windows-Anmeldekonto keine Zugriffsberechtigungen erteilt wurden.  
  
## <a name="how-to-open-editors"></a>Vorgehensweise: Öffnen von Editoren  
 In diesem Abschnitt wird erläutert, wie die verschiedenen Editoren in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]geöffnet werden.  
  
### <a name="using-the-filenew-menu"></a>Verwenden des Menüs "Datei/Neu"  
 Klicken Sie im Menü **Datei** auf **Neu**, und wählen Sie dann eine Abfrage-Editor-Option aus:  
  
-   **Abfrage mit aktueller Verbindung** – Öffnet ein neues Editor-Fenster des Typs, der der aktuellen Verbindung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]zugeordnet ist. Das Editor-Fenster verwendet die gleichen Authentifizierungsinformationen wie die aktuelle Verbindung. Wenn Sie z. B. im Objekt-Explorer eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auswählen und dann **Abfrage mit aktueller Verbindung**verwenden, wird von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ein [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor geöffnet, der mit der gleichen Instanz verbunden ist und die gleichen Authentifizierungsinformationen verwendet.  
  
-   **Datenbankmodul-Abfrage** – Öffnet einen neuen [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services MDX-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -MDX-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services DMX-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -DMX-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services XML/A-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -XML/A-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
### <a name="using-the-fileopen-menu"></a>Verwenden des Menüs "Datei/Öffnen"  
 Klicken Sie im Menü **Datei** auf **Öffnen**, und navigieren Sie anschließend zu einer Datei, und öffnen Sie sie. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] wird der entsprechende Editor-Typ für die Dateierweiterung geöffnet, der Inhalt der Datei ins Editor-Fenster kopiert und außerdem ggf. ein Dialogfeld für die Verbindung geöffnet. Wenn Sie z. B. eine Datei mit der Erweiterung ".sql" öffnen, wird von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ein Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors geöffnet, der Inhalt in die SQL-Datei kopiert und ein Verbindungsdialogfeld geöffnet. Wenn Sie eine Datei mit einer Erweiterung öffnen, die keinem bestimmten Editor zugeordnet ist, wird von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ein Text-Editor-Fenster geöffnet und der Inhalt der Datei dort hinein kopiert.  
  
 Weitere Informationen finden Sie unter [Zuordnen von Dateierweiterungen zu einem Code-Editor](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md).  
  
### <a name="using-the-toolbar"></a>Verwenden der Symbolleiste  
 Klicken Sie auf der Symbolleiste **Standard** auf eine der folgenden Schaltflächen:  
  
-   **Neue Abfrage** – Öffnet ein neues Editor-Fenster des Typs, der der aktuellen Verbindung in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]zugeordnet ist. Das Editor-Fenster verwendet die gleichen Authentifizierungsinformationen wie die aktuelle Verbindung. Wenn Sie z. B. im Objekt-Explorer eine Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] auswählen und dann auf die Schaltfläche **Neue Abfrage** klicken, wird von [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ein [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor geöffnet, der mit der gleichen Instanz verbunden ist und die gleichen Authentifizierungsinformationen verwendet.  
  
-   **Datenbankmodul-Abfrage** – Öffnet einen neuen [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services MDX-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -MDX-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services DMX-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -DMX-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
-   **Analysis Services XML/A-Abfrage** – Öffnet einen neuen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -XML/A-Abfrage-Editor und ein Dialogfeld, um die zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erforderlichen Informationen abzurufen.  
  
### <a name="using-object-explorer"></a>Verwenden des Objekt-Explorers  
 Im **Objekt-Explorer**:  
  
-   Klicken Sie mit der rechten Maustaste auf den mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]verbundenen Serverknoten, und wählen Sie anschließend **Neue Abfrage**aus. Dadurch wird ein mit derselben Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verbundenes Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors geöffnet und der Datenbankkontext des Fensters auf die Standarddatenbank für die Anmeldung festgelegt.  
  
-   Klicken Sie mit der rechten Maustaste auf einen Datenbankknoten, und wählen Sie dann **Neue Abfrage**aus. Dadurch wird ein mit derselben Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] verbundenes Fenster des [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Abfrage-Editors geöffnet und der Datenbankkontext des Fensters auf dieselbe Datenbank festgelegt.  
  
### <a name="using-solution-explorer"></a>Verwenden des Projektmappen-Explorers  
 Erweitern Sie im **Projektmappen-Explorer**einen Ordner, klicken Sie mit der rechten Maustaste auf ein Element im Ordner, und klicken Sie dann auf **Öffnen** , oder doppelklicken Sie auf das Element bzw. die Datei.  
  
### <a name="using-template-browser-to-open-the-database-engine-query-editor"></a>Verwenden des Vorlagenbrowsers zum Öffnen des Datenbankmodul-Abfrage-Editors  
  
-   Klicken Sie im Menü **Ansicht** auf **Vorlagen-Explorer**.  
  
-   Das Fenster **Vorlagenbrowser** wird im rechten Bereich angezeigt.  
  
-   Doppelklicken Sie auf eine Vorlage, um ein Fenster für die Datenbankmodul-Abfrage mit dem Text der Vorlage zu öffnen. Um z. B. eine CREATE DATABASE-Vorlage zu öffnen, öffnen Sie den Ordner **SQL Server-Vorlagen** und dann den Ordner **Datenbanken** , und doppelklicken Sie auf **Datenbank erstellen**.  
  
  
