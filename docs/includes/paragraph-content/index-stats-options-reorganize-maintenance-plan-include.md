

### <a name="index-stats-options"></a>Indexstatistik – Optionen

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


In früheren Microsoft SQL Server-Versionen konnte die Reorganisation oder Neuerstellung großer Indizes das System verlangsamen. In SQL Server 2015 wurden umfassende Leistungsverbesserungen für solche Indexvorgänge implementiert.

In früheren Versionen konnten diese Vorgänge auch noch nicht sehr genau gesteuert werden. Dies führte dazu, dass das System auch Indizes reorganisierte oder neu erstellte, die nicht sehr fragmentiert waren, was eine unnötige Systembelastung bedeutete. Mit neueren Steuerelementen auf der Benutzeroberfläche des Wartungsplans können Sie Indizes ausschließen, die gemäß Indexstatistikkriterien nicht aktualisiert werden müssen. Hierfür werden intern die folgenden dynamischen Verwaltungssichten von Transact-SQL verwendet:


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **Scantyp**  
 Das System verbraucht Ressourcen, um Indexstatistiken zu erfassen. Je nachdem, wie viel Genauigkeit Ihrer Meinung nach für Indexstatistiken erforderlich ist, können Sie auswählen, ob verhältnismäßig wenig oder eher mehr Ressourcen genutzt werden sollen. Die Benutzeroberfläche bietet folgende Genauigkeitslevel, aus denen Sie eins auswählen müssen:


- Schnell
- Stichproben
- Detailliert


 **Index nur optimieren, wenn:**  
 Die Benutzeroberfläche bietet folgende anpassbare Filter, mit denen Sie verhindern können, dass Indizes aktualisiert werden, für die eine Aktualisierung nicht unbedingt notwendig ist:


- Fragmentierung &gt; *(%)*
- Seitenanzahl &gt;
- Verwendet in den letzten *(Tagen)*

