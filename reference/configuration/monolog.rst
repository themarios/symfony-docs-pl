.. index::
   pair: Monolog; konfiguracja

Konfiguracja pakietu Monolog
============================

.. configuration-block::

    .. code-block:: yaml

        monolog:
            handlers:

                # Examples:
                syslog:
                    type:                stream
                    path:                /var/log/symfony.log
                    level:               ERROR
                    bubble:              false
                    formatter:           my_formatter
                    processors:
                        - some_callable
                main:
                    type:                fingers_crossed
                    action_level:        WARNING
                    buffer_size:         30
                    handler:             custom
                custom:
                    type:                service
                    id:                  my_handler

                # Default options and values for some "my_custom_handler" 
                my_custom_handler:
                    type:                 ~ # Required
                    id:                   ~
                    priority:             0
                    level:                DEBUG
                    bubble:               true
                    path:                 "%kernel.logs_dir%/%kernel.environment%.log"
                    ident:                false
                    facility:             user
                    max_files:            0
                    action_level:         WARNING
                    activation_strategy:  ~
                    stop_buffering:       true
                    buffer_size:          0
                    handler:              ~
                    members:              []
                    channels:
                        type:     ~
                        elements: ~
                    from_email:           ~
                    to_email:             ~
                    subject:              ~
                    mailer:               ~
                    email_prototype:
                        id:                   ~ # Required (when the email_prototype is used)
                        method:               ~
                    channels:
                        type:                 ~
                        elements:             []
                    formatter:            ~

    .. code-block:: xml

        <container xmlns="http://symfony.com/schema/dic/services"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:monolog="http://symfony.com/schema/dic/monolog"
            xsi:schemaLocation="http://symfony.com/schema/dic/services http://symfony.com/schema/dic/services/services-1.0.xsd
                                http://symfony.com/schema/dic/monolog http://symfony.com/schema/dic/monolog/monolog-1.0.xsd">

            <monolog:config>
                <monolog:handler
                    name="syslog"
                    type="stream"
                    path="/var/log/symfony.log"
                    level="error"
                    bubble="false"
                    formatter="my_formatter"
                />
                <monolog:handler
                    name="main"
                    type="fingers_crossed"
                    action-level="warning"
                    handler="custom"
                />
                <monolog:handler
                    name="custom"
                    type="service"
                    id="my_handler"
                />
            </monolog:config>
        </container>

.. note::

    Gdy profiler jest włączony, dodawana jest obsługa składowania logów  w profilerze.
    Profiler stosuje nazwę "debug", tak więc jest ona zastrzeżona i nie może być
    używana w konfiguracji.
