---
title: Installieren SSMA-Komponenten auf SQLServer (MySQLToSql) | Microsoft Docs
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
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9544fb62402871b9a93284df88e0082f62fec582
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Installieren SSMA-Komponenten auf SQLServer (MySQLToSql)
Neben der Installation von SSMA, müssen Sie auch Komponenten installieren, auf dem Computer, auf denen ausgeführt wird, ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Zu diesen Komponenten gehören das Pack der SSMA-Erweiterung, das Datenmigration und MySQL-Anbieter auf Server-zu-Server-Verbindung aktivieren unterstützt.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA für die MySQL-Erweiterung Pack  
Das SSMA-Erweiterung Pack Fügt eine Datenbank, **Sysdb**, mit der angegebenen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Diese Datenbank enthält die Tabellen und gespeicherten Prozeduren, die zum Migrieren von Daten erforderlich sind.  
  
Darüber hinaus beim Migrieren von Daten zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA erstellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Aufträge, wenn Server-Seite-Migration Datenmodul zum Migrieren Ihrer Daten verwendet wird.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Vor der Installation von SSMA für MySQL Server-Komponenten auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], stellen Sie sicher, dass der Computer die folgenden Anforderungen erfüllt:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 oder höher.  
  
-   Die MySQL-Client-Anbieter, und die Konnektivität mit der MySQL-Datenbank, die Sie migrieren möchten. Sie können den Anbieter aus der MySQL-Produktmedien oder MySQL-Website installieren.  
  
-   Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst muss ausgeführt werden, während der Installation. Wird verwendet, um eine Liste der Instanzen des Auffüllen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] im Setup-Assistenten. Sie können Deaktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst nach der Installation.  
  
    > [!NOTE]  
    > Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst ausgeführt wird, aber Sie noch nicht sehen, dass eine Liste von Instanzen im Setup, müssen Sie die Blockierung aufheben UDP-Port 1434. Können Sie Windows-Firewall vorübergehend Entsperren des Ports ein, oder Sie können die Windows-Firewall vorübergehend deaktivieren. Möglicherweise müssen auch die Antivirensoftware vorübergehend deaktivieren. Stellen Sie sicher, dass Firewalls und antivirus-Software nach der Installation aktivieren.  
  
### <a name="installing-the-extension-pack"></a>Installieren der Erweiterung-Pakets  
Sie können einem beliebigen Zeitpunkt vor dem Migrieren von Daten an, das Erweiterung Pack installieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Um die Erweiterung Pack zu installieren, muss ein Mitglied der **Sysadmin** -Serverrolle auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**So installieren Sie die Erweiterung pack**  
  
1.  Kopieren Sie SSMA für MySQL-Erweiterung Pack. *n*. Install.exe, wobei  *n*  ist, auf dem Computer, auf denen ausgeführt wird, die Nummer des Builds [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Doppelklicken Sie SSMA für MySQL-Erweiterung Pack ein. *n*. Install.exe.  
  
3.  Klicken Sie im Dialogfeld "Willkommen" auf **Weiter**.  
  
4.  Lesen Sie den Lizenzvertrag, klicken Sie im Dialogfeld Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, Aktivieren der **ich stimme den Bedingungen des Lizenzvertrags** Kontrollkästchen, und klicken Sie dann auf **Weiter**.  
  
5.  Klicken Sie auf die Installationsart auswählen-Dialogfeld auf **typisch**.  
  
6.  Klicken Sie auf der kann jetzt zu installieren (Dialogfeld), auf **installieren**.  
  
7.  Klicken Sie auf die im Dialogfeld erste Schritt der Installation abgeschlossen auf **Weiter**.  
  
    Ein neues Dialogfeld wird angezeigt, in dem Sie die Instanz von auswählen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] für die Erweiterung Paketinstallation.  
  
8.  Wählen Sie die Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , in dem Sie migrieren von MySQL-Schemas, und klicken Sie dann auf **Weiter**.  
  
    Die Standardinstanz hat den gleichen Namen wie der Computer an. Benannte Instanzen werden ein umgekehrter Schrägstrich und der Instanzname folgt.  
  
9. Klicken Sie im Dialogfeld Verbindung wählen Sie die Authentifizierungsmethode aus, und klicken Sie dann auf **Weiter**.  
  
    Windows-Authentifizierung wird Windows-Anmeldeinformationen verwenden, um zu versuchen, melden Sie sich mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Bei Auswahl des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldename und Kennwort.  
  
10. Wählen Sie im nächsten Dialogfeld **Utilities-Datenbank installieren**  *n* , wobei  *n*  ist die Versionsnummer, und klicken Sie dann auf **Weiter**.  
  
    Die **Sysdb** Datenbank mit den Tabellen und gespeicherte Prozeduren, die für die Datenmigration (mit Server-Seite-Migration Datenmodul) erforderlich sind in dieser Datenbank erstellt.  
  
11. So installieren Sie die Dienstprogramme in eine andere Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Option **Ja**, und klicken Sie dann auf **Weiter**. Um den Assistenten zu beenden, klicken Sie auf **keine**.  
  
## <a name="see-also"></a>Siehe auch  
[Installieren SSMA für MySQL-Client &#40; MySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

