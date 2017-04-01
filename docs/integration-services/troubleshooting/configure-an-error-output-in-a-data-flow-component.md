---
title: "Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Fehler [Integration Services], Datenflusskomponenten"
  - "Komponenten [Integration Services], Datenfluss"
  - "Fehlerausgaben [Integration Services]"
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# Konfigurieren einer Fehlerausgabe in einer Datenflusskomponente
  Viele Datenflusskomponenten unterstützen Fehlerausgaben, und [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer bietet je nach Komponente unterschiedliche Möglichkeiten für die Konfiguration einer Fehlerausgabe. Sie können nicht nur eine Fehlerausgabe, sondern auch die Spalten einer Fehlerausgabe konfigurieren. Dies schließt das Konfigurieren der von der Komponente hinzugefügten Spalten **ErrorCode** und **ErrorColumn** ein.  
  
## Konfigurieren einer Fehlerausgabe  
 Zum Konfigurieren einer Fehlerausgabe stehen Ihnen zwei Optionen zur Verfügung:  
  
-   Verwenden des Dialogfelds **Fehlerausgabe konfigurieren** . Sie können dieses Dialogfeld zum Konfigurieren einer Fehlerausgabe für jede Datenflusskomponente verwenden, die eine Fehlerausgabe unterstützt.  
  
-   Verwenden des Editordialogfelds für die Komponente. Die Fehlerausgaben können bei einigen Komponenten direkt in ihrem Editordialogfeld konfiguriert werden. Es ist jedoch nicht möglich, Fehlerausgaben im Editordialogfeld für die ADO NET-Quelle, die Transformation für das Importieren von Spalten, die Transformation für OLE DB-Befehl oder das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact-Ziel zu konfigurieren.  
  
 Im Folgenden wird die Verwendung dieser Dialogfelder zum Konfigurieren von Fehlerausgaben beschrieben.  
  
#### So konfigurieren Sie eine Fehlerausgabe mit dem Dialogfeld "Fehlerausgabe konfigurieren"  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Datenfluss** .  
  
4.  Ziehen Sie die Fehlerausgabe, dargestellt durch einen roten Pfeil, von der Komponente, die die Fehlerquelle darstellt, zu einer anderen Komponente im Datenfluss.  
  
5.  Wählen Sie im Dialogfeld **Fehlerausgabe konfigurieren** eine Aktion in den Spalten **Fehler** und **Abschneiden** für jede Spalte der Komponenteneingabe.  
  
6.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
#### So fügen Sie eine Fehlerausgabe mit dem Editordialogfeld für die Komponente hinzu  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Datenfluss** .  
  
4.  Doppelklicken Sie auf die Datenflusskomponenten, für die Sie eine Fehlerausgabe konfigurieren möchten, und führen Sie je nach Komponente einen der folgenden Schritte durch:  
  
    -   Klicken Sie auf **Fehlerausgabe konfigurieren**.  
  
    -   Klicken Sie auf **Fehlerausgabe**.  
  
5.  Legen Sie für jede Spalte die Option **Fehler** fest.  
  
6.  Legen Sie für jede Spalte die Option **Abschneiden** fest.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
## Konfigurieren von Fehlerausgabespalten  
 Verwenden Sie die Registerkarte **Eingabe- und Ausgabeeigenschaften** im Dialogfeld **Erweiterter Editor** zum Konfigurieren von Fehlerausgabespalten.  
  
#### So konfigurieren Sie Fehlerausgabespalten  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer auf die Registerkarte **Datenfluss** .  
  
4.  Klicken Sie mit der rechten Maustaste auf die Komponente, deren Fehlerausgabespalten Sie konfigurieren möchten, und klicken Sie auf **Erweiterten Editor anzeigen**.  
  
5.  Klicken Sie auf die Registerkarte **Eingabe- und Ausgabeeigenschaften**, und erweitern Sie **\<Komponentenname> Fehlerausgabe** und dann **Ausgabespalten**.  
  
6.  Klicken Sie auf eine Spalte, und aktualisieren Sie ihre Eigenschaften.  
  
    > [!NOTE]  
    >  Die Liste mit den Spalten enthält die Spalten in der Komponenteneingabe, die durch vorherige Fehlerausgaben hinzugefügten Spalten **ErrorCode** und **ErrorColumn** sowie die von dieser Komponente hinzugefügten Spalten **ErrorCode** und **ErrorColumn**.  
  
7.  Klicken Sie auf **OK.**  
  
8.  Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern**, um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
  