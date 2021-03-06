GPIO Switch
===========

.. seo::
    :description: Instructions for setting up GPIO pin switches in esphomelib that control GPIO outputs.
    :image: pin.png

The ``gpio`` switch platform allows you to use any pin on your node as a
switch. You can for example hook up a relay to a GPIO pin and use it
through this platform.

.. figure:: images/gpio-ui.png
    :align: center
    :width: 80.0%

.. code-block:: yaml

    # Example configuration entry
    switch:
      - platform: gpio
        pin: 25
        name: "Living Room Dehumidifier"

Configuration variables:
------------------------

- **pin** (**Required**, :ref:`Pin Schema <config-pin_schema>`): The
  GPIO pin to use for the switch.
- **name** (**Required**, string): The name for the switch.
- **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.
- **restore_mode** (*Optional*): Control how the GPIO Switch attempts to restore state on bootup.

    - ``RESTORE_DEFAULT_OFF`` (Default) - Attempt to restore state and default to OFF if not possible to restore.
    - ``RESTORE_DEFAULT_ON`` - Attempt to restore state and default to ON.
    - ``ALWAYS_OFF`` - Always initialize the pin as OFF on bootup.
    - ``ALWAYS_ON`` - Always initialize the pin as ON on bootup.

- All other options from :ref:`Switch <config-switch>` and :ref:`MQTT Component <config-mqtt-component>`.

To create an active-low switch (one that is turned off by default), use the :ref:`Pin Schema <config-pin_schema>`:

.. code-block:: yaml

    # Example configuration entry
    switch:
      - platform: gpio
        pin:
          number: 25
          inverted: yes

To create momentary switches, for example switches that toggle a pin for a moment, you can use :doc:`template switches <template>`.

An example that uses a single relay to activate a remote control button. The button can only start or stop the motor of the gate. In itself, the button or remote can not know if it opens or closes the gate. The relay simulates the button press for 500ms.

.. code-block:: yaml

    # Example configuration entry
    switch:
      - platform: gpio
        pin: 25
        id: relay
      - platform: template
        name: "Gate Remote"
        icon: "mdi:gate"
        optimistic: no
        turn_on_action:
        - switch.turn_on: relay
        - delay: 500ms
        - switch.turn_off: relay

.. figure:: images/gate-remote-ui.png
    :align: center

See Also
--------

- :doc:`index`
- :doc:`/esphomeyaml/components/output/gpio`
- :doc:`/esphomeyaml/components/cover/template`
- :doc:`/esphomeyaml/cookbook/garage-door`
- :doc:`API Reference </api/switch/index>`
- `Edit this page on GitHub <https://github.com/OttoWinter/esphomedocs/blob/current/esphomeyaml/components/switch/gpio.rst>`__

.. disqus::
