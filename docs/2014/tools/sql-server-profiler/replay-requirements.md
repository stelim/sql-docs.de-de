---
title: Anforderungen für die Wiedergabe | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], replaying traces
- traces [SQL Server], replaying
- replaying traces
- TSQL_Replay template [SQL Server]
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 447792a89be970078fdfca3f1e79eadbcc25bbfe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48173670"
---
# <a name="replay-requirements"></a>Replay Requirements
  Um Ablaufverfolgungsdaten mit [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] oder dem Distributed Replay Utility wiedergeben zu können, müssen in der Ablaufverfolgung bestimmte Ereignisklassen und Spalten aufgezeichnet werden. Diese Einstellungen sind standardmäßig aktiviert, wenn mit der **TSQL_Replay** -Ablaufverfolgungsvorlage eine Ablaufverfolgung konfiguriert wird, die später zur Wiedergabe verwendet wird. In diesem Thema sind diese Einstellungen und weiteren Wiedergabeanforderungen beschrieben.  
  
> [!NOTE]  
>  Es empfiehlt sich, zum Wiedergeben einer intensiven OLTP-Anwendung das Distributed Replay Utility (mit zahlreichen aktiven gleichzeitigen Verbindungen oder hohem Durchsatz) zu verwenden. Mit dem Distributed Replay Utility können Sie Ablaufverfolgungsdaten von mehreren Computern wiedergeben, um unternehmenswichtige Arbeitsauslastungen besser zu simulieren. Weitere Informationen finden Sie unter [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="event-classes-required-for-replay"></a>Für die Wiedergabe erforderliche Ereignisklassen  
 Für die Wiedergabe durch [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]müssen neben allen anderen zu überwachenden Ereignisklassen die folgenden Ereignisklassen in der Ablaufverfolgung aufgezeichnet werden:  
  
-   **CursorClose**(nur beim Wiedergeben serverseitiger Cursor)  
  
-   **CursorExecute** (nur beim Wiedergeben serverseitiger Cursor)  
  
-   **CursorOpen** (nur beim Wiedergeben serverseitiger Cursor)  
  
-   **CursorPrepare** (nur beim Wiedergeben serverseitiger Cursor)  
  
-   **CursorUnprepare** (nur beim Wiedergeben serverseitiger Cursor)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (nur beim Wiedergeben serverseitig vorbereiteter SQL-Anweisungen)  
  
-   **Prepare SQL** (nur beim Wiedergeben serverseitig vorbereiteter SQL-Anweisungen)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>Für die Wiedergabe erforderliche Datenspalten  
 Zusätzlich zu anderen Datenspalten, die Sie aufzeichnen möchten, müssen die folgenden Datenspalten in einer Ablaufverfolgung aufgezeichnet sein, damit die Ablaufverfolgung wiedergegeben werden kann:  
  
-   **Ereignisklasse**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **ApplicationName**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **Datenbank-ID**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **ServerName**  
  
-   **Binärdaten**  
  
-   **SPID**  
  
-   **Startzeit**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **Fehler**  
  
> [!NOTE]  
>  Mithilfe der Ablaufverfolgungsvorlage **TSQL_Replay** können Sie Ablaufverfolgungen erstellen, die Daten für die Wiedergabe aufzeichnen.  
  
## <a name="other-replay-requirements"></a>Weitere Anforderungen für die Wiedergabe  
 In Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]wird durch die Wiedergabe überprüft, ob die benötigten Ereignisse und Spalten vorhanden sind. Durch diese Änderung wird nicht nur die Genauigkeit der Wiedergabe erhöht, sondern auch die Suche bei der Problembehandlung vereinfacht, insbesondere wenn benötigte Daten fehlen. Die Wiedergabe gibt einen Fehler zurück und hält die Wiedergabe der aktuellen Datei an, wenn die von der Ablaufverfolgung benötigten Daten fehlen.  
  
 Wenn Sie eine Ablaufverfolgung für einen Server mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (das Ziel) wiedergeben möchten und dieser Server nicht mit dem Server übereinstimmt, für den die Ablaufverfolgung ursprünglich erstellt wurde, sollten folgende Schritte ausgeführt werden:  
  
-   Alle in der Ablaufverfolgung enthaltenen Benutzernamen und Benutzer müssen bereits auf dem Ziel und in derselben Datenbank wie auf der Quelle erstellt worden sein.  
  
-   Alle Benutzernamen und Benutzer auf dem Ziel müssen über dieselben Berechtigungen wie auf der Quelle verfügen.  
  
-   Alle Anmeldekennwörter müssen mit den Kennwörtern des Benutzers übereinstimmen, der die Wiedergabe ausführt.  
  
-   Die Datenbank-IDs auf dem Ziel sollten mit denen auf der Quelle übereinstimmen. Andernfalls können Sie basierend auf **DatabaseName** einen Abgleich ausführen, sofern dieser in der Ablaufverfolgung enthalten ist.  
  
-   Die Standarddatenbank für jeden in der Ablaufverfolgung enthaltenen Benutzernamen muss (auf dem Ziel) auf die entsprechende Zieldatenbank des Benutzernamens festgelegt werden. Beispielsweise enthält die wiederzugebende Ablaufverfolgung Aktivitäten für den Benutzernamen **Fred**in der **Fred_Db** -Datenbank der Quelle. Daher muss die Standarddatenbank auf dem Ziel für den Benutzernamen **Fred**auf die Datenbank festgelegt werden, die mit **Fred_Db** übereinstimmt (selbst wenn sich der Datenbankname unterscheidet). Legen Sie mithilfe der gespeicherten Systemprozedur **sp_defaultdb** die Standarddatenbank für den Benutzernamen fest.  
  
 Beim Wiedergeben von Ereignissen, die fehlende oder fehlerhafte Benutzernamen aufweisen, können Wiedergabefehler auftreten, die Wiedergabe wird jedoch fortgesetzt.  
  
 Informationen zu den Berechtigungen, die zum Wiedergeben einer Ablaufverfolgung erforderlich sind, finden Sie unter [Permissions Required to Run SQL Server Profiler](sql-server-profiler.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Wiedergeben einer Ablaufverfolgungstabelle &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)   
 [Wiedergeben einer Ablaufverfolgungsdatei &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)   
 [Ereignisklassen in SQL Server: Referenz](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-defaultdb-transact-sql)   
 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)  
  
  
