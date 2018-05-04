---
title: Überwachen von Analysis Services mit SQLServer erweiterte Ereignisse | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef749103d80d7a1f2528f71955229598c7da9575
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  Die erweiterten Ereignisse (*xEvents*) sind ein kompaktes Ablaufverfolgungs- und Leistungsüberwachungssystem, das sehr wenige Ressourcen verwendet. Dadurch stellen sie ein ideales Tool zum Diagnostizieren von Problemen sowohl auf Produktions- als auch auf Testservern dar. Sie sind zudem hoch skalierbar, konfigurierbar und durch den neuen integrierten Toolsupport in SQL Server 2016 einfacher zu verwenden. In SQL Server Management Studio können Sie bei Verbindungen mit Analysis Services-Instanzen eine Live-Ablaufverfolgung konfigurieren, ausführen und überwachen, ähnlich der Verwendung von SQL Server Profiler. Das Hinzufügen besserer Tools sollte xEvents zu einem sinnvolleren Ersatz für SQL Server Profiler machen und für mehr Symmetrie bei der Diagnostizierung von Problemen in Ihrem Datenbankmodul und Analysis Services-Workloads sorgen.  
  
 Neben [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]können Sie  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Sitzungen für erweiterte Ereignisse auch über die bisherige Methode (Erstellen von XMLA-Skripts) konfigurieren, die in vorherigen Releases unterstützt wurde.  
  
 Alle Analysis Services-Ereignisse können aufgezeichnet und auf bestimmte Consumer ausgerichtet werden, wie in [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)definiert.  
  
> [!NOTE]  
>  Sehen Sie sich dieses [kurze Einführungsvideo](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) an, oder lesen Sie den [unterstützenden Blogbeitrag](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) , um mehr über xEvents für Analysis Services in SQL Server 2016 zu erfahren.  
  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> Verwenden von Management Studio zum Konfigurieren von Analysis Services  
 Management Studio stellt sowohl für tabellarische als auch für mehrdimensionale Instanzen einen neuen Ordner namens „Verwaltung“ bereit, der vom Benutzer initiierte xEvent-Sitzungen enthält. Sie können mehrere Sitzungen gleichzeitig ausführen. In der aktuellen Implementierung unterstützt die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Benutzeroberfläche der erweiterten Ereignisse jedoch nicht das Aktualisieren oder Wiedergeben einer vorhandenen Sitzung.  
  
 ![Ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "Ssas_extended_events_ssms_start")  
  
 **Auswählen von Ereignissen**  
  
 Wenn Sie bereits wissen, welche Ereignisse Sie erfassen möchten, stellt das Suchen nach diesen Ereignissen die einfachste Methode dar, diese zur Ablaufverfolgung hinzuzufügen. Andernfalls können Sie die folgenden Ereignisse nutzen, die häufig zum Überwachen von Vorgängen verwendet werden:  
  
-   **CommandBegin** und **CommandEnd**.  
  
-   **QueryBegin**, **QueryEnd**und **QuerySubcubeVerbose** (zeigt die gesamte an den Server gesendete MDX- oder DAX-Abfrage) sowie **ResourceUsage** für Statistiken über von der Abfrage belegte Ressourcen und darüber, wie viele Zeilen zurückgegeben werden.  
  
-   **ProgressReportBegin** und **ProgressReportEnd** (für Verarbeitungsvorgänge).  
  
-   **AuditLogin** und **AuditLogout** (erfasst die Benutzeridentität, unter der eine Clientanwendung eine Verbindung mit Analysis Services herstellt).  
  
 **Wählen des Datenspeichers**  
  
 Eine Sitzung kann live an ein Fenster in Management Studio gestreamt werden oder mithilfe von Power Query oder Excel dauerhaft in einer Datei für nachfolgende Analysen gespeichert werden.  
  
-   **event_file** speichert Sitzungsdaten in einer XEL-Datei.  
  
-   **event_stream** aktiviert die Option **Livedaten ansehen** in Management Studio.  
  
