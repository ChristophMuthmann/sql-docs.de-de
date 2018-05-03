---
title: Erstellen von Skripts (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: mathoma
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e85cf27b84317c2d942a4a5e42bf619504a1cee0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="generate-scripts-sql-server-management-studio"></a>Erstellen von Skripts (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] stellt zwei Mechanismen zum Generieren von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts bereit. Verwenden Sie zum Erstellen von Skripts für mehrere Objekte den **Assistenten zum Generieren und Veröffentlichen von Skripts**. Sie können ein Skript für einzelne Objekte oder mehrere Objekte auch über das Menü **Skript für** im **Objekt-Explorer**generieren.  

Ein ausführliches Tutorial zur Skripterstellung für verschiedene Objekte mithilfe von SQL Server Management Studio finden Sie unter [Tutorial: Scripting in SSMS (Tutorial: Skripterstellung in SSMS)](https://docs.microsoft.com/en-us/sql/ssms/tutorials/scripting-ssms).

  
## <a name="before-you-begin"></a>Vorbereitungen  
 Wählen Sie den Mechanismus aus, der Ihre Anforderungen am besten erfüllt.  
  
###  <a name="GenPubScriptWiz"></a> Assistent zum Generieren und Veröffentlichen von Skripts  
 Verwenden Sie den **Assistenten zum Generieren und Veröffentlichen von Skripts** , um ein [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skript für zahlreiche Objekte zu erstellen. Der Assistent generiert ein Skript für alle in einer Datenbank enthaltenen Objekte bzw. für eine ausgewählte Teilmenge der Objekte. Der Assistent verfügt über viele Optionen für Skripts, z. B. ob Berechtigungen, Sortierung, Einschränkungen usw. eingeschlossen werden sollen. Anweisungen zum Verwenden des Assistenten finden Sie unter [Generate and Publish Scripts Wizard](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Objekt-Explorer-Menü "Skript für Objekttyp als"  
 Sie können das Menü **Skripterstellung als** des Objekt-Explorers verwenden, um ein Skript für ein einzelnes Objekt, für mehrere Objekte bzw. mehrere Anweisungen für einzelne Objekte zu erstellen. Sie können unter mehreren Skripttypen auswählen: z. B. zum Erstellen, Ändern oder Löschen des Objekts. Sie können das Skript entweder im Abfrage-Editor-Fenster, in einer Datei oder in der Zwischenablage speichern. Das Skript wird im Unicode-Format erstellt.  
  
##  <a name="ScriptSingleObject"></a> So generieren Sie ein Skript für ein einzelnes Objekt  
 **So erstellen Sie ein Skript für ein einzelnes Objekt**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie dann die Datenbank, die das Objekt enthält, das geschrieben werden soll.  
  
3.  Erweitern Sie die Kategorie des Objekts. Beispiel: Erweitern Sie den Knoten **Tabellen** oder **Sichten** .  
  
4.  Klicken Sie mit der rechten Maustaste auf das Objekt, zeigen Sie auf **Skript für \<Objekttyp> als**. Zeigen Sie z.B. auf **Skripttabelle als**.  
  
5.  Zeigen Sie auf den Skripttyp, z. B. **CREATE in** oder **ALTER in**.  
  
6.  Wählen Sie den Speicherort zum Speichern des Skripts aus, z. B. **Neues Abfrage-Editor-Fenster** oder **Zwischenablage**.  

    ![Skripterstellung für Tabellen](media/generate-scripts-sql-server-management-studio/scripttable.png)
  
  
 Sie können den Bereich **Details** des Objekt-Explorers verwenden, um ein Skript für mehrere Objekte der gleichen Kategorie zu generieren.  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit einer Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] her, und erweitern Sie dann diese Instanz.  
  
2.  Erweitern Sie **Datenbanken**, und erweitern Sie dann die Datenbank, die die Objekte enthält, die geschrieben werden sollen.  
  
3.  Erweitern Sie den Kategorieknoten der Objekttypen, für die Sie ein Skript erstellen möchten, z. B. den Knoten **Tabellen** .  
  
4.  Öffnen Sie den Bereich **Details zum Objekt-Explorer** durch Drücken von **F7**oder durch Öffnen des Menüs **Ansicht** und Auswahl der Option **Details zum Objekt-Explorer**.  
  
5.  Klicken Sie mit der linken Maustaste auf eines der Objekte, für das Sie ein Skript erstellen möchten.  
  
6.  Klicken Sie bei gedrückter STRG-TASTE mit der linken Maustaste auf das zweite Objekt, für das Sie ein Skript erstellen möchten.  
  
7.  Klicken Sie mit der rechten Maustaste auf eines der ausgewählten Objekte, und wählen Sie **Skript für \<Objekttyp> als** aus.  

    ![Objekt-Explorer](media/generate-scripts-sql-server-management-studio/objectexplorerdetails.png)
  
  
