.. _payloadtype-com.apple.mobiledevice.passwordpolicy:

Password Policy
===============
:download:`Template <../_static/examples/com.apple.mobiledevice.passwordpolicy.mobileconfig>`

On iOS, the key names generally reflect the expected functionality.

On macOS, these settings will affect the password policy of a directory node.
Additionally, some settings are applied via plist ``com.apple.screensaver``. Most keys are translated into policy
settings, see :ref:`pwpolicy` for more information.

.. contents::

Summary
-------

.. pfmheader:: /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Keys
----

.. pfmkey:: manualFetchingWhenRoaming /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist
.. pfmkey:: allowSimple /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

.. note:: A simple passcode is defined as containing repeated characters, or increasing/decreasing characters (such as 123 or CBA).
    Setting this value to false is synonymous to setting minComplexChars to "1".


.. pfmkey:: forcePIN /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

.. note:: Determines whether the user is forced to set a PIN.
    Simply setting this value (and not others) forces the user to enter a passcode, without imposing a length or quality.


.. pfmkey:: maxFailedAttempts /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

.. note:: Allowed range [1...10]. Specifies the number of allowed failed attempts to enter the passcode at the device's lock screen.
    Once this number is exceeded, the device is locked and must be connected to its designated iTunes in order to be unlocked.

.. _payloadkey-com.apple.mobiledevice.passwordpolicy.maxInactivity:
.. pfmkey:: maxInactivity /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Default Infinity. Specifies the number of minutes for which the device can be idle (without being unlocked by the user) before it gets locked by the system.
Once this limit is reached, the device is locked and the passcode must be entered.

In macOS, this translates to the key **idleTime** in ``/Library/Managed Preferences/com.apple.screensaver.plist``, which
is the number of seconds until the screen is locked.

macOS
    10.9+, possibly earlier

.. pfmkey:: maxPINAgeInDays /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Default Infinity. Specifies the number of days for which the passcode can remain unchanged.
After this number of days, the user is forced to change the passcode before the device is unlocked.

macOS
    10.9+

macOS 10.9
    This translates into the pwpolicy global policy field maxMinutesUntilChangePassword

macOS 10.10+
    This translates into an account policy containing the key **policyAttributeExpiresEveryNDays** equal to the maxInactivity value.


.. note:: Profile Manager lists the maximum PIN age for macOS to be 730 days.


.. pfmkey:: minComplexChars /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Specifies the minimum number of complex characters that a passcode must contain.
A "complex" character is a character other than a number or a letter, such as ``&%$#``.

macOS
    10.10+

macOS 10.10+
    This translates into an account policy that contains the rule ``policyAttributePassword matches '(.*[^a-zA-Z0-9].*){3,}'``.
    The number 3 in the regex signifies the configured number of complex characters.

.. note:: This implies the setting **allowSimple = FALSE** if minComplexChars is > 0

.. note:: Profile Manager lists the maximum as being 4

.. pfmkey:: minLength /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Specifies the minimum overall length of the passcode.
This parameter is independent of the also optional minComplexChars argument.

macOS
    10.10+

macOS 10.10+
    This translates into an account policy that contains the rule ``policyAttributePassword matches '.{4,}'``.
    The number 4 in the regex signifies the number of characters required.

.. note:: Profile Manager lists the maximum as being 16

.. pfmkey:: requireAlphanumeric /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Specifies whether the user must enter alphabetic characters ("abcd"), or if numbers are sufficient.

macOS
    10.10+

macOS 10.10+
    This translates into an account policy that contains the rule ``policyAttributePassword matches '^(?=.*[0-9])(?=.*[a-zA-Z]).+'``.


.. pfmkey:: pinHistory /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

When the user changes the passcode, it has to be unique within the last N entries in the history.
Minimum value is 1, maximum value is 50.

macOS
    10.9+

.. _payloadkey-com.apple.mobiledevice.passwordpolicy.maxGracePeriod:
.. pfmkey:: maxGracePeriod /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

The maximum grace period, in minutes, to unlock the phone without entering a passcode.
Default is 0, that is no grace period, which requires a passcode immediately.

In macOS, this translates to the key **askForPasswordDelay** which is the number of seconds as an integer until you
will need to unlock the account.

macOS
    10.9+, Possibly earlier

.. pfmkey:: allowFingerprintModification /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

.. pfmkey:: changeAtNextAuth /_static/manifests/com.apple.mobiledevice.passwordpolicy manifest.plist

Links
-----

- `Official Documentation <https://developer.apple.com/library/content/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html#//apple_ref/doc/uid/TP40010206-CH1-SW9>`_.

