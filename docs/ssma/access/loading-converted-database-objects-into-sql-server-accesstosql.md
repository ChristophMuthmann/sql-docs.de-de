---
title: Laden konvertierte Objekte in SQLServer (AccessToSQL) Datenbank | Microsoft Docs
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
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5def0c73f1c77a289eb926c4d8ab7691a6d19253
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>Laden konvertierte Objekte in SQLServer (AccessToSQL) Datenbank
Nachdem Sie den Zugriff auf Datenbankobjekte zu konvertiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, laden Sie die resultierende Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Kann entweder über die SSMA, die die Objekte zu erstellen, oder können Sie Skripts für die Objekte und führen Sie die Skripts selbst. Darüber hinaus SSMA können Sie die Ziel-Metadaten mit dem tatsächlichen Inhalt aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Auswählen zwischen Synchronisierung und Skripts  
Wenn Sie die konvertierte Datenbankobjekte in laden möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure ohne Änderung haben Sie SSMA direkt erstellen oder Neuerstellen von Datenbankobjekten. Diese Methode lässt sich schnell und einfach, lässt jedoch keine Anpassung der [!INCLUDE[tsql](../../includes/tsql_md.md)] Code, der definiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte als gespeicherte Prozeduren.  
  
Wenn Sie ändern möchten die [!INCLUDE[tsql](../../includes/tsql_md.md)] , der zum Erstellen von Objekten oder wenn Sie mehr Kontrolle über die Objekte erstellen möchten, verwenden SSMA zum Erstellen von Skripts verwendet wird. Sie können dann diese Skripts ändern, jedes Objekt einzeln erstellen und sogar verwenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent zum Planen, diese Objekte zu erstellen.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Mithilfe von SSMA zum Synchronisieren von Objekten mit SQLServer  
Mit SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekten, wählen Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, und synchronisieren Sie die Objekte mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, wie im folgenden Verfahren gezeigt. Standardmäßig, wenn die Objekte noch im vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und wenn die SSMA-Metadaten umfasst, einige lokale Änderungen oder Updates der Definition dieser Objekte sehr, SSMA werden die Objektdefinitionen in alter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können das Standardverhalten ändern, indem Sie die Bearbeitung **Projekteinstellungen**.  
  
> [!NOTE]  
> Sie können auswählen, vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte, die von Access-Datenbanken nicht konvertiert wurden. SSMA wird allerdings nicht neu erstellen oder ändern diese Objekte.  
  
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
  
**Um ein oder mehrere Objekte in ein Skript zu speichern.**  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Metadaten-Explorer, erweitern Sie den obersten Knoten (Servername) und dann **Datenbanken**.  
  
2.  Führen Sie eine oder mehrere der folgenden:  
  
    -   Um ein Skript erstellen eine vollständige Datenbank, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Um das Skript aus, oder lassen die einzelne Ansichten, erweitern Sie die Datenbank und **Ansichten**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Ansicht.  
  
    -   Um das Skript aus, oder lassen einzelne Tabellen, erweitern Sie die Datenbank und **Tabellen**, und klicken Sie dann aktivieren oder deaktivieren Sie das Kontrollkästchen neben der Tabelle.  
  
    -   Um das Skript aus, oder lassen die einzelnen Indizes für eine Tabelle, erweitern Sie die Tabelle und **Indizes**, und klicken Sie dann aktivieren oder Deaktivieren des Indexes.  
  
3.  Mit der rechten Maustaste **Datenbanken** , und wählen Sie **speichern als Skript**.  
  
    Sie können auch einzelne Objekte schreiben. Um ein Objekt, das Skript, unabhängig davon, welche Objekte ausgewählt sind, mit der rechten Maustaste in des Objekts, und wählen Sie **speichern als Skript**.  
  
4.  In der **speichern unter** Dialogfeld Suchen den Ordner, in dem Sie speichert das Skript in einen Dateinamen eingeben möchten, die **Dateiname** Feld, und klicken Sie dann auf **OK**.  
  
    SSMA wird die SQL-Dateinamenerweiterung angefügt.  
  
### <a name="modifying-scripts"></a>Ändern von Skripts  
Nachdem Sie gespeichert haben die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objektdefinitionen als ein Skript, können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] das Skript ändern.  
  
**So ändern Sie ein Skript**  
  
1.  Auf der [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), suchen und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Bearbeiten Sie die Skriptdatei, mit dem Abfrage-Editor.  
  
    Weitere Informationen zu den Abfrage-Editor, finden Sie unter "Editor halber Befehle und Funktionen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
4.  Wählen Sie zum Speichern des Skripts im Menü Datei **speichern**.  
  
### <a name="running-scripts"></a>Ausführen von Skripts  
Sie können ein Skript oder die einzelnen Anweisungen in ausführen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Zum Ausführen eines Skripts**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen** , und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), suchen und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Um das vollständige Skript auszuführen, drücken Sie die **F5** Schlüssel.  
  
4.  Um eine Reihe von Anweisungen auszuführen, wählen Sie die Anweisungen im Abfrage-Editor-Fenster, und drücken Sie dann die **F5** Schlüssel.  
  
Weitere Informationen zum Abfrage-Editor zu verwenden, um Skripts auszuführen, finden Sie unter "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] Abfrage" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
Sie können Skripts auch über die Befehlszeile ausführen, mit der **Sqlcmd** -Dienstprogramm und von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Weitere Informationen zu **Sqlcmd**, finden Sie unter "Sqlcmd (Hilfsprogramm)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online. Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent, finden Sie unter "Automatisieren von Verwaltungsaufgaben ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent)" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="securing-objects-in-sql-server"></a>Sichern von Objekten in SQLServer  
Nachdem Sie die konvertierte Datenbankobjekte in geladen haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie können die GRANT- und deny-Berechtigungen für diese Objekte. Es ist eine gute Idee, führen Sie dies vor dem Migrieren von Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Für finden Sie Informationen zum Sichern in Objekte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter "Security Considerations für Datenbanken und Datenbankanwendungen" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [Migrieren von Daten in SQL Server](http://msdn.microsoft.com/en-us/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

