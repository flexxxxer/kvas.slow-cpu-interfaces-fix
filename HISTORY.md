## 1.1.4
- Доработана функция по добавлению/удалению гостевой/VPN сети - команда kvas vpn guest.
- Доработан функция при обновлении правил, после которой происходил разрыв соединения [тикет 48](https://github.com/qzeleza/kvas/issues/48).
- Доработана функция получения entware интерфейса по IP, из-за чего происходило неверное распознавание данных.

## 1.1.3
- Доработана функция получения локального entware интерфейса по ip. Спасибо за помощь [@Aleksandr Akimov](https://forum.keenetic.com/profile/13033-aleksandr-akimov/).
- Доработана функция импорта данных из файла. Теперь хосты со звездочкой впереди обрабатываются корректно. 
- Доработан механизм отображения списка в случае, если этот список пуст.


## 1.1.2
- Отключено принудительное переподключение основного соединения при обновлении данных через cron [[тикет от evgeny1503](https://forum.keenetic.com/topic/14415-пробуем-квас-shadowsocks-и-другие-vpn-клиенты/?do=findComment&comment=157181)]
- Снижен уровень логирования в журнал роутера, убраны излишние сообщения необходимые для отладки пакета.
- Косметическая доработка кода. Замена имен файлов их кодовым эквивалентом.


## 1.1.1
- Исправлена ошибка при добавлении и удалении диапазона IP-адресов из списка разблокировки ([тикет #32](https://github.com/qzeleza/kvas/issues/32))
- Реализована возможность добавления доменного имени с начальными 'http[s]://', которая порой требуется при добавлении домена из буфера обмена. При этом сам доменный суффикс 'http[s]://' подлежит отсечению. 
- Добавлены предупреждения, в случае запуска команд для работы с dnsmasq и dnscrypt-proxy с активированным AdGuardHome о том, что работает только один из вариантов, либо AdGuardHome, либо связка dnsmasq+dnscrypt-proxy 

## 1.1
- Косметические изменения в документации, теперь документацией по пакету можно ознакомиться по ссылке https://github.com/qzeleza/kvas/wiki
- Доработан механизм обновления ssr соединения при редактировании его данных посредством команд `kvas ssr *` 
- Доработан механизм составления отчета об ошибке при подаче его через GitHub.

## 1.0. beta 22
- Изменен механизм установки пакета - процесс настройки выделен в отдельную функцию. Добавлена новая команда `kvas setup` для первичной настройки пакета.
- Изменен механизм удаления пакета - процесс удаления выделен в отдельную функцию. Добавлена новая команда `kvas uninstall` для удаления пакета и его архивных данных. Команда `kvas uninstall full` удаляет пакет вместе со всеми, установленными пакетами.
- Изменен механизм установки пакета AdGuardHome. Теперь для установки пакета AdGuardHome, необходимо просто выполнить команду `kvas adguard on`. В случае отсутствия пакета - он будет установлен и обновлен до крайней версии автоматически. 
- Исправлена ошибка, которая приводила к тому, что при отсутствии архивной копии ssr настроек соединения не происходило запроса на новые настройки; 
- Осуществлен перенос нескольких глобальных переменных в общий файл конфигурации kvas.conf, с целью повысить стабильность работы пакета.
- Внесены исправления в процесс инициализации и проверки соединения. Сейчас в случае проблем с интернетом происходит переподключение основного подключения к провайдеру.


## 1.0. beta 21
- Доработаны правила срабатывания создания iptables правил в библиотеке ndm 
- Исправлена ошибка приводящая к обращению к службе dnsmasq при запущенном сервисе adguard (issues [#17](https://github.com/qzeleza/kvas/issues/17), [#15](https://github.com/qzeleza/kvas/issues/15))
- Откатились на паузу в 1 сек. (как было в 19 бете) при сканировании интерфейсов и отображении их списка с целью корректного отображения названий интерфейсов. 
- Исправлена ошибка [#22](https://github.com/qzeleza/kvas/issues/22), приводящая к отсутствию запроса на ввод данных при выборе Shadowsocks соединения. 
- Добавлена новая команда `kvas uninstall` для удаления пакета и его архивных данных. Команда `kvas uninstall full` удаляет пакет вместе со всеми, установленными пакетами.

## 1.0. beta 20
- При выполнении проверки **kvas test** теперь, в случае, если **IP** домен отсутствует в **ipset** таблице, осуществляется не просто ее перезаполнение, а выполняется полная переустановка правил заново функцией cmd_kvas_init, что повышает надежность восстановления списка и приведением его в норму.
- Добавлена новая команда **kvas adguard update**, которая позволяет в ручном режиме обновлять версию пакета AdGuardHome в зависимости от Вашей платформы. Выражаю благодарность @avn за идею и сам скрипт.
- В список разблокировки по умолчанию добавлено несколько популярных доменов.
- Добавлены новые команды **kvas adblock add <d>** и **kvas adblock del <d>**, которые оперируют со списком исключений и удаляют домены в этом списке из списка блокировки рекламы. 
- Добавлена команда для удаления обновления информации о доменных ip из cron: 'kvas period del|clear'
- Исправлена ошибка приводящая к неверной работе установки периода обновления данных.
- Переписан код скрипта ipset, добавлены сообщения в лог роутера и добавлен запуск скрипта в cron каждые 5 минут, для регулярного обновления IP адресов для доменных имен.
- Оптимизирована функция установки/удаления iptables правил для shadowsocks соединений.
- Исправлена ошибка возникающая при запуске обновления - переставал работать обход блокировок.
- Доработан механизм обновления версии пакета AdGuardHome по команде kvas adguard update.

## 1.0. beta 19
- Меняем в файле конфигурации AdGuard Home DNS его адрес, в случае если он равен 0.0.0.0. Это предотвращает зависание пакета при его установке (см. [issue#9](https://github.com/qzeleza/kvas/issues/9) ). '
- Логирование в механизме прерываний ndm теперь производится только в случае ошибок, а не свершения каких либо действий.
- Произведено обновление iptables правил для SHADOWSOCKS на более эффективные. 
- Создан новый файл /opt/apps/kvas/etc/config/excluded.net c именами локальных сетей, обращения к которым будет игнорироваться при запросах к SHADOSOCKS/VPN подключениям.
- Полностью переработан механизм очистки установки правил iptables (кроме VPN правил для случая, когда программное и аппаратное ускорение ОТКЛЮЧЕНО)  
- Изменен порядок добавления хостов в список разблокировки, в случае наличия домена в списке. Теперь происходит замена домена. Например, если в списке был домен test.com, а добавляем *test.com, то просто произойдет замена домена на *test.com.
- Добавлен домен *fburl.com в список разблокировки по умолчанию для работы сайта лицокнига. 
- Добавлена новая команда reset|init которая пересоздает все правила в случае сбоя или проблем с разблокировкой.
- Введено новое правило при добавлении домена без звездочки - проверка на доступность домена осуществляться будет, а при синтаксисе добавляемого домена *domain.dom, проверка на доступность осуществляться не будет.
- Добавлена возможность тестировать любой введенный домен при исполнении команды 'kvas dns test domain.com'. По умолчанию, тестируется домен facebook.com. 
- Дополнены файлы справки и документация по проекту. 
- Добавлены дополнительно к ключу 'help', ключи '-h' и '--h' для вызова справки.
- Теперь, при добавлении любого из доменов в список разблокировки, в случае подключенной опции блокирования рекламы, добавляемые доменные имена проходят проверку на наличие их в списке блокировки рекламы и в случае их наличия они удаляются от туда. Причем, если добавлен домен в виде *domain.com, то будут удалены все доменные имена с основанием domain.com, выше второго уровня, т.е. удалению подлежат, все имена от domain.com до dm5.dm4.dm3.domain.com и выше. Но удалению НЕ подлежат такие имена, которые не заканчиваются на domain.com, как например domain.com.ru.org.


## 1.0. beta 18
- Исправлена ошибка при установке пакета в режиме установки dnsmaqs, когда установка пакета завершалась с ошибкой
- Исправлена ошибка отсутствия вывода версии пакета kvas ver
- Исправлена ошибка работы при исполнении команды kvas ssr port, сейчас выводит все правильно - версию порта.
- Добавлена новая команда **vpn rescan/scan** принудительное сканирование интерфейсов роутера, в случае, появления нового подключения, например wireguard или openvpn.
- Исправлена ошибка повторного создания правил маршрутизации и маркировки трафика VPN подключений
- Изменен формат обработки журналирования в лог роутера при ошибках в процессе создания правил маркировки и маршрутизации 
- Добавлены тесты для функций создания правил маркировки и маршрутизации (файл ndm)
- Обновлен порядок запуска пакета и созданы правила для очистки всех правил и таблиц при запуске (как для adguard, так и для dnsmasq)
- Обновлены файлы справки по всем разделам
- Внесены новые правила для маркировки VPN подключений, которые являются более эффективными, относительно предыдущих (благодарность @avn).
- Ликвидирована проблема, приводившая к неверному определению подключения интерфейсов при их сканировании.
- Ликвидирована проблема, приводившая к зависанию процесса установки пакета на заключительной стадии проверки работы пакета.  
- Изменен порядок установки пакета, теперь в первую очередь происходит выбор VPN интерфейса и затем все остальные действия.
- Исправлена ошибка, которая приводила к обнулению списка блокировки рекламы при его сканировании (благодарю @Килелева Николая)

## 1.0. beta 17
- Удалены строки с комментариями и пустые строки при выводе отладочной и тестовой информации из файлов конфигурации.
- Исправленные ошибки при выборе shadowsocks подключения во время установки
- Изменилось поведение при исполнении команды kvas без аргументов - вместо вывода справки, сейчас выводит БС (исполняет свое предназначение)
- Внесены изменения в работу команды adguard off - сейчас Adguard отключается в принудительном порядке (ранее сначала проверялся по статусу)
- Добавлена дополнительная проверка на наличие /opt/etc/kvas.dnsmasq при проверке работы dnsmasq 
- Добавлена возможность архивировать и восстанавливать настройки для dnscrypt-proxy2
- Изменен принцип проверки работы службы AdGuardHome - ориентация на наличие запущенной службы и соответствующей записи в файле настроек Кваса

## 1.0 beta 16
- доработан скрипт маркировки VPN трафика [100-vpn-mark], теперь скрипт автоматически определяет как ему маркировать трафик (с включенным или отключенным ускорением)
- теперь команда kvas ssr port отображает текущий номер локального порта shadowsocks соединения
- исправлена ошибка при установке локального порта по команде kvas ssr port <port>
- при использовании adguard и выводе команды kvas debug, секция ipset теперь выводится полностью
- удален запрос на удаленную установку AdGuard Home для избежания последующих недоразумений.
- устранена ошибка при повторном удалении AdGuard Home: 'sed: /opt/etc/AdGuardHome/AdGuardHome.yaml: No such file or directory'
- изменена структура и наименования исполняемых файлов по функциональному признаку для удобочитаемости файлов проекта
- добавлена возможность подключать гостевую сеть к VPN подключению, отличное от shadowsocks. Команда kvas vpn guest ent_network 

## 1.0 beta 15

- покрытие тестами составляет 27% (33/121)
- доступна новая команда bridge выводит список доступных гостевых интерфейсов
- исправлена ошибка, возникавшая при чтении данных из архива shadowsocks соединения
- в скрипте kvas_ipset адрес 0.0.0.0 убран из добавления в таблицу ipset
- доработан механизм установки AdGuard Home на локальное устройство
- при запуске команды kvas dns, теперь выводится сервис-владелец DNS: dnsmasq, dnscrypt_proxy2, AdGuard Home
- доработан скрипт kvas_adblock по обновлению списков рекламы в разрезе отработки различных ошибок.

## 1.0 beta 14

- исправлена ошибка, которая приводила к невозможности запустить adguard после перезагрузки роутера.
- исправлена ошибка восстановления из архивной копии shadowsocks, которая приводила к невозможности ввода новых данных
- переписан код определения состояния AdGuard Home и код по его установке

## 1.0 beta 13

- исправлена ошибка зависания при удалении пакета на стадии очистки правил iptables.
- исправлена ошибка при зависании при установке пакета на стадии тестирования соединения.
- переписан скрипт формирования списка ipset для AdGuard Home

## 1.0 beta 12

- реализованы новые команды
     - 'bridge add all' - разрешаем доступ к VPN всем существующим гостевым сетям
     - 'bridge del all' - запрещаем доступ к VPN для всех гостевых сетей.
     - 'ssr new' - меняет настройки учетной записи shadowsocks сервера
        на другие настройки, в случае смены сервера или иных данных учетной записи
     - 'adguard on' - подключает использование AdGuard Home к КВАСу
     - 'adguard off' - отключает использование AdGuard Home в КВАСе
     - 'adguard test' - тестирует правила создания ipset для AdGuard Home

- упразднены следующие команды
        - 'ssr set', вместо нее используйте 'vpn set'
        - 'dns adguard', вместо нее используйте 'adguard on'
        - 'ssr flush' за ненадобностью, вместо нее используйте 'ssr reset'
        - 'vpn flush' за ненадобностью, вместо нее используйте 'vpn reset'

- обновлена справка по новым командам
- возможность сохранения списка разблокировки при обновлении/переустановке пакета
- команда смены DNS сервера на AdGuard Home теперь работает как положено.
  AdGuard Home слушает 53 порт, а записи ipset формируются для него скриптом.
  При этом отключаются службы dnsmasq и dnscrypt_proxy2, так как AdGuard Home имеет
  полную замену всему их функционалу + WUI интерфейс.
- в случае отсутствия AdGuard Home на роутере, теперь скрипт может его автоматически скачать.
- полностью переписан скрипт сборки проекта с учетом нововведений выше.
- добавлена проверка, при установке пакета, на включение IPv6 на интерфейсе для интернета
  В случае ее наличии - отключает.
- оптимизирован код отвечающий за тесты и отладку пакета
- в целях отладки ведется сбор данных при установке пакета в файл /opt/tmp/kvas.install.log
- при удалении пакета, теперь очищаются все правила и таблицы, которые были созданы пакетом для своей работы
- упразднено большинство вопросов при установке, все делается по умолчанию
  и в случае необходимости может быть отключено вручную соответствующими командами
- внесены правки в код для проверки работоспособности пакета AdGuard Home в связке с КВАСом.
- исправлены синтаксические ошибки.
- теперь, исходный код пакета Вы сможете посмотреть по этой ссылке https://github.com/qzeleza/kvas.git