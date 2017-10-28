---
title: "Vorbereiten von Access-Datenbanken für die Migration (AccessToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
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
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
caps.latest.revision: 20
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: 0d94578759156dcde898a23267fb91922fc98b03
ms.contentlocale: de-de
ms.lasthandoff: 08/16/2017

---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>Vorbereiten von Access-Datenbanken für die Migration (AccessToSQL)
Vor dem Migrieren von Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], müssen Sie feststellen, welche Datenbanken zu migrieren, und stellen Sie sicher, dass diese Datenbanken für die Migration bereit sind.  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>Wann sollten Migration zu SQL Server  
Das Jet-Datenbankmodul, die als das Datenbankmodul für den Zugriff verwendet wird, ist eine flexible, leicht zu verwendende Lösung für die datenverwaltung. Allerdings finden viele Benutzer als Datenbanken, die umfangreicher und weitere unternehmenskritisch, bessere Leistung, Sicherheit oder Verfügbarkeit erfordern. Anwendungen, eine robustere Datenplattform erfordern, erwägen Sie die zugrunde liegenden Datenbanken für diese Anwendungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen zu entscheiden, wann eine Migration, finden Sie unter der [Migration-Informationsseite](http://go.microsoft.com/fwlink/?LinkId=68571) auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Website.  
  
Nach dem Migrieren von Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie weiterhin Zugriff mithilfe von verknüpften Tabellen verwenden oder Sie können manuell migrieren Ihrer Anwendungen auf [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework-basierten Code, der direkt mit interagiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="determining-which-databases-to-migrate"></a>Bestimmen die zu migrierenden Datenbanken  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) for Access kann den Zugriff auf Datenbanken gesucht. Sie können dann exportieren Sie Metadaten zu diesen Datenbanken dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Weitere Informationen zum Exportieren und Abfragen von Metadaten finden Sie unter [exportieren eine Inventur Zugriff](http://msdn.microsoft.com/7e1941fb-3d14-4265-aff6-c77a4026d0ed).  

   > [!NOTE]
   > Nicht alle Funktionen für Zugriff und Einstellungen von unterstützt werden oder können problemlos konvertiert werden können, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Vor der Migration von Datenbanken finden Sie unter [inkompatible Zugriffsfeatures](http://msdn.microsoft.com/99d45b9c-e3b9-4d56-8c25-b594b887ace1).
  
## <a name="preparing-for-migration"></a>Vorbereiten der migration  
Verwenden Sie die folgenden Richtlinien um zu Access-Datenbanken für die Migration zu erklären [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="upgrading-older-access-databases"></a>Aktualisieren von älteren Access-Datenbanken  
SSMA für Access unterstützt Access 97 und höher. Wenn Sie Datenbanken aus früheren Versionen von Access haben, öffnen Sie, und speichern Sie die Datenbanken in Access 97 oder höher.  
  
### <a name="removing-workgroup-protection"></a>Entfernen des Schutzes von Arbeitsgruppe  
SSMA kann keine Datenbanken migrieren, die Arbeitsgruppe Schutz verwenden. Zum Schutz von Arbeitsgruppen aus einer Access-Datenbank zu entfernen, führen Sie die folgenden Schritte aus:  
  
1.  Kopieren Sie die Access-Datenbankdatei an einen anderen Speicherort aus.  
  
2.  Öffnen Sie die kopierte Datenbank an.  
  
3.  Auf der **Tools** Sie im Menü **Sicherheit**, und wählen Sie dann **Benutzer- und Gruppenberechtigungen**.  
  
4.  Wählen Sie die **Benutzer** aus, Aktivieren der **Admin** Benutzer, und dann sicherstellen, dass die **verwalten** Berechtigung ausgewählt ist.  
  
5.  Wählen Sie die **Gruppen** aus, Aktivieren der **Benutzer** gruppieren und dann sicherstellen, dass die **verwalten** Berechtigung ausgewählt ist.  
  
6.  Klicken Sie auf **OK**, und klicken Sie dann auf die **Datei** Menü klicken Sie auf **beenden**.  
  
SSMA können jetzt um die kopierte Datenbank zu migrieren. Laden Sie das Schema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie die Datenbank manuell auf Sperren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="backing-up-databases"></a>Sichern von Datenbanken  
Vor dem Migrieren der Access-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sichern Sie sowohl die Access-Datenbanken, die Sie migrieren, sowie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbanken Sie in den migrieren Zugriff auf Objekte und Daten.  
  
Zum Sichern einer Access-Datenbank, auf die **Tools** Sie im Menü **-Datenbankdienstprogramme**, und wählen Sie dann **Datenbank sichern**.  
  
Informationen zum Sichern von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datenbanken finden Sie unter "Sichern und Wiederherstellen von Datenbanken in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]" in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Books Online.  
  
### <a name="documenting-databases"></a>Dokumentieren von Datenbanken  
Sie sollten auch die Eigenschaften, z. B. Listen von Datenbankobjekten, Dateigrößen und Berechtigungen, die von Access-Datenbanken zu dokumentieren. Zum Generieren dieser Dokumentation in Access wird für die **Tools** Sie im Menü **analysieren**, und klicken Sie dann auf **dokumentierte**.  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Verknüpfen von Access-Anwendungen mit SQLServer](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)

