---

copyright:
  years: 2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sicherungen
{: #backups}

Sie können Sicherungen erstellen und über die Seite *Verwalten* Ihres Service-Dashboards herunterladen. Es sind sowohl geplante als auch manuelle Sicherungen verfügbar.

## Vorhandene Sicherungen anzeigen

Tägliche Sicherungen Ihrer Datenbank werden automatisch geplant. Navigieren Sie zum Anzeigen Ihrer vorhandenen Sicherungen zu der Seite *Verwalten* Ihres Service-Dashboards. 

![Sicherungen](./images/redis-backups-show.png "Liste der Sicherungen im Service-Dashboard")

Klicken Sie in eine Zeile, um die Optionen für die entsprechende verfügbare Sicherung zu erweitern.

![Sicherungsoptionen](./images/redis-backups-options.png "Optionen für eine Sicherung.") 

## Sicherung bedarfsgerecht erstellen

Neben geplanten Sicherungen können Sie manuelle Sicherungen erstellen. Navigieren Sie zum Erstellen einer manuellen Sicherung zu der Seite *Verwalten* Ihres Service-Dashboards und klicken Sie auf *Jetzt sichern*.

## Sicherung herunterladen

Navigieren Sie zum Herunterladen einer Sicherung zu der Seite *Verwalten* Ihres Service-Dashboards und klicken Sie in der entsprechenden Zeile mit der Sicherung, die Sie herunterladen wollen, auf *Herunterladen*.

## Inhalt von Sicherungen

Redis speichert standardmäßig einen binären Snapshot Ihrer Daten. Die Datei 'dump.rdb' kann dann als Sicherung für die punktuelle Wiederherstellung verwendet werden. Für den Snapshot wird Redis aufgespalten, sodass die gesamte Arbeit für den Snapshot von einem untergeordneten Prozess ausgeführt wird, während der übergeordnete Prozess mit der normalen Verarbeitung Ihrer Daten fortfährt. Der Sicherungsprozess hat keine Auswirkungen auf Ihre Anwendung oder Datenbank. Sie können sowohl eine Kopie Ihrer Sicherungen herunterladen als auch sie direkt in einen neue Bereitstellung wiederherstellen.

## Sicherung mit lokaler Datenbank verwenden

Sie können mit Ihrer {{site.data.keyword.composeForRedis}}-Sicherung eine lokale Kopie Ihrer Datenbank ausführen.

1. Verschieben Sie die Datei 'dump.rdb' in ein eigenes Verzeichnis z. B. 'db'.
2. Da Sie eine Redis-Konfigurationsdatei zum Starten der Redis-Instanz benötigen, empfiehlt es sich, eine Datei 'redis.conf' aus Ihrem Verzeichnis 'install' in Ihr Verzeichnis 'db' mit der Datei 'dump.rdb' zu kopieren. Wenn Sie Redis beispielsweise unter OSX mit homebrew installiert haben, befindet sich die Datei 'redis.conf' im Pfad `/usr/local/etc`. Führen Sie daher im Verzeichnis 'db' die Datei `cp /usr/local/etc/redis.conf` aus.
3. Bearbeiten Sie die Konfigurationsdatei so, dass sie beim Start auf Ihr aktuelles Verzeichnis verweist. Öffnen Sie 'redis.conf' mit einem Texteditor und ändern Sie die Zeile `dir /usr/local/var/db/redis/` in `dir`. Speichern Sie die Datei und beenden Sie den Vorgang.
4. Starten Sie den Redis-Server im Verzeichnis 'db', indem Sie die Konfigurationsdatei `redis-server redis.conf` bereitstellen.

## Sicherung wiederherstellen

Führen Sie zum Wiederherstellen einer Sicherung in eine neue Serviceinstanz die Schritte zum Anzeigen der vorhandenen Sicherungen aus. Klicken Sie dann in die entsprechende Zeile, um die Optionen für die Sicherung zu erweitern, die Sie herunterladen wollen. Klicken Sie auf die Schaltfläche **Wiederherstellen**. Es wird eine Nachricht darüber angezeigt, dass eine Wiederherstellung eingeleitet wurde. Die neue Serviceinstanz erhält automatisch den Namen "redis-restore-[timestamp]" und wird beim Start der Bereitstellung in Ihrem Dashboard angezeigt.
