``avLuaDevice``
===============

.. seealso::
    If you're looking to implement a common system, such as
    :doc:`animation & movement of a landing gear <lua.api.landing_gear_system>`,
    please check :doc:`our guides <guide>`.

Represents a builtin device written in Lua, often used for cockpit avionics.

This file may contain any code you want, and will be executed with the appropriate
DCS Lua API functions exposed:

Hooks
-----

.. function:: SetCommand(input_id, value)

    Called whenever an input binding has been detected.

    :param input_id: The ID of the input, e.g. ``Joystick.CmsDown``.
    :type input_id: number
    :param value: The current value of the input.
    :type value: number

.. function:: CockpitEvent(name, value)

    Called whenever an in-game event has been detected:

    - GroundPowerOn
    - GroundPowerOff
    - GroundAirOff
    - GroundAirOn
    - GroundAirFailure
    - GroundAirApplyOn
    - GroundAirApplyOff
    - GroundAirApplyFailure
    - WeaponRearmFirstStep
    - WeaponRearmComplete
    - WeaponRearmSingleStepComplete
    - UnlimitedWeaponStationRestore
    - WheelChocksOn
    - WheelChocksOff
    - Repair
    - ReloadDone
    - RefuelDone
    - cockpit_release

    :param name: The name of the event.
    :type name: string
    :param value: The value associated with the event.
    :type value: any (implicit)

.. function:: GetSelf()

    Constructs an innermost table of the device specified in ``device_init.lua``.

    :returns: A table containing functions and data for the device.
    :rtype: `Device table <#device>`_

.. function:: post_initialize()

    Called upon starting a DCS mission.

.. function:: update()

    Called on an interval set by :func:`make_default_activity`.

.. function:: release()

    Called when the mission reloads, player dies or otherwise leaves the aircraft.
    Can be used to clean up any resources that are not cleaned up automatically.

----

.. function:: make_default_activity(seconds)

    Sets the callsite execution interval for the script. The recommended value is ``0.01``,
    or 1/10th a millisecond.

    :param seconds: The amount of time in-between intervals.
    :type seconds: number
    :returns: nil (implicit)

Functions
---------

.. function:: get_draw_aircraft_argument_value(number)
    
    Gets the current value of an animation argument from the exterior :term:`EDM`.

    :returns: The associated value.
    :rtype: number

.. function:: set_draw_aircraft_argument_value(number)

    Sets a value to the specified animation argument for the exterior :term:`EDM`.

    :returns: nil (implicit)

.. function:: get_cockpit_draw_argument_value(number)

    Gets the current value of an animation argument for the interior :term:`EDM`.

    :returns: The associated value.
    :rtype: number

----

.. function:: show_param_handles_list(show_imgui)

    Toggles an :term:`ImGui` widget window on and off in-game.

    :param show_imgui: Should ImGui be shown in-game?
    :type show_imgui: boolean
    :returns: ?

.. function:: dispatch_action(device_id, input_id, value)

    Triggers an involuntary input with a desired value. Similar to
    :func:`performClickableAction`, this will only result in a
    :func:`SetCommand` call.

    :param device_id: The ID of the device to use.
    :type device_id: string
    :param input_id: The ID of the input to use.
    :type input_id: number
    :param value: The value to trigger the device input with.
    :type value: number
    :returns: nil (implicit)

.. function:: print_message_to_user(string)

    Prints string text in-game in the top right corner.

    :returns: nil (implicit)

----

.. function:: get_base_data()

    Gets sensor data all over the aircraft from in-game.

    :returns: A table with functions for different sensor values.
    :rtype: `BaseData table <#base-data>`_

BaseData
********

.. function:: getAngleOfAttack()

    Gets the current angle of attack.

    :rtype: number

.. function:: getAngleOfSlide()

    Gets the current angle of slide.

    :rtype: number

.. function:: getBarometricAltitude()

    Gets the current altitude in barometric unit.

    :rtype: number

.. function:: getCanopyPos()

    Gets the current position of the canopy.

    :rtype: number

.. function:: getCanopyState()

    Gets the current state of the canopy, e.g. damaged, open, closed.

    :rtype: number (???)

.. function:: getEngineLeftFuelConsumption()

    Gets the current fuel consumption rate of the left engine.

    :rtype: number

.. function:: getEngineLeftRPM()

    Gets the current RPM percentage of the left engine.

    :rtype: number

.. function:: getEngineLeftTemperatureBeforeTurbine()

    Gets the current temperature of the left engine (in Celsius) before
    statrtup.

    :rtype: number

.. function:: getEngineRightFuelConsumption()

    Gets the current fuel consumption rate of the right engine.

    :rtype: number

.. function:: getEngineRightRPM()

    Gets the current RPM percentage of the right engine.

    :rtype: number

