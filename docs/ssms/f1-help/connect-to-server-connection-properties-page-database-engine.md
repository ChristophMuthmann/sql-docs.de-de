---
title: Verbinden mit SQL Server-Datenbankmodul (Eigenschaftenseite Verbindung) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttoce.connectionproperties.f1
- sql13.swb.connecttosqlserver.connectionproperties.f1
ms.assetid: edc1143c-6a47-4b02-92ab-441bdea8ea8a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 22cef3465036947ad6389b41c4c80bfc5ef965cb
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-connection-properties-page-database-engine"></a>Verbinden mit SQL Server-Datenbankmodul (Eigenschaftenseite Verbindung)
Auf dieser Registerkarte können Optionen für Verbindungen mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] angezeigt oder angegeben werden, oder Sie können mit dieser Registerkarte [!INCLUDE[ssDE](../../includes/ssde_md.md)] in **Registrierte Server** registrieren. Die Felder**Verbinden** und **Optionen** werden nur beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde_md.md)]in diesem Dialogfeld angezeigt. Die Felder**Testen** und **Speichern** werden nur beim Registrieren von [!INCLUDE[ssDE](../../includes/ssde_md.md)]in diesem Dialogfeld angezeigt.  
  
## <a name="options"></a>Optionen  
**Verbindung mit Datenbank herstellen**  
Wählen Sie eine Datenbank aus der Liste aus, zu der eine Verbindung hergestellt werden soll. Wenn Sie **<default>**auswählen, wird eine Verbindung zur Standarddatenbank des Servers hergestellt. Wenn Sie **<Browse server>**auswählen, können Sie den Server nach der Datenbank durchsuchen, mit der Sie eine Verbindung herstellen möchten.  
  
Wenn Sie über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] eine Verbindung mit einer Instanz des [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)]-Datenbankmoduls herstellen, müssen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Authentifizierung verwenden und im Dialogfeld **Verbindung mit Server herstellen** auf der Registerkarte **Verbindungseigenschaften** eine Datenbank angeben. Das Kontrollkästchen **Verbindung verschlüsseln** muss aktiviert sein.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] stellt standardmäßig eine Verbindung mit der **master**-Datenbank her. Wenn Sie eine Benutzerdatenbank angeben, wird im Objekt-Explorer nur diese Datenbank mit den zugehörigen Objekten angezeigt. Wenn Sie eine Verbindung mit der **master**-Datenbank herstellen, werden alle Datenbanken angezeigt. Weitere Informationen finden Sie in der [Übersicht zu Windows Azure SQL-Datenbanken](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Netzwerkprotokoll**  
Wählen Sie ein Protokoll aus der Liste aus. Die verfügbaren Clientprotokolle sind diejenigen, die Sie mithilfe der Netzwerkkonfiguration des Clients in der Computerverwaltung konfiguriert haben.  
  
**Netzwerkpaketgröße**  
Geben Sie die Größe der zu sendenden Netzwerkpakete ein. Der Standardwert ist 4096 (Bytes).  
  
**Verbindungstimeout**  
Geben Sie an, wie lange (in Sekunden) versucht werden soll, eine Verbindung herzustellen, bevor ein Timeout eintritt. Der Standardwert beträgt 15 Sekunden.  
  
**Ausführungstimeout**  
Geben Sie an, wie lange (in Sekunden) auf den Abschluss eines Tasks auf dem Server gewartet werden soll. Der Standardwert beträgt null Sekunden, d. h. es wird kein Timeout verwendet.  
  
**Verbindung verschlüsseln**  
Erzwingt die Verschlüsselung der Verbindung.  
  
**Benutzerdefinierte Farbe verwenden**  
Wählen Sie diese Option aus, um die Hintergrundfarbe für die Statusleiste in einem [!INCLUDE[ssDE](../../includes/ssde_md.md)] -Abfrage-Editor-Fenster anzugeben. Um die Farbe anzugeben, klicken Sie auf **Auswählen**. Wählen Sie im Dialogfeld **Farbe** eine vordefinierte Farben aus der Tabelle **Grundfarben** aus, oder klicken Sie auf **Benutzerdefinierte Farben** , um eine benutzerdefinierte Farbe zu definieren und zu verwenden.  
  
-   Wenn Sie eine Farbe für einen Servereintrag im Bereich **Objekt-Explorer** angeben, wird diese Farbe verwendet, wenn Sie ein Abfrage-Editor-Fenster öffnen. Um ein Abfrage-Editor-Fenster zu öffnen, klicken Sie entweder mit der rechten Maustaste auf den Servereintrag, und wählen Sie **Neue Abfrage**, oder – wenn der Bereich **Objekt-Explorer** aktiv und auf diesen Server fokussiert ist – klicken Sie auf der Symbolleiste auf **Neue Abfrage** .  
  
-   Wenn Sie eine Farbe für einen Servereintrag im Bereich **Registrierte Server** angeben, wird diese Farbe verwendet, wenn Sie ein Abfrage-Editor-Fenster öffnen. Um ein Abfrage-Editor-Fenster zu öffnen, klicken Sie entweder mit der rechten Maustaste auf den Servereintrag, und wählen Sie **Neue Abfrage**, oder – wenn der Bereich **Registrierte Server** aktiv und auf diesen Server fokussiert ist – klicken Sie auf der Symbolleiste auf **Neue Abfrage** .  
  
-   Wenn Sie im Menü **Datei** auf **Neu** und dann auf **Datenbankmodul-Abfrage**klicken, wird die Farbe, die Sie im Dialogfeld **Verbindung mit Server herstellen** angeben, für dieses Abfrage-Editor-Fenster übernommen.  
  
**Alles zurücksetzen**  
Ersetzt alle manuell eingegebenen Verbindungseigenschaftswerte durch die Standardwerte.  
  
**Verbinden**  
Versucht, mithilfe der aufgelisteten Werte eine Verbindung herzustellen.  
  
**Optionen**  
Klicken Sie hier, um die Anzeige des Dialogfelds zu ändern und die zusätzlichen Serververbindungsoptionen, z. B. Speichern des Kennworts, auszublenden.  
  
**Testenen**  
Klicken Sie hier, um beim Registrieren von [!INCLUDE[ssDE](../../includes/ssde_md.md)] in **Registrierte Server**die Verbindung zu testen.  
  
**Speichern**  
Speichert die Einstellungen in **Registrierte Server**.  
  
## <a name="see-also"></a>Siehe auch  
[Verbindungseigenschaften (Dialogfeld)](../../ssms/f1-help/connection-properties-dialog-box.md)  
  

