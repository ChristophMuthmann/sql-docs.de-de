---
title: "Transformation für OLE DB-Befehl | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 99d34e8dd153c5ca1793d14cc9638aab6529a643
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="ole-db-command-transformation"></a>Transformation für OLE DB-Befehl
  Die Transformation für OLE DB-Befehl führt eine SQL-Anweisung für jede Zeile in einem Datenfluss aus. Beispielsweise können Sie eine SQL-Anweisung ausführen, die Zeilen in einer Datenbanktabelle einfügt, aktualisiert oder löscht.  
  
 Es gibt folgende Möglichkeiten, um die Transformation für OLE DB-Befehl zu konfigurieren:  
  
-   Stellen Sie die SQL-Anweisung bereit, die die Transformation für jede Zeile ausführt.  
  
-   Geben Sie an, nach wie vielen Sekunden ein Timeout bei der SQL-Anweisung eintritt.  
  
-   Geben Sie die Standardcodepage an.  
  
 In der Regel enthält die SQL-Anweisung Parameter. Die Parameterwerte sind in externen Spalten in der Transformationseingabe gespeichert, und beim Zuordnen einer Eingabespalte zu einer externen Spalte wird eine Eingabespalte einem Parameter zugeordnet. Angenommen, Sie möchten Zeilen in der **DimProduct** -Tabelle anhand des Werts in der **ProductKey** -Spalte suchen und diese dann löschen. Hierzu können Sie die externe Spalte **Param_0** der **ProductKey** -Eingabespalte zuordnen und anschließend den SQL-Befehl `DELETE FROM DimProduct WHERE ProductKey = ?`ausführen. Die Transformation für OLE DB-Befehl stellt die Parameternamen bereit, die nicht geändert werden können. Die Parameternamen lauten **Param_0**, **Param_1**usw.  
  
 Wenn Sie die Transformation für OLE DB-Befehl mithilfe des Dialogfelds **Erweiterter Editor** konfigurieren, können die Parameter in der SQL-Anweisung automatisch externen Spalten in der Transformationseingabe zugeordnet und die Merkmale jedes Parameters definiert werden, indem Sie auf die Schaltfläche **Aktualisieren** klicken. Wenn jedoch der von der Transformation für OLE DB-Befehl verwendete OLE DB-Anbieter das Ableiten von Parameterinformationen von dem Parameter nicht unterstützt, müssen Sie die externen Spalten manuell konfigurieren. Das heißt, Sie müssen der Transformation für jeden Parameter zur externen Eingabe eine Spalte hinzufügen, die Spaltennamen aktualisieren, um Namen wie **Param_0**zu verwenden, den Wert der DBParamInfoFlags-Eigenschaft angeben sowie die Eingabespalten, die Parameterwerte enthalten, den externen Spalten zuordnen.  
  
 Der Wert von DBParamInfoFlags stellt die Merkmale des Parameters dar. Beispielsweise gibt der Wert **1** an, dass der Parameter ein Eingabeparameter ist, und der Wert **65** gibt an, dass der Parameter ein Eingabeparameter ist und einen NULL-Wert enthalten kann. Die Werte müssen mit den Werten in der OLE DB-Enumeration DBPARAMFLAGSENUM übereinstimmen. Weitere Informationen finden Sie in der OLE DB-Referenzdokumentation.  
  
 Die Transformation für OLE DB-Befehl schließt die benutzerdefinierte Eigenschaft **SQLCommand** ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Diese Transformation weist eine Eingabe, eine reguläre Ausgabe und eine Fehlerausgabe auf.  
  
