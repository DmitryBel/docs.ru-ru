# [Примеры Windows Communication Foundation](index.md)
## [Инструкции по настройке](set-up-instructions.md)
### [Процедура однократной настройки образцов Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md)
#### [Инструкции по настройке брандмауэра](firewall-instructions.md)
#### [Инструкции по размещению в службах IIS](internet-information-service-hosting-instructions.md)
#### [Инструкции по установке сертификата сервера в службах IIS](iis-server-certificate-installation-instructions.md)
#### [Инструкции по настройке виртуальных каталогов](virtual-directory-setup-instructions.md)
#### [Установка системы очередей сообщений (MSMQ)](installing-message-queuing-msmq.md)
### [Построение примеров Windows Communication Foundation](building-the-samples.md)
### [Выполнение примеров Windows Communication Foundation](running-the-samples.md)
## [Основы](basic.md)
### [Начало работы](getting-started-sample.md)
### [AJAX](ajax.md)
#### [JSONP](jsonp.md)
#### [Сериализация JSON](json-serialization.md)
#### [Базовая служба AJAX](basic-ajax-service.md)
#### [Служба AJAX с использованием HTTP POST](ajax-service-using-http-post.md)
#### [Служба AJAX без конфигурации](ajax-service-without-configuration.md)
#### [Служба AJAX, использующая сложные типы](ajax-service-using-complex-types-sample.md)
#### [Служба AJAX с JSON и XML](ajax-service-with-json-and-xml-sample.md)
### [Привязка](binding.md)
#### [Кодировщик ByteStream](bytestream-encoder.md)
#### [Простая привязка](basic-binding.md)
##### [Пример безопасности сообщений](message-security-sample.md)
##### [BasicBinding с обеспечением безопасности транспорта](basicbinding-with-transport-security.md)
##### [BasicBinding](basicbinding.md)
#### [Пользовательская привязка](custom-binding.md)
##### [Императивные пользовательские привязки](custom-binding-imperative.md)
##### [Транспорт и кодировка пользовательской привязки](custom-binding-transport-and-encoding.md)
##### [Надежный сеанс с использованием пользовательской привязки](custom-binding-reliable-session.md)
##### [Надежный сеанс по протоколу HTTPS с использованием пользовательской привязки](custom-binding-reliable-session-over-https.md)
##### [Безопасность пользовательской привязки](custom-binding-security.md)
#### [Привязка на платформе .NET](net-binding.md)
##### [Привязка MSMQ на платформе .NET](net-msmq-binding.md)
###### [Привязка MSMQ с поддержкой транзакций](transacted-msmq-binding.md)
###### [Неустойчивое взаимодействие с использованием очереди](volatile-queued-communication.md)
###### [Очереди недоставленных сообщений](dead-letter-queues.md)
###### [Обработка подозрительных сообщений в MSMQ 4.0](poison-message-handling-in-msmq-4-0.md)
###### [Сеансы и очереди](sessions-and-queues.md)
###### [Двусторонний обмен данными](two-way-communication.md)
###### [Пакетирование с поддержкой транзакций](transacted-batching.md)
###### [SRMP](srmp.md)
###### [Безопасность сообщений при использовании очереди сообщений](message-security-over-message-queuing.md)
###### [Генератор продуктов ReceiveContext](receivecontext-enabled-wcf-channels.md)
##### [Интеграция очередей сообщений](message-queueing-integration.md)
###### [Передача сообщений из приложения MSMQ в приложение Windows Communication Foundation](message-queuing-to-wcf.md)
###### [Пользовательское демультиплексирование](custom-demux.md)
###### [Отправка сообщений из приложения Windows Communication Foundation в приложение MSMQ](wcf-to-message-queuing.md)
###### [Корреляция сообщений](message-correlation.md)
##### [NetTCPBinding](nettcpbinding.md)
###### [Привязка NetTcpBinding по умолчанию](default-nettcpbinding.md)
###### [Пример совместного использования портов Net.TCP](net-tcp-port-sharing-sample.md)
##### [NetNamedPipeBinding](netnamedpipebinding.md)
#### [Привязка WS](ws-binding.md)
##### [Привязка HTTP для федерации WS 2007](ws-2007-federation-http-binding.md)
##### [WS Dual Http](ws-dual-http.md)
##### [Кодирование MTOM](mtom-encoding.md)
##### [WSHttpBinding](wshttpbinding.md)
##### [Надежный сеанс WS](ws-reliable-session.md)
##### [Безопасность транспорта WS](ws-transport-security.md)
##### [Привязка безопасности сообщений](message-security-binding.md)
###### [Безопасность сообщений с возможностью анонимного доступа](message-security-anonymous.md)
###### [Сертификат безопасности сообщений](message-security-certificate.md)
###### [Безопасность сообщений с использованием имени пользователя](message-security-user-name.md)
###### [Безопасность сообщений с использованием механизмов Windows](message-security-windows.md)
##### [Транспорт WS с учетными данными сообщения](ws-transport-with-message-credential.md)
##### [Поток транзакций WS](ws-transaction-flow.md)
### [Клиент](client.md)
#### [Взаимодействие с клиентами](client-interoperability.md)
##### [Взаимодействие с веб-службами ASMX](interoperating-with-asmx-web-services.md)
##### [Пример XMLSerializer](xmlserializer-sample.md)
#### [Заголовки адресов](address-headers.md)
#### [Фабрика каналов](channel-factory.md)
#### [Ожидаемые исключения](expected-exceptions.md)
#### [Извлечение метаданных](retrieve-metadata.md)
#### [Предотвращение проблем при использовании операторов](avoiding-problems-with-the-using-statement.md)
#### [Типизированный клиент](typed-client.md)
### [Контракт](contract.md)
#### [Контракты данных](data-contracts.md)
##### [Базовый контракт данных](basic-data-contract.md)
##### [Пример DataContractSerializer](datacontractserializer-sample.md)
##### [Известные типы](known-types.md)
##### [Ссылки на объекты](object-references.md)
##### [Поддержка POCO](poco-support.md)
##### [Использование средства привязки сериализации](usage-of-serialization-binder.md)
#### [Контракты сообщений](message-contracts.md)
##### [Контракт сообщения по умолчанию](default-message-contract.md)
##### [Нетипизированный запрос/ответ](untyped-request-reply.md)
##### [Сообщения без оболочки](unwrapped-messages.md)
##### [Установка свойств Use и Style](setting-the-use-and-style-properties.md)
##### [Пример XmlReader](xmlreader-sample.md)
#### [Контракты служб](service-contracts.md)
##### [Дуплекс](duplex.md)
##### [Контракт ошибок](fault-contract.md)
##### [Одностороннее взаимодействие](one-way.md)
##### [Сеанс](session.md)
##### [Поток](stream.md)
##### [Ошибки XmlSerializer](xmlserializer-faults.md)
#### [DataContractResolver](datacontractresolver.md)
#### [Атрибут KnownAssemblyAttribute](knownassemblyattribute.md)
#### [Использование DataContractSerializer и DataContractResolver для обеспечения функциональности NetDataContractSerializer](datacontractserializer-datacontractresolver-netdatacontractserializer.md)
### [Обнаружение](discovery-samples.md)
#### [Замечания](announcements-sample.md)
#### [Асинхронная операция Find](asynchronous-find-sample.md)
#### [Основы](basic-sample.md)
#### [Конфигурация](configuration-sample.md)
#### [Образец элемента привязки для обнаружения](discovery-binding-element-sample.md)
#### [Образец прокси-сервера обнаружения](discovery-proxy-sample.md)
#### [Образец обнаружения службы с уникальным URI прослушивания](discover-a-service-with-unique-listen-uri-mode-sample.md)
#### [Обнаружение с помощью областей](discovery-with-scopes-sample.md)
#### [Пользовательские критерии поиска](custom-find-criteria.md)
#### [Образец обнаружения рабочего процесса](workflow-discovery-sample.md)
#### [Служба обнаружения маршрутизатора](discovery-router-service.md)
### [Управление](management.md)
#### [Службы WCF и трассировка событий для Windows](wcf-services-and-event-tracing-for-windows.md)
#### [Аналитическая трассировка WCF](wcf-analytic-tracing.md)
#### [Циклическая трассировка](circular-tracing.md)
#### [Трассировка ETW](etw-tracing.md)
#### [Расширение трассировки](extending-tracing.md)
#### [Блокировка безопасности PII](pii-security-lockdown.md)
#### [Использование счетчиков производительности](using-performance-counters.md)
#### [Трассировка и ведение журнала сообщений](tracing-and-message-logging.md)
#### [Проверка безопасности](security-validation.md)
#### [Поставщик WMI](wmi-provider.md)
### [Службы маршрутизации](routing-services.md)
#### [Приветствие средствами служб маршрутизации](hello-world-with-the-routing-service.md)
#### [Использование моста и обработка ошибок](bridging-and-error-handling.md)
#### [Дополнительные фильтры](advanced-filters.md)
#### [Динамическая реконфигурация](dynamic-reconfiguration.md)
#### [Расширенная обработка ошибок](advanced-error-handling.md)
### [Безопасность](security-in-wcf.md)
#### [Криптографическая гибкость в системе безопасности WCF](cryptographic-agility-in-wcf-security.md)
### [Службы](services.md)
#### [Размещение](hosting.md)
##### [Активация процессов Windows](windows-process-activation.md)
###### [Активация NamedPipe](namedpipe-activation.md)
###### [Активация TCP](tcp-activation.md)
###### [Активация MSMQ](msmq-activation.md)
##### [Активация на основе конфигурации](configuration-based-activation.md)
##### [Образец интеграции с SystemWebRouting](systemwebrouting-integration-sample.md)
##### [Совместимость с ASP.NET](aspnet-compatibility.md)
##### [Размещение в службах IIS с использованием встроенного кода](iis-hosting-using-inline-code.md)
##### [Узел службы Windows](windows-service-host.md)
##### [Резидентное размещение](self-host.md)
#### [Взаимодействие служб](service-interoperability.md)
##### [Использование моникера WCF с клиентами COM](using-the-wcf-moniker-with-com-clients.md)
##### [Клиент ASMX со службой WCF](asmx-client-with-a-wcf-service.md)
#### [Поведения](behaviors.md)
##### [Параллелизм](concurrency.md)
##### [Поведение служб по умолчанию](default-service-behavior.md)
##### [Создание экземпляров](instancing.md)
##### [Поведение публикации метаданных](metadata-publishing-behavior.md)
##### [Транзакционное поведение службы](service-transaction-behavior.md)
##### [Поведение отладки службы](service-debug-behavior.md)
##### [Регулирование](throttling.md)
##### [Безопасность поведений](behavior-security.md)
###### [Поведение аудита службы](service-auditing-behavior.md)
###### [Поставщик членства и ролей](membership-and-role-provider.md)
###### [Авторизация доступа к операциям службы](authorizing-access-to-service-operations.md)
###### [Олицетворение клиента](impersonating-the-client.md)
#### [Упрощенная конфигурация служб WCF](simplified-configuration-for-wcf-services.md)
#### [Использование стандартных конечных точек](usage-of-standard-endpoints.md)
#### [Иерархическая модель конфигурации](hierarchical-configuration-model.md)
#### [Расширенная политика защиты](extended-protection-policy.md)
#### [Производство канала настройки](configuration-channel-factory.md)
#### [Адресация](addressing.md)
#### [Императивное определение](imperative.md)
#### [Несколько контрактов](multiple-contracts.md)
#### [Несколько конечных точек](multiple-endpoints.md)
#### [Несколько конечных точек по одному ListenUri](multiple-endpoints-at-a-single-listenuri.md)
#### [OperationContextScope](operationcontextscope.md)
#### [Описание службы](service-description.md)
#### [ConcurrencyMode.Reentrant](concurrencymode-reentrant.md)
#### [Безопасность службы](service-security.md)
##### [Образец идентификации службы](service-identity-sample.md)
### [Синдикация](syndication.md)
#### [Автономный веб-канал диагностики](stand-alone-diagnostics-feed-sample.md)
#### [Слабо типизированные расширения](loosely-typed-extensions-sample.md)
### [Размещение в Интернете](web.md)
#### [Выбор дополнительного формата](advanced-format-selection.md)
#### [Автоматический выбор формата](automatic-format-selection.md)
#### [Базовая служба HTTP](basic-http-service.md)
#### [Основная служба ресурсов](basic-resource-service.md)
#### [AspNetRouteIntegration](aspnetrouteintegration.md)
#### [Условные методы Get и Put](conditional-get-and-put.md)
#### [Конечные точки SOAP и HTTP](soap-and-http-endpoints.md)
#### [Интеграция кэширования ASP.NET](aspnet-caching-integration.md)
#### [UriTemplate](uritemplate-sample.md)
#### [Таблица UriTemplate](uritemplate-table-sample.md)
#### [Диспетчер таблицы UriTemplate](uritemplate-table-dispatcher-sample.md)
## [Расширяемость](extensibility.md)
### [Расширяемость привязок](binding-extensibility.md)
#### [WSStreamedHttpBinding](wsstreamedhttpbinding.md)
### [Расширяемость каналов](channels-extensibility.md)
#### [Локальный канал](local-channel.md)
#### [Надежный защищенный профиль](reliable-secure-profile.md)
#### [Настраиваемый диспетчер каналов](custom-channel-dispatcher.md)
#### [Фрагментирование канала](chunking-channel.md)
#### [Канал подтверждений HTTP](http-acknowledgement-channel.md)
#### [HttpCookieSession](httpcookiesession.md)
#### [Пользовательский перехватчик сообщений](custom-message-interceptor.md)
### [Расширяемость обнаружения](discovery-extensibility.md)
#### [Метаданные CustomDiscoveryMetadata](customdiscoverymetadata.md)
### [Образцы расширяемости создания экземпляров](instancing-extensibility.md)
#### [Устойчивый контекст экземпляра](durable-instance-context.md)
#### [Пользовательские службы времени существования](custom-lifetime.md)
#### [Инициализация создания экземпляров](instancing-initialization.md)
#### [Объединение в пул](pooling.md)
### [Расширяемость взаимодействий](interop-extensibility.md)
#### [Передача по элементу тела сообщения](dispatch-by-body-element.md)
#### [Маршрутизация по телу сообщения](route-by-body.md)
### [Расширяемость кодировщика сообщений](message-encoder-extensibility.md)
#### [Пользовательский кодировщик сообщений: кодировщик пользовательских текстовых сообщений](custom-message-encoder-custom-text-encoder.md)
#### [Пользовательский кодировщик сообщений: кодировщик сжатия](custom-message-encoder-compression-encoder.md)
### [Расширяемость метаданных](metadata-extensibility.md)
#### [Пользовательская конечная точка защищенных метаданных](custom-secure-metadata-endpoint.md)
#### [Пользовательская публикация WSDL](custom-wsdl-publication.md)
### [Расширяемость средств обеспечения безопасности](security-extensibility.md)
#### [Пользовательский поставщик маркеров](durable-issued-token-provider.md)
#### [Поставщик маркеров SAML](saml-token-provider.md)
#### [Вспомогательные маркеры](supporting-tokens.md)
#### [Структура проверки подлинности маркера](token-authenticator.md)
#### [Поставщик маркеров](token-provider.md)
#### [Проверяющий элемент управления для имен пользователей и паролей](user-name-password-validator.md)
#### [Проверяющий элемент управления для сертификатов X.509](x-509-certificate-validator.md)
#### [Политика авторизации](authorization-policy.md)
#### [Пользовательский маркер](custom-token.md)
#### [Проверка клиента](client-validation.md)
### [Примеры расширяемости синдикации](syndication-extensibility-samples.md)
#### [Строго типизированные расширения](strongly-typed-extensions-sample.md)
#### [Модуль форматирования веб-канала (JSON)](feed-formatter-json.md)
#### [Потоковая передача каналов](streaming-feeds-sample.md)
### [Расширяемость транспорта](transport-extensibility.md)
#### [Активация UDP](udp-activation.md)
#### [Транспорт: пользовательские транзакции по протоколу UDP](transport-custom-transactions-over-udp-sample.md)
#### [Транспорт: UDP](transport-udp.md)
#### [Транспорт: TCP-взаимодействие WSE 3.0](transport-wse-3-0-tcp-interoperability.md)
### [Веб-расширяемость](web-extensibility.md)
#### [Передача формы](form-post.md)
### [Модуль форматирования и селектор операции](operation-formatter-and-operation-selector.md)
### [Пользовательский фильтр сообщений](custom-message-filter.md)
### [Пользовательский узел службы](custom-service-host.md)
### [Суррогат DataContract](datacontract-surrogate.md)
### [Повышение управляемости обработки ошибок и формирования сообщений об ошибках](extending-control-over-error-handling-and-reporting.md)
### [Инспекторы сообщений](message-inspectors.md)
### [WebContentTypeMapper](webcontenttypemapper-sample.md)
## [Сценарий](scenario.md)
### [Сценарии привязки данных](data-binding-scenarios.md)
#### [Привязка данных в клиенте Windows Forms](data-binding-in-a-windows-forms-client.md)
#### [Привязка данных в клиенте ASP.NET](data-binding-in-an-aspnet-client.md)
#### [Привязка данных в клиенте Windows Presentation Foundation](data-binding-in-a-wpf-client.md)
### [Образец безопасности при обнаружении](discovery-security-sample.md)
### [Пример федерации](federation-sample.md)
### [Сериализация слабо типизированных данных JSON (AJAX)](weakly-typed-json-serialization-sample.md)
### [Доверенная фасадная служба](trusted-facade-service.md)
### [Шаблоны разработки: публикация-подписка на основе списка](design-patterns-list-based-publish-subscribe.md)
## [Образцы средств](tool-samples.md)
### [ConfigurationCodeGenerator](configurationcodegenerator.md)
### [CustomChannelsTester](customchannelstester.md)
### [FindPrivateKey](findprivatekey.md)