.. function:: getEngineRightTemperatureBeforeTurbine()

    Gets the current temperature of the right engine (in Celsius) before
    statrtup.

    :rtype: number

.. function:: getFlapsPos()

    Gets the current position of the flaps.

    :rtype: number

.. function:: getFlapsRetracted()

    Gets the current position of the flaps underneath the retraction threshold,
    used for aircraft definitions that have multiple flap states.

    :rtype: number

.. function:: getHeading()

    Gets the current *relative* heading in degrees. (not to be confused with
    :func:`getMagneticHeading`)

    :rtype: number

.. function:: getHorizontalAcceleration()
    
    Gets the current rate of horizontal acceleration, in meters per second.

    :rtype: number

.. function:: getIndicatedAirSpeed()

    Gets the current in-air speed (`IAS <https://en.wikipedia.org/wiki/Indicated_airspeed>`_)
    in knots per second.

    :rtype: number

.. function:: getLandingGearHandlePos()

    Gets the current position state of the landing gear handle, used for aircraft
    definitions that have multiple gear states.

    :rtype: number

.. function:: getLateralAcceleration()

    Gets the current rate of lateral (side-by-side) acceleration, in meters per second.

    :rtype: number

.. function:: getLeftMainLandingGearDown()

    Gets the current state of the left landing gear and checks if it is down.

    :returns: Truthy expression
    :rtype: number

.. function:: getLeftMainLandingGearUp()

    Gets the current state of the left landing gear and checks if it is up.

    :returns: Truthy expression
    :rtype: number

.. function:: getMachNumber()

    Gets the current mach number.

    :rtype: number

.. function:: getMagneticHeading()

    Gets the current *true* (magnetic) heading in degrees.

    :rtype: number

.. function:: getNoseLandingGearDown()

    Gets the current state of the nose landing gear and checks if it is down.

    :returns: Truthy expression
    :rtype: number

.. function:: getNoseLandingGearUp()

    Gets the current state of the nose landing gear and checks if it is up.

    :returns: Truthy expression
    :rtype: number

.. function:: getPitch()

    Gets the current pitch angle in degrees.

    :rtype: number

.. function:: getRadarAltitude()

    Gets the current altitude via. radar in degrees.

    :rtype: number

.. function:: getRateOfPitch()

    Gets the current rate of pitch in degrees per second.

    :rtype: number

.. function:: getRateOfRoll()

    Gets the current rate of roll in degrees per second.

    :rtype: number

.. function:: getRateOfYaw()

    Gets the current rate of yaw in degrees per seocnd.

    :rtype: number

.. function:: getRightMainLandingGearDown()

    Gets the current state of the right landing gear and checks if it is down.

    :returns: Truthy expression
    :rtype: number

.. function:: getRightMainLandingGearUp()

    Gets the current state of the right landing gear and checks if it is up.

    :returns: Truthy expression
    :rtype: number

.. function:: getRoll()

    Gets the current roll/bank angle in degrees.

    :rtype: number

.. function:: getRudderPosition()

    Gets the current vertical stabiliser(s)' position in degrees.

    :rtype: number

.. function:: getSpeedBrakePos()

    Gets the current position of the speedbrake, used for aircraft definitions
    with one defined.

    :rtype: number

----

.. function:: get_param_handle(name)

    Gets the name of a defined :doc:`parameter <lua.api.parameter>` with a handler.

    :param name: The name of the parameter.
    :type name: string
    :returns: A table with functions and data for handling.
    :rtype: `Handler table <#handler>`_

Handler
*******

Handlers are a special DCS construct made for controlling the state
of parameters when conditions [#1]_ are present.

.. function:: set(number)

    Sets the value of the parameter.

    :returns: nil (implicit)

.. function:: get()

    Gets the current parameter value.

    :rtype: number

Device
------

A "device" in this context is the state of a process within a plugin.
This includes the ability to add additional Lua table elements, as well
as add event hooks with functions.

.. function:: listen_command(input_id)

    Checks and calls :func:`SetCommand` when a specified
    :doc:`input profile <lua.input>` binding has been detected.

    :param input_id: The ID of the input, e.g. ``Keys.PlaneGearDown``.
    :type input_id: number
    :returns: nil (implicit)

.. function:: listen_event(name)

    Checks and calls :func:`CockpitEvent` when an event has been detected.

    :param name: The name of the event.
    :type name: string
    :returns: nil (implicit)

----

.. function:: performClickableAction(input_id, value, ???)

    Triggers an involuntary input with a desire value. This will lead to
    :func:`SetCommand` and/or :func:`CockpitEvent` called.

    (Not to be confused with :func:`dispatch_action`)

    :param input_id: The ID of the input to use.
    :type input_id: number
    :param value: The value associated with the input.
    :type value: number
    :param ???:
    :type ???: boolean

.. [#1] Calling ``update()`` with ``if``, ``for`` and ``while`` expressions present.