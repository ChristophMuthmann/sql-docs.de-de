---
title: Implementieren einer Suche ohne Cache oder partiellem Cache-Modus | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb81f969cc30366489df367016c8096ea2ac1168
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>Implementieren einer Suche im Modus "Kein Cache" oder "Teilcache"
  Sie können die Transformation für die Suche so konfigurieren, dass der Modus "Teilcache" oder "Kein Cache" verwendet wird:  
  
-   Teilcache  
  
     Die Zeilen mit übereinstimmenden Einträgen im Verweisdataset und optional die Zeilen ohne übereinstimmende Einträge im Dataset werden im Zwischenspeicher abgelegt. Wenn die Speichergröße des Caches überschritten wird, entfernt die Transformation zum Suchen automatisch die am seltensten verwendeten Zeilen aus dem Cache.  
  
-   Kein Cache  
  
     Es werden keine Daten in den Zwischenspeicher geladen.  
  
 Unabhängig davon, ob Sie Teilcache oder Kein Cache auswählen, verwenden Sie einen OLE DB-Verbindungsmanager, um die Verbindung zum Verweisdataset herzustellen. Das Verweisdataset wird durch die Verwendung einer Tabelle, Sicht oder SQL-Abfrage während der Ausführung der Transformation für Suche generiert.  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>So implementieren Sie eine Transformation für Suche im Modus für "Kein Cache" oder "Teilcache"  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket, und öffnen Sie dann das Paket.  
  
2.  Fügen Sie auf der Registerkarte **Datenfluss** eine Transformation für Suche hinzu.  
  
3.  Verbinden Sie die Suchtransformation mit dem Datenfluss, indem Sie einen Konnektor von einer Quelle oder einer vorherigen Transformation auf die Suchtransformation ziehen.  
  
    > [!NOTE]  
    >  Eine Suchtransformation, die für die Verwendung des Modus „Kein Cache“ konfiguriert ist, erzeugt möglicherweise einen Fehler, wenn die Transformation sich mit einem Flatfile verbindet, das ein leeres Datenfeld enthält. Die Gültigkeit der Transformation hängt davon ab, ob der Verbindungs-Manager für das Flatfile so konfiguriert wurde, dass NULL-Werte beibehalten werden. Um sicherzustellen, dass die Suchtransformation gültig ist, wählen Sie im **Quelleneditor für Flatfiles**auf der **Seite Verbindungs-Manager**die Option **NULL-Werte aus der Quelle als NULL-Werte im Datenfluss beibehalten** .  
  
4.  Doppelklicken Sie auf die Quelle oder die vorherige Transformation, um die Komponente zu konfigurieren.  
  
5.  Doppelklicken Sie auf die Transformation für Suche, und wählen Sie anschließend im **Transformations-Editor für Suche**auf der Seite **Allgemein** die Option **Teilcache** oder die Option **Kein Cache**aus.  
  
6.  Wählen Sie für die Liste **Angeben, wie Zeilen ohne übereinstimmende Einträge behandelt werden sollen** eine Fehlerbehandlungsoption aus der Liste aus.  
  
7.  Wählen Sie auf der Seite **Verbindung** einen Verbindungs-Manager aus der Liste **OLE DB-Verbindungs-Manager** aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen. Weitere Informationen finden Sie unter [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
8.  Führen Sie einen der folgenden Schritte aus:  
  
    -   Klicken Sie auf **Tabelle oder Sicht verwenden**, und wählen Sie dann eine Tabelle oder eine Sicht aus, oder klicken Sie auf **Neu** , um eine Tabelle oder Sicht zu erstellen.  
  
    -   Klicken Sie auf **Ergebnisse einer SQL-Abfrage verwenden**, und erstellen Sie dann eine Abfrage im Fenster **SQL-Befehl** .  
  
         – oder –  
  
         Klicken Sie auf **Abfrage erstellen** , um mit den vom **Abfrage-Generator** bereitgestellten grafischen Tools eine Abfrage zu erstellen.  
  
         – oder –  
  
         Klicken Sie auf **Durchsuchen** , um eine SQL-Anweisung aus einer Datei zu importieren.  
  
     Um die SQL-Abfrage zu überprüfen, klicken Sie auf **Abfrage analysieren**.  
  
     Um ein Beispiel der Daten anzuzeigen, klicken Sie auf **Vorschau**.  
  
9. Klicken Sie auf die Seite **Spalten** , und ziehen Sie mindestens eine Spalte aus der Liste **Verfügbare Eingabespalten** in eine Spalte in der Liste **Verfügbare Suchspalten** .  
  
    > [!NOTE]  
    >  Die Transformation für Suche ordnet automatisch Spalten mit dem gleichen Namen und dem gleichen Datentyp zu.  
  
    > [!NOTE]  
    >  Die Spalten müssen übereinstimmende Datentypen aufweisen, damit sie zugeordnet werden. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Schließen Sie Suchspalten in die Ausgabe ein, indem Sie die folgenden Schritte ausführen:  
  
    1.  Wählen Sie Spalten aus der Liste **Verfügbare Suchspalten** aus.  
  
    2.  Geben Sie in der Liste **Suchvorgang** an, ob die Werte aus den Suchspalten Werte in der Eingabespalte ersetzen oder ob sie in eine neue Spalte geschrieben werden.  
  
11. Wenn Sie in Schritt 5 **Teilcache** auf der Seite **Erweitert** ausgewählt haben, legen Sie die folgenden Cacheoptionen fest:  
  
    -   Wählen Sie aus der Liste **Cachegröße (32-Bit)** die Cachegröße für 32-Bit-Umgebungen aus.  
  
    -   Wählen Sie aus der Liste **Cachegröße (64-Bit)** die Cachegröße für 64-Bit-Umgebungen aus.  
  
    -   Um die Zeilen ohne übereinstimmende Einträge in der Referenz im Zwischenspeicher abzulegen, aktivieren Sie die Option **Cache für Zeilen ohne übereinstimmende Einträge aktivieren**.  
  
    -   Wählen Sie aus der Liste **Zuordnung von Cache** den Prozentsatz des Zwischenspeichers aus, der zum Speichern der Zeilen ohne übereinstimmende Einträge verwendet werden soll.  
  
12. Um die SQL-Anweisung zu ändern, die das Verweisdataset generiert, wählen Sie **SQL-Anweisung ändern**aus, und ändern Sie die im Textfeld angezeigte SQL-Anweisung.  
  
     Falls die Anweisung Parameter enthält, klicken Sie auf **Parameter** , um den Eingabespalten die Parameter zuzuordnen.  
  
    > [!NOTE]  
    >  Durch die auf dieser Seite angegebene optionale SQL-Anweisung wird der auf der Seite **Verbindung** im Transformations-Editor für Suche ****angegebene Tabellenname überschrieben und ersetzt.  
  
13. Um die Fehlerausgabe zu konfigurieren, klicken Sie auf die Seite **Fehlerausgabe** , und legen Sie die Fehlerbehandlungsoptionen fest. Weitere Informationen finden Sie unter [Transformations-Editor für Suche &#40;Seite Fehlerausgabe&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
14. Klicken Sie auf **OK** , um die Änderungen an der Suchtransformation zu speichern, und führen Sie dann das Paket aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  

