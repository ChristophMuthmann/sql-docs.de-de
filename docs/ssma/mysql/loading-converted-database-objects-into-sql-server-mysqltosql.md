---
title: Laden konvertierte Objekte in SQLServer (MySQLToSQL) Datenbank | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
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
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc70aebab39bc1d60f6b6e933f53d9f32cb87d6e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>Laden konvertierte Objekte in SQLServer (MySQLToSQL) Datenbank
Nachdem Sie die MySQL-Datenbanken zu konvertiert haben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, laden Sie die resultierende Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Kann entweder über die SSMA, die die Objekte zu erstellen, oder können Sie Skripts für die Objekte und führen Sie die Skripts selbst. Darüber hinaus SSMA können Sie die Ziel-Metadaten mit dem tatsächlichen Inhalt aktualisieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbank.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Auswählen zwischen Synchronisierung und Skripts  
Wenn Sie die konvertierte Datenbankobjekte in laden möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure ohne Änderung haben Sie SSMA direkt erstellen oder Neuerstellen von Datenbankobjekten. Dass die Methode lässt sich schnell und einfach, lässt jedoch keine für die Anpassung von der Transact-SQL-Code, definiert die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Objekte.  
  
Verwenden Sie Transact-SQL zu ändern, die zum Erstellen von Objekten verwendet werden sollen, oder wenn Sie mehr Kontrolle über die Objekte erstellen möchten, SSMA zum Erstellen von Skripts. Sie können diese Skripts ändern, klicken Sie dann jedes Objekt einzeln erstellen und sogar mit der SQL Server-Agent planen, diese Objekte erstellt.  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>Mithilfe von SSMA zum Synchronisieren von Objekten mit SQLServer  
Um SSMA SQL Server- bzw. SQL Azure-Datenbankobjekte erstellen, wählen Sie die Objekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Metadaten-Explorer, und synchronisieren Sie die Objekte mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, wie im folgenden Verfahren gezeigt. Standardmäßig, wenn die Objekte noch im vorhanden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und wenn die SSMA-Metadaten umfasst, einige lokale Änderungen oder Updates der Definition dieser Objekte sehr, SSMA werden die Objektdefinitionen in alter [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können das Standardverhalten ändern, indem Sie die Bearbeitung **Projekteinstellungen**.  
  
> [!NOTE]  
> Sie können auswählen, vorhandene [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Datenbankobjekte, die vom MySQL-Datenbanken nicht konvertiert wurden. Allerdings werden diese Objekte nicht neu erstellt oder geändert werden von SSMA.  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>Zum Synchronisieren von Objekten mit SQL Server oder SQL Azure  
  
1.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure Metadaten-Explorer, erweitern im oberen Bereich [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Knoten, und erweitern Sie dann **Datenbanken**.  
  
2.  Wählen Sie die zu verarbeitenden Objekte aus:  
  
    -   Um eine gesamte Datenbank zu synchronisieren, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
    -   Zu synchronisieren, oder lassen Sie einzelne Objekte oder Kategorien von Objekten, aktivieren Sie, oder deaktivieren Sie das Kontrollkästchen neben dem Objekt oder einen Ordner aus.  
  
3.  Nachdem Sie die zu verarbeitenden in SQL Server oder SQL Azure-Metadaten-Explorer Objekte ausgewählt haben, mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Sie können auch die einzelne Objekte oder Kategorien von Objekten synchronisieren, indem das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und klicken Sie dann auf **mit Datenbank synchronisieren**.  
  
    Danach SSMA zeigt die **mit Datenbank synchronisieren** im Dialogfeld, in dem zwei Gruppen von Elementen angezeigt. Auf der linken Seite zeigt SSMA ausgewählte Datenbankobjekte in einer Struktur dargestellt. Auf der rechten Seite sehen Sie eine Struktur, die dieselben Objekte in SSMA Metadaten darstellt. Sie können die Struktur durch Klicken auf Links oder rechts erweitern Schaltfläche "+". Die Richtung der Synchronisierung wird in der Spalte Aktion, die zwischen den beiden Strukturen angeordnet wurden, angezeigt.  
  
    Eine Aktion anmelden können die folgenden drei Zustände aufweisen:  
  
    -   Eine nach-links-Taste bedeutet, dass der Inhalt der Metadaten in der Datenbank (Standard) gespeichert werden.  
  
    -   Ein Pfeil nach rechts hindurch Datenbankinhalte SSMA Metadaten überschrieben werden.  
  
    -   Ein Kreuz bedeutet, dass keine Aktion durchgeführt wird.  
  
    -   Klicken Sie auf den Aktion-Anmeldenamen, um den Status zu ändern. Tatsächliche Synchronisierung wird durchgeführt, wenn Sie auf **OK** Schaltfläche der **mit Datenbank synchronisieren** Dialogfeld.  
  
## <a name="scripting-objects"></a>Skripterstellung für Objekte  
Speichern [!INCLUDE[tsql](../../includes/tsql_md.md)] Definitionen der konvertierten Datenbankobjekte, um die Objektdefinitionen ändern und Ausführen von Skripts selbst, können Sie speichern die konvertierte Datenbank Definitionen von Systemobjekten, [!INCLUDE[tsql](../../includes/tsql_md.md)] Skripts.  
  
**Zum Speichern von Objekten wie Skripts**  
  
1.  Nachdem Sie die Objekte in einem Skript speichern ausgewählt haben, mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **speichern als Skript**.  
  
    Sie können auch einzelne Objekte oder Kategorien von Objekten durch das Objekt oder der übergeordnete Ordner mit der rechten Maustaste, und klicken Sie dann auf schreiben **speichern als Skript**.  
  
2.  In der **speichern unter** Dialogfeld Suchen den Ordner, in dem Sie speichert das Skript in einen Dateinamen eingeben möchten, die **Dateiname** Feld, und klicken Sie dann [!INCLUDE[clickOK](../../includes/clickok_md.md)] SSMA wird die SQL-Dateinamenerweiterung angefügt.  
  
### <a name="modifying-scripts"></a>Ändern von Skripts  
Nachdem Sie die SQL Server- oder SQL Azure-Objektdefinitionen als Skript gespeichert haben, können Sie SQL Server Management Studio, das Skript ändern.  
  
**So ändern Sie ein Skript**  
  
1.  Management Studio **Datei** Sie im Menü **öffnen**, und klicken Sie dann auf **Datei**.  
  
2.  Klicken Sie im Dialogfeld "Öffnen" suchen, und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Bearbeiten Sie die Skriptdatei, mit dem Abfrage-Editor. Weitere Informationen zu den Abfrage-Editor finden Sie unter "Editor halber Befehle und Funktionen" in der SQL Server-Onlinedokumentation.  
  
4.  Wählen Sie zum Speichern des Skripts im Menü Datei **speichern**.  
  
### <a name="running-scripts"></a>Ausführen von Skripts  
Sie können ein Skript oder einzelne Anweisungen in SQL Server Management Studio ausführen.  
  
**Zum Ausführen eines Skripts**  
  
1.  Auf der SQL Server Management Studio **Datei** Sie im Menü **öffnen** , und klicken Sie dann auf **Datei**.  
  
2.  Klicken Sie im Dialogfeld "Öffnen" suchen, und wählen Sie Ihre Skriptdatei, und klicken Sie dann auf **OK**.  
  
3.  Um das vollständige Skript auszuführen, drücken Sie die **F5** Schlüssel.  
  
4.  Um eine Reihe von Anweisungen auszuführen, wählen Sie die Anweisungen im Abfrage-Editor-Fenster, und drücken Sie dann die **F5** Schlüssel.  
  
5.  Weitere Informationen zum Abfrage-Editor zu verwenden, um Skripts auszuführen finden Sie unter "SQL Server Management Studio Transact-SQL-Abfrage" in SQL Server-Onlinedokumentation.  
  
6.  Sie können Skripts auch über die Befehlszeile ausführen, mit der **Sqlcmd** -Hilfsprogramm und von SQL Server-Agent. Weitere Informationen zu **Sqlcmd**, finden Sie unter "Sqlcmd (Hilfsprogramm)" in SQL Server-Onlinedokumentation. Weitere Informationen zu SQL Server-Agent finden Sie unter "Automatisieren von Verwaltungsaufgaben (SQL Server-Agent)" in SQL Server-Onlinedokumentation.  
  
## <a name="securing-objects-in-sql-server"></a>Sichern von Objekten in SQLServer  
Nachdem Sie die konvertierte Datenbankobjekte in SQL Server geladen haben, können Sie GRANT- und deny-Berechtigungen für diese Objekte. Es ist eine gute Idee, führen Sie dies vor dem Migrieren von Daten in SQL Server. Informationen zu sicheren Objekte in SQL Server zu schützen finden Sie unter "Security Considerations for Datenbanken und Datenbank Applications" in SQL Server-Onlinedokumentation.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [Migrieren von MySQL-Daten in SQL Server - Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