-   **ring_buffer** speichert Sitzungsdaten solange im Arbeitsspeicher, wie der Server ausgeführt wird. Bei einem Neustart des Servers werden die Sitzungsdaten verworfen.  
  
 **Hinzufügen von Ereignisfeldern**  
  
 Achten Sie darauf, die Sitzung so zu konfigurieren, dass Ereignisfelder enthalten sind, damit Sie einfach die für Sie interessanten Informationen einsehen können.  
  
 **Konfigurieren** ist eine Option am äußersten Ende des Dialogfelds.  
  
 ![Konfigurieren von SSAS-Xevents](../../analysis-services/instances/media/ssas-xevents-configure.PNG "Konfigurieren von Ssas-Xevents")  
  
 Wählen Sie bei der Konfiguration auf der Registerkarte „Ereignisfelder“ **TextData** aus, damit dieses Feld neben dem Ereignis auftaucht und dabei Rückgabewerte anzeigt, einschließlich auf dem Server ausgeführter Abfragen.  
  
 Nachdem Sie eine Sitzung für die gewünschten Ereignisse und Datenspeicher konfiguriert haben, können Sie auf die Schaltfläche „Skript“ klicken, um Ihre Konfiguration an eines der unterstützten Ziele zu senden, einschließlich einer Datei, einer neuen Abfrage in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]und der Zwischenablage.  
  
 **Aktualisieren von Sitzungen**  
  
 Nachdem Sie die Sitzung erstellt haben, sollten Sie den Ordner „Sitzungen“ in Management Studio aktualisieren, um die gerade erstellte Sitzung anzuzeigen. Wenn Sie einen event_stream konfiguriert haben, können Sie mit der rechten Maustaste auf den Namen der Sitzung klicken und **Livedaten ansehen** auswählen, um die Serveraktivität in Echtzeit zu überwachen.  
  
##  <a name="bkmk_script_start"></a> XMLA-Skript zum Starten der erweiterten Ereignisse in Analysis Services  
 Die Erweiterte Ereignis-Ablaufverfolgung wird mit einem ähnlichen XMLA-Skriptbefehl zum Erstellen eines Objekts wie unten dargestellt aktiviert:  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Dabei sind die folgenden Elemente abhängig von den Ablaufverfolgungsanforderungen vom Benutzer zu definieren:  
  
 *trace_id*  
 Definiert den eindeutigen Bezeichner für diese Ablaufverfolgung.  
  
 *trace_name*  
 Der Name dieser Ablaufverfolgung, normalerweise eine lesbare Beschreibung der Ablaufverfolgung. Üblicherweise wird der *trace_id* -Wert als Name verwendet.  
  
 *AS_event*  
 Das Analysis Services-Ereignis, das verfügbar gemacht werden soll. Die Namen der Ereignisse finden Sie unter [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md) .  
  
 *data_filename*  
 Der Name der Datei, die die Ereignisdaten enthält. Für diesen Namen wird ein Zeitstempel als Suffix verwendet, um das Überschreiben von Daten zu vermeiden, wenn die Ablaufverfolgung fortlaufend gesendet wird.  
  
 *metadata_filename*  
 Der Name der Datei, die die Ereignismetadaten enthält. Für diesen Namen wird ein Zeitstempel als Suffix verwendet, um das Überschreiben von Daten zu vermeiden, wenn die Ablaufverfolgung fortlaufend gesendet wird.  
  
  
##  <a name="bkmk_script_stop"></a> XMLA-Skript zum Beenden der erweiterten Ereignisse in Analysis Services  
 Um das Erweiterte Ereignisse-Ablaufverfolgungsobjekt zu beenden, müssen Sie dieses Objekt mit einem ähnlichen XMLA-Skriptbefehl zum Löschen eines Objekts wie unten dargestellt löschen:  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Dabei sind die folgenden Elemente abhängig von den Ablaufverfolgungsanforderungen vom Benutzer zu definieren:  
  
 *trace_id*  
 Definiert den eindeutigen Bezeichner für die zu löschende Ablaufverfolgung.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  
