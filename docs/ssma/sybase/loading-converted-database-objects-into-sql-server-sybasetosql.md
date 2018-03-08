---
title: Laden konvertierte Objekte in SQLServer (SybaseToSQL) Datenbank | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5eaf1ddf88b1658a3eb7c96d65cbae9630cc3784
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Laden konvertierte Objekte in SQLServer (SybaseToSQL) Datenbank
Nachdem Sie die Datenbankobjekte Sybase Adaptive Server Enterprise (ASE) konvertiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, laden Sie die resultierende Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Kann entweder über die SSMA, die die Objekte zu erstellen, oder können Sie Skripts für die Objekte und führen Sie die Skripts selbst. Darüber hinaus SSMA können Sie die Ziel-Metadaten mit dem tatsächlichen Inhalt aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Auswählen zwischen Synchronisierung und Skripts  
Wenn Sie die konvertierte Datenbankobjekte in laden möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure ohne Änderung können Sie SSMA direkt zu erstellen oder Neuerstellen der Datenbankobjekte haben. Diese Methode lässt sich schnell und einfach, lässt jedoch keine Anpassung der [!INCLUDE[tsql](../../includes/tsql_md.md)] Code, definiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte als gespeicherte Prozeduren.  
  
Wenn Sie ändern möchten die [!INCLUDE[tsql](../../includes/tsql_md.md)] , dient zum Erstellen der Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, oder wenn Sie mehr Kontrolle über die Objekte in, wann und wie erstellt werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, SSMA verwenden, um erstellen [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts. Sie können dann diese Skripts ändern, jedes Objekt einzeln erstellen und sogar verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure--Agent zum Planen, diese Objekte zu erstellen.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Mithilfe von SSMA zum Laden von Objekten in SQL Server- bzw. SQL Azure  
Mit SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekten, wählen Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, und synchronisieren Sie die Objekte mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, wie im folgenden Verfahren gezeigt. Standardmäßig, wenn die Objekte noch im vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und wenn die SSMA-Metadaten umfasst, einige lokale Änderungen oder Updates der Definition dieser Objekte sehr, SSMA werden die Objektdefinitionen in alter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können das Standardverhalten ändern, indem Sie die Bearbeitung **Projekteinstellungen**.  
  
> [!NOTE]  
> Sie können auswählen, vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte, die nicht von ASE Datenbanken konvertiert wurden. Allerdings werden diese Objekte nicht neu erstellt oder geändert werden von SSMA.  
  
**Zum Synchronisieren von Objekten mit SQL Server oder SQL Azure**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure Metadaten-Explorer, erweitern im oberen Bereich [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Knoten, und erweitern Sie dann **Datenbanken**.  
  
2.  Wählen Sie die zu verarbeitenden Objekte aus:  
  
    -   Um eine gesamte Datenbank zu synchronisieren, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zu synchronisieren, oder lassen Sie einzelne Objekte oder Kategorien von Objekten, aktivieren Sie, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt oder einen Ordner aus.  
  
3.  Nachdem Sie die zu verarbeitenden in Objekte ausgewählt haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Sie können auch die einzelne Objekte oder Kategorien von Objekten synchronisieren, indem das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Danach SSMA zeigt die **mit Datenbank synchronisieren** im Dialogfeld, in dem zwei Gruppen von Elementen angezeigt. Auf der linken Seite zeigt SSMA ausgewählte Datenbankobjekte in einer Struktur dargestellt. Auf der rechten Seite sehen Sie eine Struktur, die dieselben Objekte in SSMA Metadaten darstellt. Sie können die Struktur durch Klicken auf Links oder rechts erweitern Schaltfläche "+". Die Richtung der Synchronisierung wird in der Spalte Aktion, die zwischen den beiden Strukturen angeordnet wurden, angezeigt.  
  
    Eine Aktion anmelden können drei Status aufweisen:  
  
    -   Eine nach-links-Taste bedeutet, dass der Inhalt der Metadaten in der Datenbank (Standard) gespeichert werden.  
  
    -   Ein Pfeil nach rechts hindurch Datenbankinhalte SSMA Metadaten überschrieben werden.  
  
    -   Ein Kreuz bedeutet, dass keine Aktion durchgeführt wird.  
  
Klicken Sie auf den Aktion-Anmeldenamen, um den Status zu ändern. Tatsächliche Synchronisierung wird durchgeführt, wenn Sie auf **OK** Schaltfläche der **mit Datenbank synchronisieren** Dialogfeld.  
  
## <a name="scripting-objects"></a>Skripterstellung für Objekte  
Wenn Sie speichern möchten [!INCLUDE[tsql](../../includes/tsql_md.md)] möchten, dass die Definitionen der konvertierten Datenbankobjekte, oder wenn Sie die Objektdefinitionen ändern und Ausführen von Skripts selbst, können Sie der konvertierten Datenbank Definitionen von Systemobjekten, speichern [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts.  
  
**Zum Speichern von Objekten wie Skripts**  
  
1.  Nachdem Sie die Objekte in einem Skript speichern ausgewählt haben, mit der rechten Maustaste **Datenbanken**, und wählen Sie dann **speichern als Skript**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder einem enthaltenden Ordner mit der rechten Maustaste und wählen dann schreiben **speichern Skripts**.  
  
2.  In der **speichern unter** Dialogfeld Suchen den Ordner, in dem Sie speichert das Skript in einen Dateinamen eingeben möchten, die **Dateiname** Feld, und klicken Sie dann auf **OK**.  
  
    SSMA wird die SQL-Dateinamenerweiterung angefügt.  
  
### <a name="modifying-scripts"></a>Ändern von Skripts  
Nachdem Sie gespeichert haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen als ein oder mehrere Skripts, können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] anzeigen und ändern Sie die Skripts.  
  
**So ändern Sie ein Skript**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), navigieren Sie zu und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Bearbeiten und die Skriptdatei mit dem Abfrage-Editor.  
  
    Weitere Informationen zu den Abfrage-Editor, finden Sie unter "Editor halber Befehle und Funktionen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
4.  Wählen Sie zum Speichern des Skripts im Menü Datei **speichern**.  
  
### <a name="running-scripts"></a>Ausführen von Skripts  
Sie können ein Skript oder die einzelnen Anweisungen in ausführen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Zum Ausführen eines Skripts**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), navigieren Sie zu und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Um das vollständige Skript auszuführen, drücken Sie die **F5** Schlüssel.  
  
4.  Um eine Reihe von Anweisungen auszuführen, wählen Sie die Anweisungen im Abfrage-Editor-Fenster, und drücken Sie dann die **F5** Schlüssel.  
  
Weitere Informationen zum Abfrage-Editor zu verwenden, um Skripts auszuführen, finden Sie unter "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] Abfrage" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
Sie können Skripts auch über die Befehlszeile ausführen, mit der **Sqlcmd** -Dienstprogramm und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Weitere Informationen zu **Sqlcmd**, finden Sie unter "Sqlcmd (Hilfsprogramm)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent, finden Sie unter "Automatisieren von Verwaltungsaufgaben ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="securing-objects-in-sql-server"></a>Sichern von Objekten in SQLServer  
Nachdem Sie die konvertierte Datenbankobjekte in geladen haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie können die GRANT- und deny-Berechtigungen für diese Objekte. Es ist eine gute Idee, führen Sie dies vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Für finden Sie Informationen zum Sichern in Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter "Security Considerations für Datenbanken und Datenbankanwendungen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Migrieren von Sybase ASE Daten in SQL Server / SQL Azure(SybaseToSQL)](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
