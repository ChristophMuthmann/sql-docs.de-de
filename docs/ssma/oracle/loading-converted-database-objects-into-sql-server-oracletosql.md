---
title: Laden konvertierte Objekte in SQLServer (OracleToSQL) Datenbank | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6fd5616c61af419d5d2ff3134177ae296b317d57
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>Laden konvertierte Objekte in SQLServer (OracleToSQL) Datenbank
Nachdem Sie die Oracle-Schemas in SQL Server konvertiert haben, können Sie die resultierende Datenbankobjekte in SQL Server laden. Kann entweder über die SSMA, die die Objekte zu erstellen, oder können Sie Skripts für die Objekte und führen Sie die Skripts selbst. Darüber hinaus können mit SSMA Sie Metadaten durch den tatsächlichen Inhalt der SQL Server-Datenbank zu aktualisieren.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Auswählen zwischen Synchronisierung und Skripts  
Wenn Sie die konvertierte Datenbankobjekte ohne Änderungen in SQL Server laden möchten, haben Sie SSMA direkt erstellen oder Neuerstellen von Datenbankobjekten. Dass die Methode lässt sich schnell und einfach, lässt jedoch keine Anpassung der [!INCLUDE[tsql](../../includes/tsql_md.md)] Code, der die SQL Server-Objekte als gespeicherte Prozeduren definiert.  
  
Wenn Sie ändern möchten die [!INCLUDE[tsql](../../includes/tsql_md.md)] , der zum Erstellen von Objekten oder wenn Sie mehr Kontrolle über die Objekte erstellen möchten, verwenden SSMA zum Erstellen von Skripts verwendet wird. Sie können dann diese Skripts ändern, jedes Objekt einzeln erstellen und auch mit der SQL Server-Agent planen, diese Objekte zu erstellen.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Mithilfe von SSMA zum Synchronisieren von Objekten mit SQLServer  
Um SSMA verwenden, um SQL Server-Datenbankobjekte zu erstellen, wählen Sie die Objekte in SQL Server-Metadaten-Explorer, und synchronisieren Sie die Objekte mit SQL Server, wie im folgenden Verfahren gezeigt. Standardmäßig wird, wenn die Objekte in SQL Server bereits vorhanden sind, und wenn die SSMA-Metadaten neuer ist als das Objekt in SQL Server, SSMA die Objektdefinitionen in SQL Server geändert werden. Sie können das Standardverhalten ändern, indem Sie die Bearbeitung **Projekteinstellungen**.  
  
> [!NOTE]  
> Sie können vorhandene SQL Server-Datenbankobjekte auswählen, die aus Oracle-Datenbanken nicht konvertiert wurden. Allerdings werden diese Objekte nicht neu erstellt oder geändert werden von SSMA.  
  
**Zum Synchronisieren von Objekten mit SQL Server**  
  
1.  In SQL Server-Metadaten-Explorer, erweitern Sie den obersten Knoten des SQL Server, und dann **Datenbanken**.  
  
2.  Wählen Sie die zu verarbeitenden Objekte aus:  
  
    -   Um eine gesamte Datenbank zu synchronisieren, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zu synchronisieren, oder lassen Sie einzelne Objekte oder Kategorien von Objekten, aktivieren Sie, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt oder einen Ordner aus.  
  
3.  Nachdem Sie die zu verarbeitenden in SQL Server-Metadaten-Explorer Objekte ausgewählt haben, mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
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
  
2.  In der **speichern unter** Dialogfeld Suchen den Ordner, in dem Sie speichert das Skript in einen Dateinamen eingeben möchten, die **Dateiname** Feld, und klicken Sie dann auf OK SSMA wird die SQL-Dateinamenerweiterung angefügt.  
  
### <a name="modifying-scripts"></a>Ändern von Skripts  
Nachdem Sie die SQL Server-Objektdefinitionen als ein oder mehrere Skripts gespeichert haben, können Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] anzeigen und ändern Sie die Skripts.  
  
**So ändern Sie ein Skript**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), wählen Sie Ihre Skriptdatei, und klicken Sie auf OK.
  
3.  Bearbeiten Sie die Skriptdatei, mit dem Abfrage-Editor.  
  
    Weitere Informationen zu den Abfrage-Editor finden Sie unter "Editor halber Befehle und Funktionen" in der SQL Server-Onlinedokumentation.  
  
4.  So speichern Sie das Skript auf im Menü Datei auf **speichern**.  
  
### <a name="running-scripts"></a>Ausführen von Skripts  
Sie können ein Skript oder die einzelnen Anweisungen in ausführen [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Zum Ausführen eines Skripts**  
  
1.  Auf der [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  In der **öffnen** (Dialogfeld), wählen Sie Ihre Skriptdatei, und klicken Sie dann auf OK  
  
3.  Um das vollständige Skript auszuführen, drücken Sie die **F5** Schlüssel.  
  
4.  Um eine Reihe von Anweisungen auszuführen, wählen Sie die Anweisungen im Abfrage-Editor-Fenster, und drücken Sie dann die **F5** Schlüssel.  
  
Weitere Informationen zum Abfrage-Editor zu verwenden, um Skripts auszuführen, finden Sie unter "[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] Abfrage" in SQL Server-Onlinedokumentation.  
  
Sie können Skripts auch über die Befehlszeile ausführen, mit der **Sqlcmd** -Hilfsprogramm und aus der SQL Server-Agent. Weitere Informationen zu **Sqlcmd**, finden Sie unter "Sqlcmd (Hilfsprogramm)" in SQL Server-Onlinedokumentation. Weitere Informationen zu SQL Server-Agent finden Sie unter "Automatisieren von Verwaltungsaufgaben (SQL Server-Agent)" in SQL Server-Onlinedokumentation.  
  
## <a name="securing-objects-in-sql-server"></a>Sichern von Objekten in SQLServer  
Nachdem Sie die konvertierte Datenbankobjekte in SQL Server geladen haben, können Sie die GRANT- und deny-Berechtigungen für diese Objekte. Es ist eine gute Idee, führen Sie dies vor dem Migrieren von Daten in SQL Server. Informationen zu sicheren Objekte in SQL Server zu schützen finden Sie unter "Security Considerations for Datenbanken und Datenbank Applications" in SQL Server-Onlinedokumentation.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Migrieren von Daten in SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