## <a name="logging"></a>Protokollierung  
 Sie können die von der Transformation für OLE DB-Befehl an externe Datenanbieter gerichteten Aufrufe protokollieren. Mithilfe dieser Protokollierungsfunktion können Sie Probleme bei Verbindungen mit externen Datenquellen und bei Befehlen an externe Datenquellen durch die Transformation für OLE DB-Befehl behandeln. Aktivieren Sie zum Protokollieren der von der Transformation für OLE DB-Befehl an externe Datenanbieter gerichteten Aufrufe die Paketprotokollierung, und wählen Sie das **Diagnostic** -Ereignis auf Paketebene aus. Weitere Informationen finden Sie unter [Behandeln von Problemen mit Paketausführungstools](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 Sie können die Transformation konfigurieren, indem Sie entweder den [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder das Objektmodell verwenden. Details zum programmgesteuerten Konfigurieren dieser Transformation finden Sie im Entwicklerhandbuch.  
  
## <a name="configure-the-ole-db-command-transformation"></a>Konfigurieren der Transformation für OLE DB-Befehl
  Das Paket muss bereits mindestens einen Datenflusstask und eine Quelle, wie z. B. eine Flatfilequelle oder eine OLE DB-Quelle, einschließen, damit Sie eine Transformation für OLE DB-Befehl hinzufügen und konfigurieren können. Diese Transformation wird normalerweise zum Ausführen parametrisierter Abfragen verwendet.  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>So konfigurieren Sie die Transformation für OLE DB-Befehl  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Fenster **Toolbox**die Transformation für OLE DB-Befehl auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für OLE DB-Befehl mit dem Datenfluss, indem Sie einen Konnektor (der grüne oder rote Pfeil) von einer Datenquelle oder einer vorherigen Transformation mit der Maus auf die Transformation für OLE DB-Befehl ziehen.  
  
5.  Klicken Sie mit der rechten Maustaste auf die Komponente, und wählen Sie „Bearbeiten“ oder **Erweiterten Editor anzeigen**aus.  
  
6.  Wählen Sie auf der Registerkarte **Verbindungs-Manager** in der Liste **Verbindungs-Manager** einen OLE DB-Verbindungs-Manager aus. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Klicken Sie auf die Registerkarte **Komponenteneigenschaften** , und klicken Sie im Feld **SqlCommand** auf die Schaltfläche mit den drei Punkten ( **…** ).  
  
8.  Geben Sie in **Zeichenfolgenwert-Editor**die parametrisierte SQL-Anweisung mithilfe eines Fragezeichens (?) als Parametermarkierung für jeden Parameter ein.  
  
9. Klicken Sie auf **Aktualisieren**. Wenn Sie auf **Aktualisieren**klicken, erstellt die Transformation eine Spalte für jeden Parameter in der Sammlung externer Spalten und legt die DBParamInfoFlags-Eigenschaft fest.  
  
10. Klicken Sie auf die Registerkarte **Eingabe- und Ausgabeeigenschaften** .  
  
11. Erweitern Sie **Eingabe des OLE DB-Befehls**und anschließend **Externe Spalten**.  
  
12. Überprüfen Sie, ob **Externe Spalten** eine Spalte für jeden Parameter in der SQL-Anweisung auflistet. Die Spaltennamen lauten **Param_0**, **Param_1**usw.  
  
     Die Spaltennamen sollten nicht geändert werden. Wenn Sie die Spaltennamen ändern, generiert [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] einen Überprüfungsfehler für die Transformation für den OLE DB-Befehl.  
  
     Der Datentyp sollte auch nicht geändert werden. Die DataType-Eigenschaft der einzelnen Spalten wird auf den entsprechenden Datentyp festgelegt.  
  
13. Falls **Externe Spalten** keine Spalten auflistet, müssen sie manuell hinzugefügt werden.  
  
    -   Klicken Sie für jeden Parameter in der SQL-Anweisung einmal auf **Spalte hinzufügen** .  
  
    -   Aktualisieren Sie die Spaltennamen auf **Param_0**, **Param_1**usw.  
  
    -   Geben Sie einen Wert in der DBParamInfoFlags-Eigenschaft an. Der Wert muss mit einem Wert in der OLE DB-Enumeration DBPARAMFLAGSENUM übereinstimmen. Weitere Informationen finden Sie in der OLE DB-Referenzdokumentation.  
  
    -   Geben Sie den Datentyp der Spalte und, in Abhängigkeit vom Datentyp, die Codepage, die Länge, die Genauigkeit und die Dezimalstellen der Spalte an.  
  
    -   Wenn Sie einen nicht verwendeten Parameter löschen möchten, wählen Sie den Parameter in **Externe Spalten**aus, und klicken Sie auf **Spalte entfernen**.  
  
    -   Klicken Sie auf **Spaltenzuordnungen** , und ordnen Sie Spalten in der Liste **Verfügbare Eingabespalten** Parametern in der Liste **Verfügbare Zielspalten** zu.  
  
14. Klicken Sie auf **OK**.  
  
15. Klicken Sie im Menü **Datei** auf **Speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
