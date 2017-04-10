---
title: "Konfigurieren der Transformation f&#252;r OLE DB-Befehl | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Parameter [Integration Services]"
  - "Transformation für OLE DB-Befehl"
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Konfigurieren der Transformation f&#252;r OLE DB-Befehl
  Das Paket muss bereits mindestens einen Datenflusstask und eine Quelle, wie z. B. eine Flatfilequelle oder eine OLE DB-Quelle, einschließen, damit Sie eine Transformation für OLE DB-Befehl hinzufügen und konfigurieren können. Diese Transformation wird normalerweise zum Ausführen parametrisierter Abfragen verwendet.  
  
### So konfigurieren Sie die Transformation für OLE DB-Befehl  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Fenster **Toolbox**die Transformation für OLE DB-Befehl auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für OLE DB-Befehl mit dem Datenfluss, indem Sie einen Konnektor (der grüne oder rote Pfeil) von einer Datenquelle oder einer vorherigen Transformation mit der Maus auf die Transformation für OLE DB-Befehl ziehen.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Komponente, und wählen Sie „Bearbeiten“ oder **Erweiterten Editor anzeigen** aus.  
  
6.  Wählen Sie auf der Registerkarte **Verbindungs-Manager** in der Liste **Verbindungs-Manager** einen OLE DB-Verbindungs-Manager aus. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Klicken Sie auf die Registerkarte **Komponenteneigenschaften**, und klicken Sie im Feld **SqlCommand** auf die Schaltfläche mit den drei Punkten (**…**).  
  
8.  Geben Sie in **Zeichenfolgenwert-Editor** die parametrisierte SQL-Anweisung mithilfe eines Fragezeichens (?) als Parametermarkierung für jeden Parameter ein.  
  
9. Klicken Sie auf **Aktualisieren**. Wenn Sie auf **Aktualisieren** klicken, erstellt die Transformation eine Spalte für jeden Parameter in der Sammlung externer Spalten und legt die DBParamInfoFlags-Eigenschaft fest.  
  
10. Klicken Sie auf die Registerkarte **Eingabe- und Ausgabeeigenschaften** .  
  
11. Erweitern Sie **Eingabe des OLE DB-Befehls**und anschließend **Externe Spalten**.  
  
12. Überprüfen Sie, ob **Externe Spalten** eine Spalte für jeden Parameter in der SQL-Anweisung auflistet. Die Spaltennamen lauten **Param_0**, **Param_1** usw.  
  
     Die Spaltennamen sollten nicht geändert werden. Wenn Sie die Spaltennamen ändern, generiert [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] einen Überprüfungsfehler für die Transformation für den OLE DB-Befehl.  
  
     Der Datentyp sollte auch nicht geändert werden. Die DataType-Eigenschaft der einzelnen Spalten wird auf den entsprechenden Datentyp festgelegt.  
  
13. Falls **Externe Spalten** keine Spalten auflistet, müssen sie manuell hinzugefügt werden.  
  
    -   Klicken Sie für jeden Parameter in der SQL-Anweisung einmal auf **Spalte hinzufügen** .  
  
    -   Aktualisieren Sie die Spaltennamen auf **Param_0**, **Param_1** usw.  
  
    -   Geben Sie einen Wert in der DBParamInfoFlags-Eigenschaft an. Der Wert muss mit einem Wert in der OLE DB-Enumeration DBPARAMFLAGSENUM übereinstimmen. Weitere Informationen finden Sie in der OLE DB-Referenzdokumentation.  
  
    -   Geben Sie den Datentyp der Spalte und, in Abhängigkeit vom Datentyp, die Codepage, die Länge, die Genauigkeit und die Dezimalstellen der Spalte an.  
  
    -   Wenn Sie einen nicht verwendeten Parameter löschen möchten, wählen Sie den Parameter in **Externe Spalten**aus, und klicken Sie auf **Spalte entfernen**.  
  
    -   Klicken Sie auf **Spaltenzuordnungen** , und ordnen Sie Spalten in der Liste **Verfügbare Eingabespalten** Parametern in der Liste **Verfügbare Zielspalten** zu.  
  
14. Klicken Sie auf **OK**.  
  
15. Klicken Sie im Menü **Datei** auf **Speichern** , um das aktualisierte Paket zu speichern.  
  
## Siehe auch  
 [Transformation für OLE DB-Befehl](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [SQL Server Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  