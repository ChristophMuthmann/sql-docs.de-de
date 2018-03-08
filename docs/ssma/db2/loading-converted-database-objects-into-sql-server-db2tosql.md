---
title: Laden konvertierte Objekte in SQLServer (DB2ToSQL) Datenbank | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d662bcab0fe8c804b75f7908ca6fc04f2e96a650
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>Laden konvertierte Objekte in SQLServer (DB2ToSQL) Datenbank
Nachdem Sie zu DB2-Schemas konvertiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie die resultierende Datenbankobjekte in laden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Kann entweder über die SSMA, die die Objekte zu erstellen, oder können Sie Skripts für die Objekte und führen Sie die Skripts selbst. Darüber hinaus SSMA können Sie die Ziel-Metadaten mit dem tatsächlichen Inhalt aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Auswählen zwischen Synchronisierung und Skripts  
Wenn Sie die konvertierte Datenbankobjekte in laden möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ohne Änderung können Sie SSMA direkt zu erstellen oder neu erstellen die Datenbankobjekte haben. Diese Methode lässt sich schnell und einfach, lässt jedoch keine Anpassung der [!INCLUDE[tsql](../../includes/tsql_md.md)] Code, der definiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] andere Objekte als gespeicherte Prozeduren.  
  
Wenn Sie ändern möchten die [!INCLUDE[tsql](../../includes/tsql_md.md)] , der zum Erstellen von Objekten oder wenn Sie mehr Kontrolle über die Objekte erstellen möchten, verwenden SSMA zum Erstellen von Skripts verwendet wird. Sie können dann diese Skripts ändern, jedes Objekt einzeln erstellen und sogar verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zum Planen, diese Objekte zu erstellen.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Mithilfe von SSMA zum Synchronisieren von Objekten mit SQLServer  
Mit SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbankobjekte, die Sie auswählen, dass die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, und synchronisieren Sie die Objekte mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], wie im folgenden Verfahren gezeigt. Standardmäßig, wenn die Objekte noch im vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und wenn die SSMA Metadaten neuer ist als das Objekt in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA werden die Objektdefinitionen in alter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können das Standardverhalten ändern, indem Sie die Bearbeitung **Projekteinstellungen**.  
  
> [!NOTE]  
> Sie können auswählen, vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbankobjekte, die vom DB2-Datenbanken nicht konvertiert wurden. Allerdings werden diese Objekte nicht neu erstellt oder geändert werden von SSMA.  
  
**Zum Synchronisieren von Objekten mit SQL Server**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, erweitern Sie im oberen Bereich [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Knoten, und erweitern Sie dann **Datenbanken**.  
  
2.  Wählen Sie die zu verarbeitenden Objekte aus:  
  
    -   Um eine gesamte Datenbank zu synchronisieren, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zu synchronisieren, oder lassen Sie einzelne Objekte oder Kategorien von Objekten, aktivieren Sie, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt oder einen Ordner aus.  
  
3.  Nachdem Sie die zu verarbeitenden in Objekte ausgewählt haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Sie können auch die einzelne Objekte oder Kategorien von Objekten synchronisieren, indem das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Danach SSMA zeigt die **mit Datenbank synchronisieren** im Dialogfeld, in dem zwei Gruppen von Elementen angezeigt. Auf der linken Seite zeigt SSMA ausgewählte Datenbankobjekte in einer Struktur dargestellt. Auf der rechten Seite sehen Sie eine Struktur, die dieselben Objekte in SSMA Metadaten darstellt. Sie können die Struktur durch Klicken auf Links oder rechts erweitern Schaltfläche "+". Die Richtung der Synchronisierung wird in der Spalte Aktion, die zwischen den beiden Strukturen angeordnet wurden, angezeigt.  
  
    Eine Aktion anmelden können drei Status aufweisen:  
  
    -   Eine nach-links-Taste bedeutet, dass der Inhalt der Metadaten in der Datenbank (Standard) gespeichert werden.  
  
    -   Ein Pfeil nach rechts hindurch Datenbankinhalte SSMA Metadaten überschrieben werden.  
  
    -   Ein Kreuz bedeutet, dass keine Aktion durchgeführt wird.  
  
Klicken Sie auf den Aktion-Anmeldenamen, um den Status zu ändern. Tatsächliche Synchronisierung wird durchgeführt, wenn Sie auf **OK** Schaltfläche der **mit Datenbank synchronisieren** Dialogfeld.  
  
## <a name="scripting-objects"></a>Skripterstellung für Objekte  
Speichern [!INCLUDE[tsql](../../includes/tsql_md.md)] Definitionen der konvertierten Datenbankobjekte, um die Objektdefinitionen ändern und Ausführen von Skripts selbst, können Sie speichern die konvertierte Datenbank Definitionen von Systemobjekten, [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts.  
  
**Zum Speichern von Objekten wie Skripts**  
  
1.  Nachdem Sie die Objekte in einem Skript speichern ausgewählt haben, mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **speichern als Skript**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und klicken Sie dann auf schreiben **speichern als Skript**.  
  
2.  In der **speichern unter** Dialogfeld Suchen den Ordner, in dem Sie speichert das Skript in einen Dateinamen eingeben möchten, die **Dateiname** Feld, und klicken Sie dann [!INCLUDE[clickOK](../../includes/clickok_md.md)]. SSMA wird die SQL-Dateinamenerweiterung angefügt.  
  
### <a name="modifying-scripts"></a>Ändern von Skripts  
Nachdem Sie gespeichert haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Objektdefinitionen als ein oder mehrere Skripts können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] anzeigen und ändern Sie die Skripts.  
  
**So ändern Sie ein Skript**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), wählen Sie Ihre Skriptdatei, und klicken Sie dann auf OK.
  
3.  Bearbeiten Sie die Skriptdatei, mit dem Abfrage-Editor.  
  
    Weitere Informationen zu den Abfrage-Editor, finden Sie unter "Editor halber Befehle und Funktionen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
4.  So speichern Sie das Skript auf im Menü Datei auf **speichern**.  
  
### <a name="running-scripts"></a>Ausführen von Skripts  
Sie können ein Skript oder die einzelnen Anweisungen in ausführen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Zum Ausführen eines Skripts**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** Dialogfeld wählen die Skriptdatei, und klicken Sie dann[!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
3.  Um das vollständige Skript auszuführen, drücken Sie die **F5** Schlüssel.  
  
4.  Um eine Reihe von Anweisungen auszuführen, wählen Sie die Anweisungen im Abfrage-Editor-Fenster, und drücken Sie dann die **F5** Schlüssel.  
  
Weitere Informationen zum Abfrage-Editor zu verwenden, um Skripts auszuführen, finden Sie unter "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] Abfrage" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
Sie können Skripts auch über die Befehlszeile ausführen, mit der **Sqlcmd** -Dienstprogramm und aus der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Weitere Informationen zu **Sqlcmd**, finden Sie unter "Sqlcmd (Hilfsprogramm)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent, finden Sie unter "Automatisieren von Verwaltungsaufgaben ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="securing-objects-in-sql-server"></a>Sichern von Objekten in SQLServer  
Nachdem Sie die konvertierte Datenbankobjekte in geladen haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie können die GRANT- und deny-Berechtigungen für diese Objekte. Es ist eine gute Idee, führen Sie dies vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Für finden Sie Informationen zum Sichern in Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter "Security Considerations für Datenbanken und Datenbankanwendungen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [DB2-Daten in SQL Server Migration](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Daten in SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
