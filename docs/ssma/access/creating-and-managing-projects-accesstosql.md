---
title: Erstellen und Verwalten von Projekten (AccessToSQL) | Microsoft Docs
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
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: 22
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc89d40afd125aef5c874c4578bb153cdfcf6993
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="creating-and-managing-projects-accesstosql"></a>Erstellen und Verwalten von Projekten (AccessToSQL)
Zum Migrieren von Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, müssen Sie zuerst eine SSMA-Projekt erstellen. Das Projekt ist eine Datei mit Metadaten über die Access-Datenbanken, die Sie zum migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Metadaten zu der Zielinstanz von SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, die die migrierten Objekte und Daten, erhalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungs- und Einstellungen für Projektdateien.  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen die standardmäßigen Projekteinstellungen  
SSMA enthält mehrere Optionen zum Umrechnen und Synchronisieren von Datenbankobjekten und zum Konvertieren von Daten. Die Standardeinstellung für diese Optionen eignet sich für viele Benutzer. Jedoch bevor Sie ein neues SSMA-Projekt erstellen, sollten Sie überprüfen Sie die Optionen und, wenn Sie möchten, ändern die Standardeinstellungen, die für alle neuen Projekte verwendet werden.  
  
**Um standardprojekteinstellungen zu überprüfen.**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**.  
  
2.  Wählen Sie den Projekttyp in **Migration Zielversion** Dropdownmenü für die Einstellungen angezeigt bzw. geändert werden, und klicken Sie dann auf **allgemeine** Registerkarte.  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich die Optionen aus. Weitere Informationen zu diesen Optionen finden Sie unter [Projekteinstellungen (Konvertierung)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Ändern Sie Optionen nach Bedarf.  
  
6.  Wiederholen Sie die vorherigen Schritte für die **Migration**, **GUI**, und **Type Mapping** Seiten.  
  
    -   Informationen zu Migrationsoptionen finden Sie unter [Projekteinstellungen (Migration)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Informationen zu den Benutzeroberflächenoptionen finden Sie unter [Projekt Einstellungen (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Weitere Informationen zu den datentypzuordnung Einstellungen finden Sie unter [Projekteinstellungen (Zuordnung)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Weitere Informationen zu SQL Azure-Einstellungen finden Sie unter [Projekteinstellungen (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Hinweis** SQL Azure-Einstellungen stehen nur, wenn Sie die Migration zu SQL Azure beim Erstellen eines Projekts auswählen.  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
SSMA wird gestartet, ohne ein Standardprojekt geladen. Zum Migrieren von Daten aus Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, müssen Sie ein Projekt erstellen.  
  
**Zum Erstellen eines neuen Projekts**  
  
1.  Wählen Sie im Menü **Datei** die Option **Neues Projekt** aus.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
3.  In der **Speicherort** Feld, geben Sie ein oder wählen Sie einen Ordner für das Projekt  
  
4.  In der Dropdownliste der Migration auf nach unten, wählen Sie eine der SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / SQL Server 2016 / Azure SQL-Datenbank, und klicken Sie dann auf **OK**.  
  
SSMA wird die Projektdatei erstellt. Sie können nun den nächsten Schritt ausführen [Hinzufügen von Access-Datenbanken für eine oder mehrere](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Zusätzlich zum Definieren von standardmäßigen projekteinstellungen verwenden, die für alle neuen SSMA-Projekte gelten, können Sie auch die Einstellungen für jedes Projekt anpassen. Weitere Informationen finden Sie unter [Einstellung Konvertierung und Migrationsoptionen](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167).  
  
Wenn Sie datentypzuordnungen zwischen Quell-und Zieldatenbanken anpassen, können Sie Zuordnungen auf das Projekt, Datenbank oder Objektebene definieren. Weitere Informationen zur Zuordnung finden Sie unter [Zuordnungsquelle und Ziel-Datentypen](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Wenn Sie ein Projekt speichern, speichert SSMA den projekteinstellungen und optional die Datenbank-Metadaten in die Projektdatei.  
  
**Um ein Projekt zu speichern.**  
  
-   Auf der **Datei** klicken Sie im Menü **Projekt speichern**.  
  
    Wenn Datenbanken innerhalb des Projekts sich verändert haben oder nicht konvertiert wurde, fordert SSMA Sie Metadaten in das Projekt zu speichern. Speichern von Metadaten können offline arbeiten. Außerdem können Sie eine vollständige Projektdatei an andere Personen, einschließlich der technischen Support in Verbindung zu senden. Wenn Sie aufgefordert werden, um Metadaten zu speichern, führen Sie folgende Schritte aus:  
  
    1.  Für jede Datenbank, die den Status anzeigt **fehlenden Metadaten**, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
        Speichern von Metadaten kann einige Minuten dauern. Wenn Sie nicht, um Metadaten zu diesem Zeitpunkt zu speichern möchten, wählen Sie alle Kontrollkästchen nicht.  
  
    2.  Klicken Sie auf **Speichern**.  
  
        SSMA analysiert der Access-Schemas und speichern Sie die Metadaten in die Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird getrennt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Dadurch können Sie offline arbeiten. Beim Aktualisieren der Metadaten-Load-Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Um Daten zu migrieren, müssen die Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
**Öffnen eines Projekts**  
  
1.  Verwenden Sie eine der folgenden Verfahren aus:  
  
    -   Auf der **Datei** Sie im Menü **zuletzt geöffnete Projekte**, und wählen Sie dann das Projekt, das Sie öffnen möchten.  
  
    -   Auf der **Datei** klicken Sie im Menü **Projekt öffnen**, suchen Sie die Projektdatei .a2ssproj, wählen Sie die Datei, und klicken Sie dann auf **öffnen**.  
  
2.  Eine Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]auf die **Datei** klicken Sie im Menü **eine erneute Verbindung mit SQL Server**.  
  
3.  Verbindung zu SQL Azure, auf die **Datei** klicken Sie im Menü **das erneute Verbinden mit SQL Azure.**  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [eine oder mehrere Access-Datenbanken hinzufügen](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Hinzufügen und Entfernen von Access-Datenbankdateien](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  

