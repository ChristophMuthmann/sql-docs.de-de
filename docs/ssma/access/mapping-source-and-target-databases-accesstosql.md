---
title: Zuordnen von Quell- und Zieldatenbanken (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 77266085cf8a55322abf184fb18c5be26af95939
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Zuordnen von Quell- und Zieldatenbanken (AccessToSQL)
Wenn Sie eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, müssen Sie eine Zieldatenbank für die Migration angeben. Wenn Sie mehrere Access-Datenbanken haben können Sie sie mit mehreren zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken (oder Schemas) oder auf mehrere Schemas unter der verbundenen SQL Azure-Datenbank.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server- oder SQL Azure-Datenbankschemas  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken verwenden das Konzept des Schemas, um Objekte innerhalb einer Datenbank in logische Gruppen zu unterteilen. Bibliotheksdatenbank könnten z. B. drei Schemas, die mit dem Namen verwenden **Bücher**, **audio**, und **video** Buch, Audio- und Videofunktionen Objekte voneinander zu trennen. Wird standardmäßig die Access-Datenbank zugeordnet ist **master** Datenbank und **Dbo** Schema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bzw. aus einer verbundenen Datenbank und **Dbo** Schema in SQL Azure.  
  
Wenn Sie die Zuordnung zwischen jeder Access-Datenbank anzupassen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank- und Schemaobjekte, SSMA werden migriert, die Schemas und Daten der Zugriffsdatenbank auf die Standarddatenbank zugeordnet zugeordnet.  
  
## <a name="modifying-the-target-database-and-schema"></a>Ändern der Zieldatenbank und Schema  
SSMA können Sie jede Access-Datenbank zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank und Schema. Das folgende Verfahren beschreibt, wie die Zuordnung pro Datenbank anpassen.  
  
**So ändern Sie die Zieldatenbank und das schema**  
  
1.  Wählen Sie im Bereich Metadaten-Explorer Zugriff **Metadaten zugreifen**.  
  
    Schemazuordnung ist auch verfügbar, bei der Auswahl der **Datenbanken** alle Datenbankknoten "oder". Die Liste der Schema-Zuordnung wird für das ausgewählte Objekt angepasst.  
  
2.  Klicken Sie im rechten Bereich auf die **Schema zuordnen** Registerkarte.  
  
    Sehen Sie eine Tabelle mit Access Datenbanknamen und der entsprechenden SsNoVersion oder des Sql Azure-Schemas. Das Zielschema wird in zwei Teilen Vermerk (database.schema) gekennzeichnet.  
  
3.  Wählen Sie die Zeile, die die Zuordnung enthält anpassen, und klicken Sie dann auf **ändern**.  
  
4.  In der **Zielschema auswählen** (Dialogfeld), können Sie für die Zieldatenbank verfügbar "und" Schema "oder" Geben Sie die Datenbank und das Schema in das Textfeld in einer zweiteiligen-Schreibweise (database.schema) und klicken Sie dann auf Durchsuchen **OK**.  
  
**Modi für eine Zuordnung**  
  
-   Zuordnen von SQL Server  
  
Sie können keiner Zieldatenbank Quelldatenbank zuordnen. Standardmäßig wird die Quelldatenbank zugeordnet Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, mit denen Sie über SSMA verbunden haben. Wenn die Zieldatenbank zuzuordnenden auf nicht vorhanden ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann mit einer Meldung werden Sie aufgefordert **"die Datenbank bzw. das Schema ist nicht im Ziel vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen?"** Klicken Sie auf "Ja". Auf ähnliche Weise können Sie Schemas unter Ziel nicht vorhandenen Schema zuordnen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank, der während der Synchronisierung erstellt wird.  
  
-   Zuordnen zu SQL Azure  
  
Sie können die Quelldatenbank zuordnen, mit dem Ziel verbunden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank oder alle Schemas in der verbundenen Ziel [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank. Wenn Sie alle nicht vorhandenen Schema unter verbundenen Zieldatenbank Quelle Schema zuordnen, werden Sie mit einer Meldung aufgefordert **"das Schema ist im Ziel-Metadaten nicht vorhanden. Sie würden während der Synchronisierung erstellt werden. Möchten Sie den Vorgang fortsetzen? "** Klicken Sie auf "Ja".  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Zurücksetzen auf die ursprüngliche Datenbank und Schema  
Wenn Sie die Zuordnung zwischen einer Access-Datenbank anpassen und eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank und Schema können Sie die Zuordnung wieder in der Datenbank, die Sie angegeben, wenn Sie mit verbunden wiederherstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
**Zurücksetzen auf die Standarddatenbank und schema**  
  
1.  Klicken Sie unter der Registerkarte "Schema-Zuordnung" Wählen Sie eine beliebige Zeile, und klicken Sie auf **auf Standard zurücksetzen** , um die Standarddatenbank und das Schema wiederherzustellen.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [Konvertieren von Datenbankobjekten](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
