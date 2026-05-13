---
title: ASUS TUF GAMING X870-PLUS BM
source: ASUS_TUF_GAMING_X870-PLUS_BM.pdf
format: auto-extracted from PDF via pdftotext -layout, post-processed
---

              Motherboard
PRIME /
ProArt /
TUF GAMING
AMD 800
Series

BIOS Manual

    E25269
    First Edition
    December 2024

    Copyright© 2024 ASUSTeK COMPUTER INC. All Rights Reserved.
    No part of this manual, including the products and software described in it, may be reproduced,
    transmitted, transcribed, stored in a retrieval system, or translated into any language in any form or by any
    means, except documentation kept by the purchaser for backup purposes, without the express written
    permission of ASUSTeK COMPUTER INC. (“ASUS”).
    Product warranty or service will not be extended if: (1) the product is repaired, modified or altered, unless
    such repair, modification of alteration is authorized in writing by ASUS; or (2) the serial number of the
    product is defaced or missing.
    ASUS PROVIDES THIS MANUAL “AS IS” WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS
    OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OR CONDITIONS OF
    MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. IN NO EVENT SHALL ASUS, ITS
    DIRECTORS, OFFICERS, EMPLOYEES OR AGENTS BE LIABLE FOR ANY INDIRECT, SPECIAL, INCIDENTAL,
    OR CONSEQUENTIAL DAMAGES (INCLUDING DAMAGES FOR LOSS OF PROFITS, LOSS OF BUSINESS,
    LOSS OF USE OR DATA, INTERRUPTION OF BUSINESS AND THE LIKE), EVEN IF ASUS HAS BEEN ADVISED
    OF THE POSSIBILITY OF SUCH DAMAGES ARISING FROM ANY DEFECT OR ERROR IN THIS MANUAL OR
    PRODUCT.
    SPECIFICATIONS AND INFORMATION CONTAINED IN THIS MANUAL ARE FURNISHED FOR
    INFORMATIONAL USE ONLY, AND ARE SUBJECT TO CHANGE AT ANY TIME WITHOUT NOTICE, AND
    SHOULD NOT BE CONSTRUED AS A COMMITMENT BY ASUS. ASUS ASSUMES NO RESPONSIBILITY OR
    LIABILITY FOR ANY ERRORS OR INACCURACIES THAT MAY APPEAR IN THIS MANUAL, INCLUDING THE
    PRODUCTS AND SOFTWARE DESCRIBED IN IT.
    Products and corporate names appearing in this manual may or may not be registered trademarks or
    copyrights of their respective companies, and are used only for identification or explanation and to the
    owners’ benefit, without intent to infringe.

2

Contents
 1.   Knowing BIOS.............................................................................................. 5
 2.   BIOS setup program..................................................................................... 6

## 2.1 EZ Mode...............................................................................................

## 2.2 Advanced Mode...................................................................................

## 2.3 Qfan Control.......................................................................................11

## 2.4 AI OC Guide........................................................................................11

## 2.5 Q-Dashboard......................................................................................12

 3.   My Favorites.............................................................................................. 13
 4.   Main menu................................................................................................. 15
 5.   Ai Tweaker menu....................................................................................... 17
 6.   Advanced menu......................................................................................... 48

## 6.1 Trusted Computing............................................................................48

## 6.2 AMD fTPM configuration..................................................................49

## 6.3 UEFI Variables Protection.................................................................50

## 6.4 CPU Configuration.............................................................................50

## 6.5 PCI Subsystem Settings....................................................................50

## 6.6 USB Configuration.............................................................................51

## 6.7 Network Stack Configuration............................................................51

## 6.8 NVMe Configuration..........................................................................52

## 6.9 HDD/SSD SMART Information..........................................................52

## 6.10 SATA Configuration...........................................................................52

## 6.11 APM Configuration............................................................................53

## 6.12 Onboard Devices Configuration........................................................54

## 6.13 NB Configuration...............................................................................56

## 6.14 AMD CBS............................................................................................57

## 6.15 AMD PBS............................................................................................76

## 6.16 AMD Overclocking.............................................................................78

 7.   Monitor menu............................................................................................ 94
 8.   Boot menu............................................................................................... 104
 9.   Tool menu................................................................................................ 109

## 9.1 ASUS EZ Flash 3 Utility....................................................................110

## 9.2 ASUS Secure Erase..........................................................................110

## 9.3 BIOS Q-Dashboard...........................................................................110

## 9.4 ASUS User Profile............................................................................111

## 9.5 ASUS SPD Information....................................................................111

## 9.6 ASUS MyHotkey...............................................................................111

## 9.7 ASUS DriverHub...............................................................................112

                                                                                                                                3

    10.   Exit menu................................................................................................. 113
    11.   Updating BIOS......................................................................................... 114

## 11.1 ASUS EZ Flash 3..............................................................................114

## 11.2 ASUS CrashFree BIOS 3..................................................................115

4

BIOS Setup
1.           Knowing BIOS
     NOTE: The new ASUS UEFI BIOS is a Unified Extensible Interface that complies with UEFI
     architecture, offering a user-friendly interface that goes beyond the traditional keyboard-only BIOS
     controls to enable a more flexible and convenient mouse input. You can easily navigate the new
     UEFI BIOS with the same smoothness as your operating system. The term “BIOS” in this user
     manual refers to “UEFI BIOS” unless otherwise specified.

BIOS (Basic Input and Output System) stores system hardware settings such as storage
device configuration, overclocking settings, advanced power management, and boot
device configuration that are needed for system startup in the motherboard CMOS. In
normal circumstances, the default BIOS settings apply to most conditions to ensure
optimal performance. DO NOT change the default BIOS settings except in the following
circumstances:
•    An error message appears on the screen during the system bootup and requests you
     to run the BIOS Setup.
•    You have installed a new system component that requires further BIOS settings or
     update.

     CAUTION! Inappropriate BIOS settings may result to instability or boot failure. We strongly
     recommend that you change the BIOS settings only with the help of a trained service personnel.

     IMPORTANT! We Strongly recommend ALWAYS using the ZIP file from the ASUS website to
     update your BIOS when using ASUS EZ Flash, so that the ME version will be updated as well. If you
     opt to only use the CAP file, make sure the ME version matches the new BIOS. Keep in mind that
     once the ME is updated, it cannot be rolled back. For more information please check the product
     page on the ASUS website.

     NOTE:
     • When downloading or updating the BIOS file for your motherboard, rename it as XXXXX.CAP or
       launch the BIOSRenamer.exe application to automatically rename the file. The name of the CAP
       file varies depending on models. Refer to the user manual that came with your motherboard for
       the name.
     • The screenshots in this manual are for reference only, please refer to the latest BIOS version for
       settings and options.
     • BIOS settings and options may vary due to different BIOS release versions or CPU installed.
       Please refer to the latest BIOS version for settings and options.

                                                                                                            5

    2.            BIOS setup program
    Use the BIOS Setup to update the BIOS or configure its parameters. The BIOS screen include
    navigation keys and brief onscreen help to guide you in using the BIOS Setup program.

    Entering BIOS at startup
    To enter BIOS Setup at startup, press <Delete> or <F2> during the Power-On Self Test
    (POST). If you do not press <Delete> or <F2>, POST continues with its routines.

    Entering BIOS Setup after POST
    To enter BIOS Setup after POST:
    •     Press <Ctrl>+<Alt>+<Delete> simultaneously.
    •     Press the reset button on the system chassis.
    •     Press the power button to turn the system off then back on. Do this option only if you
          failed to enter BIOS Setup using the first two options.
    After doing either of the three options, press <Delete> key to enter BIOS.

          IMPORTANT!
          • The BIOS setup screens shown in this section are for reference purposes only, and may not
            exactly match what you see on your screen.
          • Ensure that a USB mouse is connected to your motherboard if you want to use the mouse to
            control the BIOS setup program.
          • If the system becomes unstable after changing any BIOS setting, load the default settings to
            ensure system compatibility and stability. Select the Load Optimized Defaults item under the
            Exit menu or press hotkey <F5>. See section Exit menu for details.
          • If the system fails to boot after changing any BIOS setting, try to clear the CMOS and reset the
            motherboard to the default value. See your motherboard manual for information on how to
            erase the RTC RAM.
          • The BIOS setup program does not support Bluetooth devices.

    BIOS menu screen
    The BIOS Setup program can be used under two modes: EZ Mode and Advanced Mode. You
    can change modes from Setup Mode in Boot menu or by pressing the <F7> hotkey.

          NOTE: The BIOS settings and options for each motherboard may differ slightly with the
          screenshots in this manual. Please refer to the BIOS of your motherboard for the actual settings
          and options.

6

## 2.1 EZ Mode

 The EZ Mode provides you an overview of the basic system information, and allows you to
 select the display language, system performance, mode and boot device priority. To access
 the Advanced Mode, select Advanced Mode(F7) or press the <F7> hotkey for the advanced
 BIOS settings.

         NOTE: The default screen for entering the BIOS setup program can be changed. Refer to the Setup
         Mode item in section Boot menu for details.

Displays a quick overview of the system status                  Displays the system properties of the selected mode.
                                                                Click < or > to switch modes
               Selects the display language
               of the BIOS setup program     ReSize BAR
                                   Search AURA

                Displays the CPU Fan’s speed. Click the
                button to manually tune the fans          Click to go to Q-Dashboard
                                                                              Loads optimized
                                                                              default settings
                                                                                       Saves the changes and
                                                                                       resets the system
                                                                                       Click to go to Advanced mode
                                                                                       Click to display boot devices
                                                                           Selects the boot device priority

         NOTE: The boot device options vary depending on the devices you installed to the system.

                                                                                                                       7

## 2.2 Advanced Mode

    The Advanced Mode provides advanced options for experienced end-users to configure
    the BIOS settings. The figure below shows an example of the Advanced Mode. Refer to the
    following sections for the detailed configurations.

            NOTE: To switch from EZ Mode to Advanced Mode, click Advanced Mode(F7) or press the <F7>
            hotkey.

    Configuration fields                                                                  Scroll bar
    Pop-up Menu
                 Language               Qfan Control        AURA
    Menu bar                  My Favorite          Search          ReSize BAR

       Submenu items         General help             Click to go to Q-Dashboard Last modified            Hot keys
       Menu items                                                                settings
                                                                                          Go back to EZ Mode
                                                                                    Displays a quick overview of the
                                                                                    system status and prediction

    Menu bar
    The menu bar on top of the screen has the following main items:

     My Favorites            For saving the frequently-used system settings and configuration.
     Main                    For changing the basic system configuration
     Ai Tweaker              For changing the overclocking settings
     Advanced                For changing the advanced system settings
                             For displaying the system temperature, power status, and changing
     Monitor
                             the fan settings.
     Boot                    For changing the system boot configuration
     Tool                    For configuring options for special functions
     Exit                    For selecting the exit options and loading default settings

8

Menu items
The highlighted item on the menu bar displays the specific items for that menu. For
example, selecting Main shows the Main menu items. The other items on the menu bar have
their respective menu items.

Submenu items
An arrow sign (>) before each item on any menu screen means that the item has a submenu.
To display the submenu, select the item and press <Enter>.

Language
This button above the menu bar contains the languages that you can select for your BIOS.
Click this button to select the language that you want to display in your BIOS screen.

My Favorite
This button above the menu bar shows all BIOS items in a Tree Map setup. Select frequently-
used BIOS settings and save it to My Favorites menu. You may also access this item by
pressing the <F3> key on the keyboard.

       NOTE: Refer to section My Favorites for more information.

Qfan
This button above the menu bar displays the current settings of your fans. Use this button to
manually tweak the fans to your desired settings. You may also access this item by pressing
the <F6> key on the keyboard.

       NOTE: Refer to section Qfan Control for more information.

AI OC Guide
This button above the menu bar allows you to view the descriptions of AI overclocking and
enable it. You may also access this item by pressing the <F11> key on the keyboard.

       NOTE:
       • Refer to section AI OC Guide for more information.
       • This function is only enabled when using an unlocked CPU.
       • This function is only available on selected models.

Search
This button allows you to search for BIOS items by entering its name, enter the item name to
find the related item listing. You may also access this item by pressing the <F9> key on the
keyboard.

AURA
This button allows you to turn the RGB LED lighting or functional LED on or off. You may also
access this item by pressing the <F4> key on the keyboard.
[All On]:           All LEDs (Aura or Functional) will be enabled.
[Stealth Mode]:     All LEDs (Aura and Functional) will be disabled.
[Aura Only]:        Aura LEDs will be enabled and functional LEDs will be disabled.
[Aura Off]:         Aura LEDs will be disabled, however functional LEDs will still be enabled.

                                                                                                 9

     ReSize BAR
     This button allows you to turn ReSize BAR function on or off.
     [On]	Enable ReSize BAR support to fully harness GPU memory. CSM
           (Compatibility Support Module) will be disabled.
     [Off]               ReSize BAR support will be disabled.

     Hot keys
     This button at the bottom right contains the navigation keys for the BIOS setup program. Use
     the navigation keys to select items in the menu and change the settings.

     Scroll bar
     A scroll bar appears on the right side of a menu screen when there are items that do not fit
     on the screen. Press the Up/Down arrow keys or <Page Up> / <Page Down> keys to display
     the other items on the screen.

     General help
     At the bottom of the menu screen is a brief description of the selected item. Use <F12> key
     to capture the BIOS screen and save it to the removable storage device.

     Configuration fields
     These fields show the values for the menu items. If an item is user-configurable, you can
     change the value of the field opposite the item. You cannot select an item that is not user-
     configurable.
     A configurable field is highlighted when selected. To change the value of a field, select it and
     press <Enter> to display a list of options.

     Last Modified button
     This button shows the items that you last modified and saved in BIOS Setup.

     Q-Dashboard
     This button allows you to view all the ports and connectors on your motherboard as well as
     quick access to the settings of these ports and connectors. You may also access this item
     by pressing the <Insert> key on the keyboard.

             NOTE: Refer to section Q-Dashboard for more information.

10

## 2.3 Qfan Control

The Qfan Control allows you to set a fan profile or manually configure the operating speed of
your CPU and chassis fans.

### 2.3.1 Configuring fans manually

Select Manual from the list of profiles to manually configure your fans’ operating speed.
To configure your fans:
1.      Select the fan that you want to configure and to view its current status.
2.      Click and drag the speed points to adjust the fans’ operating speed.
3.      Click Apply to save the changes then click Exit (ESC).

## 2.4 AI OC Guide

        NOTE:
        • This function is only enabled when using an unlocked CPU.
        • This function is only available on selected models.

The AI OC Guide allows you to enable the Ai Overclocking feature, or view a quick guide
of the Ai Overclocking feature which highlights the recommended setup procedure and
descriptions of the AI Overclocking.
Clicking on Enable AI will enable AI Overclocking.

                                                                                                11

## 2.5 Q-Dashboard

     The Q-Dashboard gives you a quick overview of the ports and connectors available on your
     motherboard. Clicking on a port or connector will redirect you to the BIOS setting of the
     selected port or connector.

                                                                          General help      Exit Q-Dashboard

     Displays device name if a device is
     connected to this port/connector
                                                               Display only the items of the selected group

12

3.            My Favorites
My Favorites is your personal space where you can easily save and access your favorite
BIOS items. You can personalize this screen by adding or removing items.

      NOTE: The screenshots in this section are for reference only and items listed may differ to your
      motherboard. Please refer to your motherboard for the actual items.

                                                                                                         13

       Adding items to My Favorites
       To add BIOS items:
       1.     Press <F3> on your keyboard or click MyFavorite from the BIOS screen to open Setup
              Tree Map screen.
       2.     On the Setup Tree Map screen, select an item from main menu panel, then click the
              submenu that you want to save as favorite from the submenu panel and click      or
              press <Enter> on your keyboard.

              NOTE: You cannot add the following items to My Favorite items:
              • Items with submenu options.
              • User-managed items such as language and boot order.
              • Configuration items such as Memory SPD Information, system time and date.

     Main menu panel
                                                                                            Selected shortcut items

      Submenu panel

                                                                                            Delete all favorite items

                                                                                            Recover to default
                                                                                            favorite items

       3.     Click Exit (ESC) or press <Esc> key to close Setup Tree Map screen.
       4.     Go to My Favorites menu to view the saved BIOS items.

14

4.            Main menu
The Main menu screen appears when you enter the Advanced Mode of the BIOS Setup
program. The Main menu provides you an overview of the basic system information, and
allows you to set the system date, time, language, and security settings.

System Language
Allows you to set the system default language.
System Date
Allows you to set the system date. Use <Tab> to switch between Date elements.
System Language
Allows you to set the system time. Use <Tab> to switch between Time elements.
Security
The Security menu items allow you to change the system security settings.

      NOTE:
      • If you have forgotten your BIOS password, erase the CMOS Real Time Clock (RTC) RAM to clear
        the BIOS password. See the motherboard for information on how to erase the RTC RAM.
      • The Administrator or User Password items on top of the screen show the default [Not
        Installed]. After you set a password, these items show [Installed].

                                                                                                      15

     Administrator Password
     If you already have an administrator password set, we recommend that you enter the
     administrator password for accessing the system. Otherwise, you might be able to see or
     change only selected fields in the BIOS setup program.
     To set an administrator password:
     1.    Select the Administrator Password item and press <Enter>.
     2.    In the Create New Password box, key in a password, then press <Enter>.
     3.    Re-type to confirm the password then select OK.
     To change an administrator password:
     1.    Select the Administrator Password item and press <Enter>.
     2.    In the Enter Current Password box, key in the current password, then press <Enter>.
     3.    In the Create New Password box, key in a new password, then press <Enter>.
     4.    Re-type to confirm the password then select OK.
     To clear an administrator password:
     1.    Select the Administrator Password item and press <Enter>.
     2.    In the Enter Current Password box, key in the current password, then press <Enter>.
     3.    Press <Enter> when prompted to create/confirm the password. After you clear
           the password, the Administrator Password item on top of the screen shows [Not
           Installed].

     User Password
     If you have set a user password, you must enter the user password for accessing the
     system. The User Password item on top of the screen shows the default [Not Installed].
     After you set a password, this item shows [Installed].
     To set a user password:
     1.    Select the User Password item and press <Enter>.
     2.    In the Create New Password box, key in a password, then press <Enter>.
     3.    Re-type to confirm the password then select OK.
     To change a user password:
     1.    Select the User Password item and press <Enter>.
     2.    In the Enter Current Password box, key in the current password, then press <Enter>.
     3.    In the Create New Password box, key in a new password, then press <Enter>.
     4.    Re-type to confirm the password then select OK.
     To clear a user password:
     1.    Select the User Password item and press <Enter>.
     2.    In the Enter Current Password box, key in the current password, then press <Enter>.
     3.    Press <Enter> when prompted to create/confirm the password. After you clear the
           password, the User Password item on top of the screen shows [Not Installed].

16

5.           Ai Tweaker menu
The Ai Tweaker menu items allow you to configure overclocking-related items.

      CAUTION! Be cautious when changing the settings of the Ai Tweaker menu items. Incorrect field
      values can cause the system to malfunction.

      NOTE: The configuration options for this section vary depending on the CPU and DIMM model you
      installed on the motherboard.

Scroll down to display other BIOS items.

Ai Overclock Tuner
[Auto]            Loads the optimal settings for the system.
[Manual]	When the manual mode is selected, the BCLK (base clock) frequency can
                  be assigned manually.
[DOCP I]	Load the DIMM’s default DOCP memory timings (CL, TRCD, TRP, TRAS)
                  and other memory parameters optimized by ASUS.
[DOCP II]         Load the DIMM’s complete default DOCP profile.
[DOCP Tweaked]	Load DOCP profile with tweaks for improved performance if config
                  matches.
[EXPO I]	Load the DIMM’s default EXPO memory timings (CL, TRCD, TRP, TRAS) and
                  other memory parameters optimized by ASUS.
[EXPO II]         Load the DIMM’s complete default EXPO profile.
[EXPO Tweaked]	Load EXPO profile with tweaks for improved performance if config
                  matches.
[EXPO on the fly] On the fly for dynamic control.
[AEMP]            Load the memory parameters profile optimized by ASUS if no DIMM
                  profiles detected.

      NOTE: The configuration options for this item vary depending on the DIMM model you installed on
      the motherboard.

                                                                                                        17

           NOTE: The following items appear only when Ai Overclock Tuner is set to [Manual], [DOCP I],
           [DOCP II], [DOCP Tweaked], [EXPO I], [EXPO II], [EXPO Tweaked], [EXPO on the fly], or [AEMP].

     BCLK Frequency
     Adjusts Base Clock Frequency for CPU and also PCIE. Default is 100. Please note that
     changing the BCLK will affect stability of devices, in particular SATA devices.

           NOTE: The following item appears only when Ai Overclock Tuner is set to [DOCP I], [DOCP II], or
           [DOCP Tweaked].

     DOCP
     Each profile has its own DRAM frequency, timing and voltage.

           NOTE: The following item appears only when Ai Overclock Tuner is set to [EXPO I], [EXPO II], or
           [EXPO Tweaked], or [EXPO on the fly].

     EXPO
     Each profile has its own DRAM frequency, timing and voltage.

           NOTE: The following item appears only when Ai Overclock Tuner is set to [AEMP].

     AEMP
     Each profile has its own DRAM frequency, timing and voltage.
     Memory Frequency
     Forces a DDR5 frequency slower than the common tCK detected via SPD.
     [Auto] [DDR5-2000 MHz] - [DDR5-12000 MHz]
     FCLK Frequency
     Specifies the FCLK frequency.
     Configuration options: [Auto] [800 MHz] - [3000 MHz]
     Core Performance Boost
     Automatically overclocks the CPU and DRAM to enhance system performance.
     Configuration options: [Auto] [Enabled] [Disabled]
     CPU Core Ratio
     Configuration options: [Auto] [CPU Core Ratio] [AI Optimized]

           NOTE: The following item appears only when CPU Core Ratio is set to [CPU Core Ratio].

     CPU Core Ratio
     Allows you to set the CPU core ratio. Use the <+> or <-> to adjust the value. The values range
     from 8.00 to 100.00 with an interval of 0.25.
     Configuration options: [Auto] [8.00] - [100.00]

18

CPU Core Ratio (Per CCX)
The sub-items in this menu allow you to adjust Core Ratios for each CCX.
      Core VID
      Allows you to specify a custom CPU core VID. Power saving features for idle cores
      (e.g. cc6 sleep) remain active.
      CCD 0
      CCX0 Ratio
      Allows you to specify a custom Core Ratio for this CCX. Use the <+> or <-> to adjust
      the value. The values range from 8.00 to 100.00 with an interval of 0.25.
      Configuration options: [Auto] [8.00] - [100.00]
      CCD 1
      CCX0 Ratio
      Allows you to specify a custom Core Ratio for this CCX. Use the <+> or <-> to adjust
      the value. The values range from 8.00 to 100.00 with an interval of 0.25.
      Configuration options: [Auto] [8.00] - [100.00]
      Dynamic OC Switcher
      Enabling this dynamically switches back and forth between OC mode and Default
      modes based on current and temperature threshold specified.
      Configuration options: [Auto] [Disabled] [Enabled]

      NOTE: The following items appear only when Dynamic OC Switcher is set to [Enabled].

      Current Threshold to Switch to OC Mode
      Set this threshold to control when the CPU goes into OC Mode and when it comes
      back to default. Bigger than this value = OC Mode, smaller than this value = Default
      Mode. Recommend a value of 40A for single CCD and 60A for two CCDs. In Amps
      unit.
      Calibrated Temperature Threshold to switch back
      Set this threshold to control when the CPU returns to default mode. When CPU
      Calibrated Temperature is bigger than this threshold, CPU returns to default. Likewise,
      when temperature is smaller than this threshold AND current is bigger than Current
      Threshold, CPU slips into OC Mode. In Celsius Unit.
      Hysteresis
      Higher number increase the time required to persist in state when crossing thresholds
      before switching. Set 0 for fastest reaction and increase this to require longer times to
      remain said state before activation.
      Overclocking Load Guard
      Enable to switch over to PBO Mode from OC Mode during periods of very heavy
      loading.
      Configuration options: [Auto] [Disable] [Enable]
Preference
Select Performance for better overall performance or Power Efficient for more energy
savings.
Configuration options: [Performance] [Power Efficient]

                                                                                                  19

     GPU Boost
     Set to [Manual] if you want to select the desired value in frequency range.
     Configuration options: [Auto] [Manual Mode]

           NOTE: The following item appears only when GPU Boost is set to [Manual Mode].

     GPU clock frequency
     Allows you to set the GPU clock frequency.
     DRAM Timing Control
     The sub-items in this menu allow you to set the DRAM timing control features. Use the
     <+> and <-> keys to adjust the value. To restore the default setting, type [Auto] using the
     keyboard and press the <Enter> key. You can also select various Memory Presets to load
     settings suitably tuned for some memory modules.

           CAUTION! Changing the values in this menu may cause the system to become unstable! If this
           happens, revert to the default settings.

           Primary Timings
           Tcl
           DRAM CAS# Latency, the value stepping is 2.
           Trcd
           DRAM RAS# to CAS# Delay.
           Trp
           DRAM RAS# PRE Time.
           Tras
           DRAM RAS# ACT Time.
           Secondary Timings
           Trc
           DRAM Row Cycle Time.
           Twr
           DRAM WRITE to READ Delay, the value stepping is 6.
           Refresh Interval
           Allows you to set Refresh Interval.
           Trfc1
           DRAM REF Cycle Time.
           Trfc2
           Allows you to set Trfc2.
           Trfcsb
           Allows you to set Trfcsb.
           Trtp
           DRAM READ to PRE Time.

20

TrrdL
DRAM RAS# to RAS# Delay(tRRDL).
TrrdS
DRAM RAS# to RAS# Delay(tRRDS).
Tfaw
Allows you to set Tfaw.
TwtrL
DRAM WRITE to READ Delay(tWTR_L).
TwtrS
DRAM WRITE to READ Delay(tWTR_S).
TrdrdScl
Allows you to set TrdrdScl.
TrdrdSc
Allows you to set TrdrdSc.
TrdrdSd
Allows you to set TrdrdSd.
Trdrddd
Allows you to set Trdrddd.
TwrwrScl
Allows you to set TwrwrScl.
TwrwrSc
Allows you to set TwrwrSc.
TwrwrSd
Allows you to set TwrwrSd.
TwrwrDd
Allows you to set TwrwrDd.
Twrrd
Allows you to set Twrrd.
Trdwr
Allows you to set Trdwr.
Additional Timings
IBUF_LPWR_MODE
Configuration options: [Auto] [Enabled] [Disabled]
ADDR_CMD_MODE
Configuration options: [Auto] [Buf] [UnBuf]
M_ORDERING
Configuration options: [Auto] [NORM] [STRICT] [RELAXED]
S_COL_WIDTH
Allows you to set S_COL_WIDTH.

                                                          21

     MC_SVA_TRIM0
     Allows you to set MC_SVA_TRIM0.
     MC_SVA_TRIM1
     Allows you to set MC_SVA_TRIM1.
     MC_SVA_TRIM2
     Allows you to set MC_SVA_TRIM2.
     MMCM_MULT_F
     Configuration options: [Auto] [Enabled] [Disabled]
     DRAM Signal Control
     DDR Turnaround Times
             Read Drift Adjustment P0
             AUTO - Read Drift Adjustment 0.
             Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1] [plus 1]
             [plus 2] [plus 3] [plus 4]
             Write Drift Adjustment P0
             AUTO - Write Drift Adjustment 0.
             Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1] [plus 1]
             [plus 2] [plus 3] [plus 4]
     DDR PMU Training
             Read Preamble P0
             Specifies the Read Preamble P0.
             Configuration options: [Auto] [1 tCK - 10 Pattern] [2 tCK - 0010 Pattern] [2 tCK -
             1110 Pattern (DDR4 Style)] [3 tCK - 000010 Pattern] [4 tCK - 00001010 Pattern]
             Write Preamble P0
             Specifies the Write Preamble P0.
             Configuration options: [Auto] [2 tCK - 0010 Pattern] [3 tCK - 000010 Pattern] [4
             tCK - 00001010 Pattern]
             PHY VrefDAC0 P0 Control
             Configuration options: [Auto] [Manual]
             PHY VrefDAC1 P0 Control
             Configuration options: [Auto] [Manual]
             PMU DQ Vref P0 Control
             Configuration options: [Auto] [Manual]
             ARdPtrInitVal P0 Control
             [Auto]     Follow default setting.
             [Manual]   Manually specify ARdPtrInitValMP0.
     Processor ODT P0-P3 Page
             CA ODT GroupA
             Specifies the CA ODT.
             Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
             (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]
             CK ODT GroupA
             Specifies the CK ODT.
             Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
             (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]

22

CS ODT GroupA
Specifies the CS ODT.
Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
(120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]
CA ODT GroupB
Specifies the CA ODT.
Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
(120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]
CK ODT GroupB
Specifies the CK ODT.
Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
(120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]
CS ODT GroupB
Specifies the CS ODT.
Configuration options: [Auto] [RTT_OFF] [RZQ/0.5 (480)] [RZQ/1 (240)] [RZQ/2
(120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6 (40)]
Processor ODT P state mode
Processor ODT P state mode.
Configuration options: [Sync all P-states] [By per P-states]
Processor ODT P0 Page
Processor ODT Impedance Pull Up P0
Specifies the Processor ODT Impedance Pull Up P0.
Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
ohm]
Processor ODT Impedance Pull Down P0
Specifies the Processor ODT Impedance Pull Down P0.
Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
ohm]
Processor DQ drive strengths Pull Up P0
Processor DQ drive strengths Pull Up P0.
Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
[60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
Processor DQ drive strengths Pull Down P0
Processor DQ drive strengths Pull Down P0.
Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
[60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
Dram ODT Impedance RTT_NOM_WR P0
Dram ODT Impedance RTT_NOM_WR P0.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
Dram ODT impedance RTT_NOM_RD P0
Dram ODT impedance RTT_NOM_RD P0.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]

                                                                               23

     Dram ODT impedance RTT_WR P0
     Dram ODT impedance RTT_WR P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance RTT_PARK P0
     Dram ODT impedance RTT_PARK P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance DQS_RTT_PARK P0
     Dram ODT impedance DQS_RTT_PARK P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram DQ drive strengths Pull Up P0
     Dram DQ drive strengths Pull Up P0.
     Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
     Dram DQ drive strengths Pull Down P0
     Dram DQ drive strengths Pull Down P0.
     Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
     Processor ODT P1 Page
     Processor ODT Impedance Pull Up P1
     Processor ODT Impedance Pull Up P1.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
     ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
     ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
     ohm]
     Processor ODT Impedance Pull Down P1
     Processor ODT Impedance Pull Down P1.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
     ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
     ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
     ohm]
     Processor DQ drive strengths Pull Up P1
     Processor DQ drive strengths Pull Up P1.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
     [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Processor DQ drive strengths Pull Down P1
     Processor DQ drive strengths Pull Down P1.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
     [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Dram ODT Impedance RTT_NOM_WR P1
     Dram ODT Impedance RTT_NOM_WR P1.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance RTT_NOM_RD P1
     Dram ODT impedance RTT_NOM_RD P1.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]

24

Dram ODT impedance RTT_WR P1
Dram ODT impedance RTT_WR P1.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
Dram ODT impedance RTT_PARK P1
Dram ODT impedance RTT_PARK P1.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
Dram ODT impedance DQS_RTT_PARK P1
Dram ODT impedance DQS_RTT_PARK P1.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
Dram DQ drive strengths Pull Up P1
Dram DQ drive strengths Pull Up P1.
Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
Dram DQ drive strengths Pull Down P1
Dram DQ drive strengths Pull Down P1.
Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
Processor ODT P2 Page
Processor ODT Impedance Pull Up P2
Processor ODT Impedance Pull Up P2.
Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
ohm]
Processor ODT Impedance Pull Down P2
Processor ODT Impedance Pull Down P2.
Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
ohm]
Processor DQ drive strengths Pull Up P2
Processor DQ drive strengths Pull Up P2.
Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
[60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
Processor DQ drive strengths Pull Down P2
Processor DQ drive strengths Pull Down P2.
Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
[60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
Dram ODT Impedance RTT_NOM_WR P2
Dram ODT Impedance RTT_NOM_WR P2.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
Dram ODT impedance RTT_NOM_RD P2
Dram ODT impedance RTT_NOM_RD P2.
Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
(80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]

                                                                              25

     Dram ODT impedance RTT_WR P2
     Dram ODT impedance RTT_WR P2.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance RTT_PARK P2
     Dram ODT impedance RTT_PARK P2.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance DQS_RTT_PARK P2
     Dram ODT impedance DQS_RTT_PARK P2.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram DQ drive strengths Pull Up P2
     Dram DQ drive strengths Pull Up P2.
     Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
     Dram DQ drive strengths Pull Down P2
     Dram DQ drive strengths Pull Down P2.
     Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
     Processor ODT P3 Page
     Processor ODT Impedance Pull Up P3
     Processor ODT Impedance Pull Up P3.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
     ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
     ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
     ohm]
     Processor ODT Impedance Pull Down P3
     Processor ODT Impedance Pull Down P3.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160
     ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm] [48 ohm] [43
     ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28 ohm] [26 ohm] [25
     ohm]
     Processor DQ drive strengths Pull Up P3
     Processor DQ drive strengths Pull Up P3.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
     [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Processor DQ drive strengths Pull Down P3
     Processor DQ drive strengths Pull Down P3.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm]
     [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Dram ODT Impedance RTT_NOM_WR P3
     Dram ODT Impedance RTT_NOM_WR P3.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT impedance RTT_NOM_RD P3
     Dram ODT impedance RTT_NOM_RD P3.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
     (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]

26

       Dram ODT impedance RTT_WR P3
       Dram ODT impedance RTT_WR P3.
       Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
       (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
       Dram ODT impedance RTT_PARK P3
       Dram ODT impedance RTT_PARK P3.
       Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
       (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
       Dram ODT impedance DQS_RTT_PARK P3
       Dram ODT impedance DQS_RTT_PARK P3.
       Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3
       (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
       Dram DQ drive strengths Pull Up P3
       Dram DQ drive strengths Pull Up P3.
       Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
       Dram DQ drive strengths Pull Down P3
       Dram DQ drive strengths Pull Down P3.
       Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
Proc CS Drive Strength
Proc CS Drive Strength.
Configuration options: [Auto] [120 ohm] [60 ohm] [40 ohm] [30 ohm]
Proc CK Drive Strength
Proc CK Drive Strength.
Configuration options: [Auto] [120 ohm] [60 ohm] [40 ohm] [30 ohm]
Proc CA Drive Strength
Proc CA Drive Strength.
Configuration options: [Auto] [120 ohm] [60 ohm] [40 ohm] [30 ohm]
Proc Data Drive Strength
Proc Data Drive Strength.
Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm] [80 ohm] [60
ohm] [48 ohm] [40 ohm] [34.3 ohm]
CPU On-Die Termination
CPU On-Die Termination(ProcODT).
Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm] [160 ohm] [120
ohm] [96 ohm] [80 ohm] [68.6 ohm] [60 ohm] [53.3 ohm] [48 ohm] [43.6 ohm] [40 ohm]
[36.9 ohm] [34.3 ohm] [32 ohm] [30 ohm] [28.2 ohm] [26.7 ohm] [25.3 ohm]
Proc Data Drive Strength
Proc Data Drive Strength.
Configuration options: [Auto] [High Impedance] [120 ohm] [60 ohm] [40 ohm] [30 ohm]
Proc CA ODT impedance
Select the ODT impedance for ACHAN CA IOs.
Configuration options: [Auto] [30 ohm] [40 ohm] [60 ohm] [120 ohm] [Disabled]
Proc CK ODT impedance
Select the ODT impedance for ACHAN CK IOs.
Configuration options: [Auto] [30 ohm] [40 ohm] [60 ohm] [120 ohm] [Disabled]

                                                                                      27

     Proc DQ ODT impedance
     Select the ODT impedance for ACHAN DQ IOs.
     Configuration options: [Auto] [30 ohm] [40 ohm] [60 ohm] [120 ohm] [Disabled]
     Proc DQS ODT impedance
     Select the ODT impedance for ACHAN DQS IOs.
     Configuration options: [Auto] [30 ohm] [40 ohm] [60 ohm] [120 ohm] [Disabled]
     DRAM Data Drive Strength
     DRAM Data Drive Strength.
     Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
     Rtt Nom Wr
     Rtt Nom Wr.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4
     (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Rtt Nom Rd
     Rtt Nom Rd.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4
     (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Rtt Wr
     Rtt Wr.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4
     (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Rtt Park
     Rtt Park.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4
     (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Rtt Park Dqs
     Rtt Park Dqs.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4
     (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Power Down Enable
     Power Down Enable.
     Configuration options: [Disabled] [Enabled] [Auto]
     Memory Context Restore
     Configure the memory context restore mode. When enabled, DRAM re-retraining is
     avoided when possible and the POST latency is minimized.
     Configuration options: [Disabled] [Enabled] [Auto]
     UCLK DIV1 MODE
     Set UCLK DIV mode.
     Configuration options: [Auto] [UCLK=MEMCLK] [UCLK=MEMCLK/2]
     CA Tx Phase Shift Clk
     CA Tx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]
     CS Tx Phase Shift Clk
     CS Tx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]

28

     CK Tx Phase Shift Clk
     CK Tx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]
     CA Rx Phase Shift Clk
     CA Rx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]
     CS Rx Phase Shift Clk
     CS Rx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]
     CK Rx Phase Shift Clk
     CK Rx Phase Shift Clk.
     Configuration options: [Auto] [0] - [7]
     FIFO Wr En Fine Delay
     FIFO Wr En Fine Delay.
     Configuration options: [Auto] [0] [1]
     POC Sample PD
     POC Sample PD.
     Configuration options: [Auto] [Enabled] [Disabled]
     Bank Swap Mode
     Bank Swap Mode.
     Configuration options: [Auto] [Disabled] [Swap CPU] [Swap APU]
     Mem Over Clock Fail Count
     Mem Over Clock Fail Count.
Precision Boost Overdrive
     Prochot VRM Throttling
     Disabling Prochot will disable the VRMs ability to throttle the CPU when the voltage
     regulator is approaching its thermal limits.
     Configuration options: [Auto] [Disable] [Enable]
     Peak Current Control
     Enable or Disable PCC Feature. Only need to Disable during extreme overclocking.
     Configuration options: [Auto] [Disable] [Enable]
     Medium Load Boostit
     Enabling may help improve performance under medium loads.
     Configuration options: [Auto] [Disabled] [Enabled]
     Precision Boost Overdrive
     When this item is enabled, it allows the processor to run beyond defined values for
     PPT, VDD_CPU EDC, VDD_CPU TDC, VDD_SOC EDC, VDD_SOC TDC to the limits of
     the board, and allows it to boost at higher voltages for longer durations than default
     operation.
     Configuration options: [Auto] [Disabled] [Enabled] [Enhancement] [Manual] [AMD ECO
     Mode]

                                                                                              29

     NOTE: The following item appears only when Precision Boost Overdrive is set to [Enhancement].

     Thermal Limit
     Thermal Limit.
     Configuration options: [Level 1 (90°C)] [Level 2 (80°C)] [Level 3 (70°C)]

     NOTE: The following items appear only when Precision Boost Overdrive is set to [Manual].

     PPT Limit
     PPT Limit [W], Board Socket Power capability, adjustable up to motherboard
     programed PPT limit.
     TDC Limit
     TDC Limit [A], Board thermally constrained current delivery capability, adjustable up to
     motherboard programed board TDC limit.
     EDC Limit
     EDC Limit [A], Board electrically constrained current delivery capability, adjustable up
     to motherboard programed board EDC limit.

     NOTE: The following items appear only when Precision Boost Overdrive is set to [AMD ECO
     Mode].

     AMD ECO Mode
     Adjust the CPU control limits to manage performance. Performance may vary
     depending on the CPU cooler or other components.
     cTDP 65W (88W/75A/150A)
     cTDP 105W (142W/110A/170A)
     cTDP 170W (230W/160A/225A)
     Configuration options: [Auto] [cTDP 35W] [cTDP 65W] [cTDP 105W] [cTDP 170W]
     Precision Boost Overdrive Scalar
     [Auto]          Part runs with a scalar of 1X, i.e. normal operation.
     [Manual]          Part runs with a scalar of customized value.

     NOTE: The following item appears only when Precision Boost Overdrive Scalar is set to [Manual].

     Customized Precision Boost Overdrive Scalar
     Precision Boost Overdrive increases the maximum boost voltage used (runs above
     parts specified maximum) and the amount of time spent at that voltage. The larger
     the value entered the larger the boost voltage used and the longer that voltage will be
     maintained.
     Configuration options: [1X] - [10X]
     CPU Boost Clock Override
     Allows you to increase (positive) or decrease (negative) the maximum CPU frequency
     that may be automatically achieved by the CPU Boost Algorithm.
     Configuration options: [Auto] [Disabled] [Enabled (Positive)] [Enabled (Negative)]

30

NOTE: The following item appears only when CPU Boost Clock Override is set to [Enabled
(Positive)].

Max CPU Boost Clock Override(+)
Increases the maximum CPU frequency that may be automatically achieved by the
Precision Boost 2 algorithm.

NOTE: The following item appears only when CPU Boost Clock Override is set to [Enabled
(Negative)].

Max CPU Boost Clock Override(-)
Decreases the maximum CPU frequency that may be automatically achieved by the
Precision Boost 2 algorithm.
Per-Core Boost Clock Limit
         Per-Core Boost Clock Limit
         Set specific limits to each core in MHz unit. This will still be capped by the
         global CPU Boost clock but limiting down from this for each core will restrain
         it’s frequency.
         Limiting a weaker core may improve it’s curve optimizer margin.
         Configuration options: [Auto] [Disabled] [Enabled]

NOTE: The following items appear only when Per-Core Boost Clock Limit is set to [Enabled].

         Core 0~15
         The recommended value is based on parameters of your setup with the
         current settings of Ai Tweaker Menu.
Platform Thermal Throttle Limit
Allows the user to decrease the maximum allowed processor temperature (celsius).
Configuration options: [Manual] [Auto]

NOTE: The following items appear only when Per-Core Boost Clock Limit is set to [Manual].

Platform Thermal Throttle Limit
Allows the user to decrease the maximum allowed processor temperature (celsius).
Curve Optimizer
         Curve Optimizer
         Allows the user to shift the Voltage / Frequency (AVFS) curve to include higher
         voltages (positive values) or lower voltages (negative values). The larger the
         value entered the larger the magnitude of the voltage limit.
         Configuration options: [Auto] [All Cores] [Per Core]

NOTE: The following items appear only when Curve Optimizer is set to [All Cores].

         All Core Curve Optimizer Sign
         Determines the direction of the curve shift on all cores. Positive shifts the
         curve up to use higher voltages. Negative shifts the curve down to use lower
         voltages.
         Configuration options: [Positive] [Negative]

                                                                                             31

             All Core Curve Optimizer Magnitude
             Determines the magnitude of the curve shift to be made (entered in whole
             numbers) the larger the value entered the larger the magnitude of the shift.

     NOTE: The following items appear only when Curve Optimizer is set to [Per Core].

             Core 0-63 Curve Optimizer Sign
             Determines the direction of the curve shift on this core. Positive shifts the
             curve up to use higher voltages. Negative shifts the curve down to use lower
             voltages.
             Configuration options: [Positive] [Negative]
             Core 0-63 Curve Optimizer Magnitude
             Determines the magnitude of the curve shift to be made to this core (entered
             in whole numbers) the larger the value entered the larger the magnitude of the
             shift.
     GFX Curve Optimizer
             GFX Curve Optimizer
             Allows the user to shift the GFX Voltage / Frequency (AVFS) curve to include
             higher voltages (positive values) or lower voltages (negative values). The
             larger the value entered the larger the magnitude of the voltage shift.
             Configuration options: [Auto] [GFX Curve Optimizer]

     NOTE: The following items appear only when GFX Curve Optimizer is set to [GFX Curve Optimizer].

             GFX Curve Optimizer Sign
             Determines the direction of the curve shift for GFX. Positive shifts the curve
             up to use higher voltages. Negative shifts the curve down to use lower
             voltages.
             Configuration options: [Positive] [Negative]
             GFX Curve Optimizer Magnitude
             Determines the magnitude of the GFX curve shift to be made (entered in
             whole numbers) the larger the value entered the larger the magnitude of the
             shift. Field defaults to 0 and the user can enter whole integer numbers. Value
             entered, combined with the sign above, is used to send the SMU a GFX Curve
             Optimizer command.
     Curve Shaper
             Min Frequency - Low Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

32

NOTE: The following items appear only when Min Frequency - Low Temperature is set to [Enable].

        Min Frequency - Low Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Min Frequency - Low Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Min Frequency - Med Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

NOTE: The following items appear only when Min Frequency - Med Temperature is set to [Enable].

        Min Frequency - Med Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Min Frequency - Med Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Min Frequency - High Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

                                                                                                 33

     NOTE: The following items appear only when Min Frequency - High Temperature is set to [Enable].

             Min Frequency - High Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             Min Frequency - High Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             Low Frequency - Low Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

     NOTE: The following items appear only when Min Frequency - High Temperature is set to [Enable].

             Low Frequency - Low Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             Low Frequency - Low Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             Low Frequency - Med Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

34

NOTE: The following items appear only when Low Frequency - Med Temperature is set to [Enable].

        Low Frequency - Med Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Low Frequency - Med Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Low Frequency - High Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

NOTE: The following items appear only when Min Frequency - High Temperature is set to [Enable].

        Low Frequency - High Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Low Frequency - High Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Med Frequency - Low Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

                                                                                                  35

     NOTE: The following items appear only when Med Frequency - Low Temperature is set to [Enable].

             Med Frequency - Low Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             Med Frequency - Low Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             Med Frequency - Med Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

     NOTE: The following items appear only when Med Frequency - Med Temperature is set to
     [Enable].

             Med Frequency - Med Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             Med Frequency - Med Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             Med Frequency - High Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

36

NOTE: The following items appear only when Med Frequency - High Temperature is set to
[Enable].

        Med Frequency - High Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Med Frequency - High Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        High Frequency - Low Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

NOTE: The following items appear only when High Frequency - Low Temperature is set to [Enable].

        High Frequency - Low Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        High Frequency - Low Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        High Frequency - Med Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

                                                                                                  37

     NOTE: The following items appear only when High Frequency - Med Temperature is set to
     [Enable].

             High Frequency - Med Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             High Frequency - Med Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             High Frequency - High Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

     NOTE: The following items appear only when High Frequency - High Temperature is set to
     [Enable].

             High Frequency - High Temperature Sign
             Determines the direction of the shift. Positive shifts the curve up to use higher
             voltages. Negative shifts the curve down to use lower voltages.
             Configuration options: [Positive] [Negative]
             High Frequency - High Temperature Magnitude
             Determines the magnitude of the shift to be made (entered in whole numbers)
             the larger the value entered the larger the magnitude of the shift.
             Max Frequency - Low Temperature
             Curve Shaper is an advanced overclocking tuning suite utilizing the same
             ''Curve optimizer'' steps. It changes variable voltage across all cores for
             finite (overlapping) frequency and temperature regions. This can be used
             to more precisely tune the voltage required by your system. In general, Low
             temperature corresponds to idle temps, Med Temperature corresponds to 1T/
             Gaming Workloads, and high temperature is for stress tests. Additionally, Min
             and Low frequencies are idle/background tasks, Medium is high core count
             workloads, and high and Max frequency are for gaming and 1T workloads.
             These settings work as ''bands'' so you may find that for particular cases
             several settings impact the behavior. Ex, A workload running at 65 Celsius
             will likely be influenced by Low temp and Med temp values. Workloads lower
             than 65C will be more impacted by Low. Workloads above 65C will be more
             impacted by Medium.
             Configuration options: [Auto] [Enable] [Disable]

38

NOTE: The following items appear only when Max Frequency - Low Temperature is set to [Enable].

        Max Frequency - Low Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Max Frequency - Low Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Max Frequency - Med Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

NOTE: The following items appear only when Max Frequency - Med Temperature is set to [Enable].

        Max Frequency - Med Temperature Sign
        Determines the direction of the shift. Positive shifts the curve up to use higher
        voltages. Negative shifts the curve down to use lower voltages.
        Configuration options: [Positive] [Negative]
        Max Frequency - Med Temperature Magnitude
        Determines the magnitude of the shift to be made (entered in whole numbers)
        the larger the value entered the larger the magnitude of the shift.
        Max Frequency - High Temperature
        Curve Shaper is an advanced overclocking tuning suite utilizing the same
        ''Curve optimizer'' steps. It changes variable voltage across all cores for
        finite (overlapping) frequency and temperature regions. This can be used
        to more precisely tune the voltage required by your system. In general, Low
        temperature corresponds to idle temps, Med Temperature corresponds to 1T/
        Gaming Workloads, and high temperature is for stress tests. Additionally, Min
        and Low frequencies are idle/background tasks, Medium is high core count
        workloads, and high and Max frequency are for gaming and 1T workloads.
        These settings work as ''bands'' so you may find that for particular cases
        several settings impact the behavior. Ex, A workload running at 65 Celsius
        will likely be influenced by Low temp and Med temp values. Workloads lower
        than 65C will be more impacted by Low. Workloads above 65C will be more
        impacted by Medium.
        Configuration options: [Auto] [Enable] [Disable]

                                                                                                 39

         NOTE: The following items appear only when Max Frequency - High Temperature is set to
         [Enable].

                 Max Frequency - High Temperature Sign
                 Determines the direction of the shift. Positive shifts the curve up to use higher
                 voltages. Negative shifts the curve down to use lower voltages.
                 Configuration options: [Positive] [Negative]
                 Max Frequency - High Temperature Magnitude
                 Determines the magnitude of the shift to be made (entered in whole numbers)
                 the larger the value entered the larger the magnitude of the shift.
         CO Load Guard
         Enable to switch over to Safe Curve Optimizer value during periods of very heavy
         loading.
         Configuration options: [Auto] [Disable] [Enable]

         NOTE: The following items appear only when CO Load Guard is set to [Enable].

         All Core Safe CO Sign
         Configuration options: [Positive] [Negative]
     Digi+ VRM
         VRM Initialization Check
         When any error occurs during VRM initialization, the system will hang at POST code
         76/77 if this function is enabled.
         Configuration options: [Disabled] [Enabled]
         Voltage training
         Configuration options: [Auto] [Disabled] [Enabled]
         CPU Load-line Calibration
         CPU Load-Line Calibration is defined by AMD VRM spec and affects CPU voltage. The
         CPU working voltage will decrease proportionally to CPU loading. Higher value could
         get higher voltage and good overclocking performance but increase the CPU and VRM
         thermal.
         Configuration options [Auto] [Level 1] [Level 2] [Level 3] [Level 4] [Level
         5:Recommended for OC] [Level 6] [Level 7] [Level 8]

         CAUTION! DO NOT remove the thermal module. The thermal conditions should be monitored.

         CPU Current Capability
         A higher value brings a wider total power range and extends the overclocking
         frequency range simultaneously.
         Configuration options: [Auto] [100%] - [140%]

         NOTE: Configure higher values when overclocking or under a high loading for extra power support.

40

CPU VRM Switching Frequency
Sets the VRM switching frequency. VRM switching frequency affects transient
response and VRM component temperatures. Setting a higher switching frequency
will result in better transient response at the expense of higher VRM temperatures.
Active cooling of the VRM heatsink is recommended when running high CPU voltage
and high load-line calibration values.
Configuration options: [Auto] [Manual]

CAUTION! Do not remove the VRM heatsink.\

NOTE: The following item appears only when CPU VRM Switching Frequency is set to [Manual].

Fixed CPU VRM Switching Frequency(KHz)
Allows you to set a higher frequency for a quicker transient response speed. The
values range from 300 KHz to 800 KHz with an interval of 50 KHz.
CPU Power Duty Control
CPU power duty control adjusts the duty cycle of each VRM phase based upon current
and/or temperature.
[T. Probe]          Select to maintain VRM thermal balance
[Extreme]           Select to maintain VRM current balance.

CAUTION! DO NOT remove the thermal module when setting this item to [Extreme]. The thermal
conditions should be monitored.

CPU Power Phase Control
Allows you to set the power phase control of the CPU.
[Auto]           Automatically selects the power phase control.
[Standard]        The number of active phases is controlled by the CPU.
[Optimized]       Set to the ASUS optimized phase tuning profile.
[Extreme]         Sets full phase mode.
[Manual]          Manually select the power phase response speed.

CAUTION! DO NOT remove the thermal module when setting this item to [Extreme]. The thermal
conditions should be monitored.

NOTE: The following item appears only when CPU Power Phase Control is set to [Manual].

Power Phase Response
Select the ultra fast mode for a faster power phase response. The reaction time will be
longer when the regular mode is selected.
Configuration options: [Ultra Fast] [Fast] [Medium] [Regular]
VDDSOC Current Capability
Configuration options: [Auto] [100%] - [140%]
VDDSOC Switching Frequency
Configuration options: [Auto] [Manual]

                                                                                             41

           NOTE: The following item appears only when VDDSOC Switching Frequencyis set to [Manual].

           Fixed VDDSOC VRM Switching Frequency(KHz)
           The switching frequency will affect the VDDSOC transient response speed and the
           component thermal production. Configure a higher frequency for a quicker transient
           response speed. The values range from 300 KHz to 800 KHz with an interval of 100
           KHz.
           VDDSOC Power Duty Control
           VDDSOC Power Duty Control adjusts the current and thermal of every VRM phase
           component.
           [T. Probe]        Select to maintain VRM thermal balance
           [Extreme]         Select to maintain VRM current balance.

           CAUTION! DO NOT remove the thermal module when setting this item to [Extreme]. The thermal
           conditions should be monitored.

           VDDSOC Power Phase Control
           Configuration options: [Auto] [Standard] [Optimized] [Extreme] [Manual]

           CAUTION! DO NOT remove the thermal module when setting this item to [Extreme]. The thermal
           conditions should be monitored.

           NOTE: The following item appears only when VDDSOC Power Phase Control is set to [Manual].

           Power Phase Response
           Select ultra fast mode for a faster power phase response. The reaction time will be
           longer when regular mode is selected.
           Configuration options: [Ultra Fast] [Fast] [Medium] [Regular]
           MISC Switching Frequency
           Configuration options: [Auto] [Manual]

           NOTE: The following item appears only when MISC Switching Frequencyis set to [Manual].

           Fixed MISC Switching Frequency(KHz)
           The switching frequency will affect the MISC transient response speed and the
           component thermal production. Configure a higher frequency for a quicker transient
           response speed. The values range from 400 KHz to 700 KHz with an interval of 100
           KHz.
     Performance Bias
     Different Values may help different Software’s performance.
     Configuration options: [Auto] [None] [CB R23] [GB3]
     Tweaker’s Paradise
           Clock Spread Spectrum
           Allows you to enable or disable Clock Spread Spectrum.
           Configuration options: [Auto] [Enabled] [Disabled]

42

     Stretch mode for L3 DFLL
     Configuration options: [Auto] [Enabled] [Disabled]
     1.8V PLL Voltage
     Allows you to set the 1.8V PLL Voltage. Use the <+> or <-> to adjust the value. The
     values range from 1.500V to 2.500V with an interval of 0.010V.
     1.8V Standby Voltage
     Allows you to set the 1.8V Standby Voltage. Use the <+> or <-> to adjust the value. The
     values range from 1.500V to 2.500V with an interval of 0.010V.
     Misc_ALW
     Allows you to set the Misc_ALW Voltage. Use the <+> or <-> to adjust the value. The
     values range from 0.600V to 1.500V with an interval of 0.010V.
     Chipset0 VDD Voltage
     Allows you to set the Chipset0 VDD Voltage. Use the <+> or <-> to adjust the value.
     The values range from 0.800V to 1.400V with an interval of 0.005V.
     Chipset1 VDD Voltage
     Allows you to set the Chipset1 VDD Voltage. Use the <+> or <-> to adjust the value.
     The values range from 0.800V to 1.400V with an interval of 0.005V.
     CPU 3.3V
     Allows you to set the CPU 3.3V Voltage. Use the <+> or <-> to adjust the value. The
     values range from 2.800V to 4.000V with an interval of 0.020V.
     Sense MI Skew 4
     Configuration options: [Auto] [Disabled] [Enabled]
     Sense MI Skew 4
     Use the <+> or <-> to adjust the value. The values range from 0.000 to 2.800 with an
     interval of 0.00625V.
Core Flex
Customize your own algorithms to adjust boosting behavior for more optimized power
efficiency, temperatures and performance. Customize up to 3 concurrent algorithms.
     Load X3D Core Flex Gaming Preset
     Loads a preconfigured Algorithm for X3D Processors.
     Algorithm 1-3
     Set to Enabled to customize this Algorithm.
     Configuration options: [Auto] [Disabled] [Enabled]

     NOTE: The following items appear only when Algorithm 1-3 is set to [Enabled].

     Algorithm 1-3 Condition
     Select the condition to monitor for and take action upon. When multiple Algorithms
     watch for the same condition then the result is ‘AND’ and the smaller of the 2 Action
     Values get written.
     Configuration options: [Auto] [CPU Temperature] [Core Voltage] [Core Current]

                                                                                               43

          Algorithm 1-3 Action
          Select the Action to take when targeted condition crosses the threshold. When
          multiple Algorithms execute the same Actions then the result is ‘AND’ and the smaller
          of the 2 Action Values get written.
          Configuration options: [Auto] [Package Power Limit Fast] [Package Power Limit Slow]
          [Thermal Limit] [Vcore TDC Limit] [Vcore EDC Limit] [SOC TDC Limit] [SOC EDC Limit]
          [CCD Priority] [Mem On The Fly]
          Level1 Threshold Value
          Set the boundary separating Level1 Action Value and Level2 Action Value. When
          condition is below or equal to this value, then Level1 Action Value gets written. If
          above but below Level2 Threshold Value, then Level2 Action Value gets written.
          Temperature is in degrees Celsius, Voltage is in millivolts, and current is in Ampere.
          Level2 Threshold Value
          Set the boundary separating Level2 Action Value and Level3 Action Value. When
          condition is below or equal to this value and above Level1 Threshold Value, then
          Level2 Action Value gets written. If above, then Level3 Action Value gets written.
          Temperature is in degrees Celsius, Voltage is in millivolts, and current is in Ampere.
          Level1 Action Value
          Set the value for Action to take when condition lies below the first boundary. Power
          is in Watt, Temperature in degrees Celsius, current is in Ampere, BCLK is in MHz. CCD
          Priority Action Value refers to CCD number, 0 for CCD0, 1 for CCD1, any values higher
          than 1 will be capped to 1.
          Level2 Action Value
          Set the value for Action to take when condition lies between the first boundary and
          the second boundary. Power is in Watt, Temperature in degrees Celsius, current is in
          Ampere, BCLK is in MHz. CCD Priority Action Value refers to CCD number, 0 for CCD0,
          1 for CCD1, any values higher than 1 will be capped to 1.
          Level3 Action Value
          Set the value for Action to take when condition lies above the second boundary. Power
          is in Watt, Temperature in degrees Celsius, current is in Ampere, BCLK is in MHz. CCD
          Priority Action Value refers to CCD number, 0 for CCD0, 1 for CCD1, any values higher
          than 1 will be capped to 1.
          CCD Priority Memory Activity Threshold
          If Algo is set to CCD Priority, CCD Priority Switching will only occur if the Memory
          Activity is higher than the threshold specified. For no checks, just set this to 0.
          CCD Priority Hysteresis
          If Algo is set to CCD Priority, CCD Priority Switching will only occur if the Memory
          Activity is higher than the threshold specified. For no checks, just set this to 0.
     AI Features
          Processor Utilization
          Displays processor utilization information.

44

      Cooler Efficiency Customize
      [Keep Training]	Continuous evaluations will be performed on Cooler efficiency
                          and updated accordingly.
      [Stop Training]	Cooler efficiency evaluations will stop and current evaluated
                          efficiency will be used.
      [User Specify]	Manually specify the Cooler efficiency and all predictions will be
                          based off this manual setting.

      NOTE: The following item appears only when Cooler Efficiency Customize is set to [User Specify].

      Cooler Score
      The value of the Cooler’s pts. [Maximum] 250 pts; [Minimum] 67 pts; [Default] 125 pts.
      Recalibrate Cooler
      Allows you to recalibrate your cooler efficiency.
      Cooler Re-evaluation Algorithm
      Allows you to set how inclined the re-evaluation will update.
      Configuration options: [Normal] [More inclined to update] [Very inclined to update]
      [Less inclined to update] [Least inclined to update]
      Optimism Scale
      Allows you to set the optimism of the predictions. The higher the value, the more
      optimistic the predictions and vice versa.
Extreme Over-voltage
This item can only be enabled when the onboard CPU_OV jumper is switched on. Setting
this item to [Enabled] allows you to configure higher voltages for overclocking, but the CPU
lifetime will not be guaranteed.
Configuration options: [Disabled] [Enabled]
CPU SOC Voltage
Increase to help Memory Frequency overclock. The reading shown on the right is the SOC
Voltage Reading from the remote ADC Sensing. The reading shown below is the true SOC
Voltage sensed from the Processor's sensor.
Configuration options: [Auto] [Manual Mode]

      NOTE: The following item appears only when CPU SOC Voltage is set to [Manual Mode].

VDDSOC Voltage Override
Use the <+> and <-> keys to adjust the value. The values range from 0.625V to 1.300V with
an interval of 0.005V.
CPU VDDIO / MC Voltage
Use the <+> or <-> to adjust the value. The values range from 0.800V to 2.000V with an
interval of 0.010V.
Misc Voltage
Misc Voltage supplies power for the internal VDDG rails which power the GMI bus.
Configuration options: [Auto] [Manual Mode] [Offset Mode]

                                                                                                         45

           NOTE: The following items appear only when Misc Voltage is set to [Manual Mode].

     Misc Voltage Override
     Configure the input voltage for the Misc by the external voltage regulator.

           NOTE: The following items appear only when Misc Voltage is set to [Offset Mode].

     Offset Mode Sign
     [+]               To offset the Misc voltage by a positive value.
     [–]               To offset the Misc voltage by a negative value.
     Misc Voltage Offset
     Use the <+> or <-> to adjust the value. The values range from 0.0050V to 0.5000V with an
     interval of 0.0050V.
     VDDP Voltage
     Use the <+> or <-> to adjust the value. The values range from 0.700V to 1.800V with an
     interval of 0.001V.
     High DRAM Voltage Mode
     If disabled, the upper range for DRAM Voltage will be 1.435V. If enabled, the upper range will
     be 2.070V. If enabled on non-supported DRAM, the voltage will be lower than requested.
     Configuration options: [Auto] [Disabled] [Enabled]
     DRAM VDD Voltage
     Allows you to set the power for the DRAM IC’s VDD portion.
     DRAM VDDQ Voltage
     Allows you to set the power for the DRAM IC’s VDD Data portion.
     VDDG CCD Voltage
     VDDG CCD represents voltage for the data portion of the Infinity Fabric. Range is
     650mV~1650mV of stepping 10mV.
     Configuration options: [Auto] [650 mV] - [1650 mV]
     VDDG IOD Voltage
     VDDG IOD represents voltage for the data portion of the Infinity Fabric. Range is
     650mV~1650mV of Stepping 10mV.
     Configuration options: [Auto] [650 mV] - [1650 mV]
     Advanced Memory Voltages
           PMIC Force Continuous Current Mode
           Configuration options: [Auto] [Enabled] [Disabled]
           PMIC Voltages
           Configuration options: [Auto] [Sync All PMICs] [By per PMIC]

           NOTE: The following items appear only when PMIC Voltages is set to [Sync All PMICs].

           SPD HUB VLDO (1.8V)
           Allows you to set the main power for the SPD Hub Logic. Default set to 1.8V.

46

SPD HUB VDDIO (1.0V)
Allows you to set the main power for the SPD Hub side-band interface. Default set to
1.0V.
Memory VDD Voltage
Allows you to set the power for the DRAM IC’s VDD portion.
Memory VDDQ Voltage
Allows you to set the power for the DRAM IC’s Data portion.
Memory VPP Voltage
Allows you to set the power for the DRAM Activating Power Supply.
Memory Voltage Switching Frequency
Allows you to set the switching frequency of memory voltage regulator in MHz.
Memory Current Capability
Allows you to set the current capability for the Switching Regulators in Amps.

                                                                                       47

     6.           Advanced menu
     The Advanced menu items allow you to change the settings for the CPU and other system
     devices. Scroll down to display other BIOS items.

           CAUTION! Be cautious when changing the settings of the Advanced menu items. Incorrect field
           values can cause the system to malfunction.

## 6.1 Trusted Computing

     The items in this menu allow you to configure the Trusted Computing settings.

     Security Device Support
     Allows you to enable or disable the BIOS support for security device. O.S. will not show
     Security Device. TCG EFI protocol and INT1A interface will not be available.
     Configuration options: [Disable] [Enable]

           NOTE: The following items appear only when Security Device Support is set to [Enable].

     SHA-1 PCR Bank
     Enable or disable SHA-1 PCR Bank.
     Configuration options: [Disabled] [Enabled]
     SHA256 PCR Bank
     Enable or disable SHA256 PCR Bank.
     Configuration options: [Disabled] [Enabled]
     SHA512 PCR Bank
     Enable or disable SHA512 PCR Bank.
     Configuration options: [Disabled] [Enabled]

48

SM3_256 PCR Bank
Enable or disable SM3_256 PCR Bank.
Configuration options: [Disabled] [Enabled]
Pending operation
Schedule an Operation for the Security Device.
Configuration options: [None] [TPM Clear]

      NOTE: Your computer will reboot during restart in order to change the State of the Security Device.

Platform Hierarchy
Enable or Disable Platform Hierarchy.
Configuration options: [Disabled] [Enabled]
Storage Hierarchy
Enable or disable Storage Hierarchy.
Configuration options: [Disabled] [Enabled]
Endorsement Hierarchy
Enable or disable Endorsement Hierarchy.
Configuration options: [Disabled] [Enabled]
Physical Presence Spec Version
Allows you to select to Tell O.S. to support PPI Version 1.2 or 1.3.
Configuration options: [1.2] [1.3]

      NOTE: Some HCK tests might not support 1.3.

## 6.2 AMD fTPM configuration

The items in this menu show the AMD fTPM configuration options.

Firmware TPM switch
Allows you to enable or disable Firmware TPM.
[Enable Firmware TPM]       Enables platform Firmware TPM.
[Disable Firmware TPM]         Disables platform Firmware TPM.

      CAUTION! When [Disable Firmware TPM] is selected, fTPM will be disabled and all data saved on
      it will be lost.

Erase fTPM NV for factory reset
Allows you to enable or disable fTPM reset for newly installed CPUs.
[Disabled]	Keep previous fTPM records and continue system boot, fTPM will not be
                 enabled with the new CPU unless fTPM is reset (reinitialized). Swapping
                 back to the old CPU may allow you to recover TPM related keys and data.
[Enabled]	Reset fTPM, if you have Bitlocker or encryption-enabled system, the
           system will not boot without a recovery key.

                                                                                                            49

## 6.3 UEFI Variables Protection

     Password protection of Runtime Variables
     Control the NVRAM Runtime Variable protection through System Admin Password.
     Configuration options: [Enable] [Disable]

## 6.4 CPU Configuration

     The items in this menu show the CPU-related information that the BIOS automatically
     detects. Scroll down to display other BIOS items.

     PSS Support
     Allows you to enable or disable the generation of ACPI_PPC, and _PCT objects.
     Configuration options: [Disabled] [Enabled]
     NX Mode
     Allows you enable or disable No-execute page protection Function.
     Configuration options: [Disabled] [Enabled]
     SVM Mode
     Allows you enable or disable CPU Virtualization.
     Configuration options: [Disabled] [Enabled]

           IMPORTANT! The items in this menu may vary based on the CPU installed.

## 6.5 PCI Subsystem Settings

     The items in this menu allow you to configure PCI, PCI-X, and PCI Express settings.

     Above 4G Decoding
     Allows you to enable or disable 64bit capable Devices to be Decoded in Above 4G Address
     Space (Only if System supports 64 bit PCI Decoding).
     Configuration options: [Disabled] [Enabled]

           NOTE:
           • Only enabled under 64bit operating system.
           • The following item appears only when Above 4G Decoding is set to [Enabled].

     Re-Size BAR Support
     If the system has Resizable BAR capable PCIe Devices, this option enables or disables
     Resizable BAR Support (Only if System supports 64 bit PCI Decoding).
     Configuration options: [Disabled] [Enabled]

           NOTE: To enable Re-Size BAR Support for harnessing full GPU memory, please go to the Boot
           section and set CSM(Compatibility Support Module) to [Disabled].

50

SR-IOV Support
Allows you to enable or disable Single Root IO Virtualization Support if the system has SR-
IOV capable PCIe devices.
Configuration options: [Disabled] [Enabled]

## 6.6 USB Configuration

The items in this menu allow you to change the USB-related features.

         NOTE: The Mass Storage Devices item shows the auto-detected values. If no USB device is
         detected, the item shows None.

Legacy USB Support
[Enabled]            Enables the Legacy USB support.
[Disabled]           USB devices are available only for EFI applications.
[Auto]               Automatically disables the Legacy USB support if USB devices are not
                     connected.

XHCI Hand-off
This is a workaround for OSes without XHCI hand-off support. The XHCI ownership change
should be claimed by XHCI driver.
[Disabled]        Support XHCI by XHCI drivers for operating systems with XHCI support.
[Enabled]            Support XHCI by BIOS for operating systems without XHCI support.

USB Mass Storage Driver Support
Allows you to enable or disable USB Mass Storage Driver Support
Configuration options: [Disabled] [Enabled]
Mass Storage Devices:
Allows you to select the mass storage device emulation type for devices connected. [Auto]
enumerates devices according to their media format. Optical drives are emulated as [CD-
ROM], drives with no media will be emulated according to a drive type.
Configuration options: [Auto] [Floppy] [Forced FDD] [Hard Disk] [CD-ROM]
USB Single Port Control
Allows you to enable or disable the individual USB ports.

         NOTE: Refer to section Motherboard layout and Rear I/O connection in your motherboard’s user
         guide for the location of the USB ports.

## 6.7 Network Stack Configuration

The items in this menu allow you to change the Network Stack Configuration.

Network stack
Allows you to disable or enable the UEFI network stack.
Configuration options: [Disabled] [Enabled]

                                                                                                        51

            NOTE: The following items appear only when Network Stack is set to [Enabled].

     Ipv4/Ipv6 PXE Support
     Allows you to enable or disable the Ipv4/Ipv6 PXE boot support.
     Configuration options: [Disabled] [Enabled]

## 6.8 NVMe Configuration

     This menu displays the NVMe controller and Drive information of the connected devices.
     You may press <Enter> on a connected NVMe device which appears in this menu to view
     more information on the NVMe device.

            NOTE: The options displayed in this menu may vary depending on the devices connected to your
            motherboard. Please refer to the BIOS of your motherboard for the actual settings and options.

## 6.9 HDD/SSD SMART Information

     The items in this menu allow you to view the SMART information for connected storage
     devices.

            NOTE:
            • The options displayed in this menu may vary depending on the devices connected to your
              motherboard. Please refer to the BIOS of your motherboard for the actual settings and options.
            • NVM Express devices do not support SMART information.

## 6.10 SATA Configuration

     While entering Setup, the BIOS automatically detects the presence of SATA devices. The
     SATA Port items show Empty if no SATA device is installed to the corresponding SATA port.
     Scroll down to display the other BIOS items.

            NOTE: The settings and options of this menu may vary depending on your motherboard. Please
            refer to the BIOS of your motherboard for the actual settings and options.

     SATA Controller(s)
     Allows you to enable or disable the SATA Device.
     Configuration options: [Disabled] [Enabled]

52

       NOTE: The following items appear only when SATA Controller(s) is set to [Enabled].

SATA Mode
This item allows you to set the SATA configuration.
 [AHCI]            Set to [AHCI] when you want the SATA hard disk drives to use the AHCI
                   (Advanced Host Controller Interface). The AHCI allows the onboard
                   storage driver to enable advanced Serial ATA features that increases
                   storage performance on random workloads by allowing the drive to
                   internally optimize the order of commands.
 [RAID]            Set to [RAID] when you want to create a RAID configuration from the
                   SATA hard disk drives.
NVMe RAID Mode
This item allows you to enable or disable the NVMe RAID mode.
Configuration options: [Disabled] [Enabled]
SATA6G
Allows you to enable or disable the selected SATA port.
Configuration options: [Disabled] [Enabled]
SATA6G Hot Plug
Designates this port as Hot Pluggable.
Configuration options: [Disabled] [Enabled]

## 6.11 APM Configuration

The items in this menu allow you to change the advanced power management settings.

Restore AC Power Loss
Select AC power state when power is re-applied after a power failure.
Configuration options: [Power Off] [Power On] [Last State]
ErP Ready
Allow BIOS to switch off some power at S4/S5 to get the system ready for ErP requirement.
When set to Enabled, all other PME options will be switched off. RGB LEDs and RGB/
Addressable RGB Headers will also be disabled.
Configuration options: [Disabled] [Enabled (S4+S5)] [Enabled (S5)]
Max Power Saving
Configuration options: [Disabled] [Enabled]
Power On By PCI-E
Enable or disable the wake-on-LAN function of the onboard LAN controller or other installed
PCI-E LAN cards.
Configuration options: [Disabled] [Enabled]
Power On By RTC
Enable or disable the RTC (Real-Time Clock) to generate a wake event and configure the RTC
alarm date. When enabled, you can set the days, hours, minutes, or seconds to schedule an
RTC alarm date.
Configuration options: [Disabled] [Enabled]

                                                                                              53

## 6.12 Onboard Devices Configuration

     The items in this menu allow you to change the onboard devices settings. Scroll down to
     view the other BIOS items.

              NOTE: The settings and options of this menu may vary depending on your motherboard. Please
              refer to the BIOS of your motherboard for the actual settings and options.

     Native ASPM
     [Auto]               Default setting
     [Enabled]            OS Controlled ASPM
     [Disabled]           BIOS Controlled ASPM

     CPU PCIE ASPM Mode Control
     Configuration options: [Disabled] [L0s Entry] [L1 Entry] [L0s And L1 Entry] [Auto]

     PCIEX16_1 Bandwidth Bifurcation Configuration
     [Auto Mode]:		Automatically switch PCIEX16_1 to x8 based on PCIEX16_2
                    usage.
     [PCIE RAID Mode]:               Detect up to 4 SSDs on Hyper M.2 X16 series card.
     [GPU with M.2 Storage]:         Support x8 graphics card and x4 NVMe M.2 SSD on PCIEX16_1.

              NOTE: Use [PCIE RAID Mode] when installing the Hyper M.2 X16 series card or other M.2 adapter
              cards. Installing other devices may result in a boot-up failure. The number of SSDs supported
              varies with the PCIe bifurcation abilities enabled by each processor.

     PCIEX16_2 Bandwidth Bifurcation Configuration
     [Auto Mode]:		Auto detect and switch.
                    If PCIE device is inserted to M.2_2, switch PCIEX16_2 to x4.
                    If no device is inserted to M.2_2, switch PCIEX16_2 to x8.
     [PCIE RAID Mode]:               Up to 2 SSDs installed onto the Hyper M.2 card can be detected.

              NOTE: Use [PCIE RAID Mode] when installing the Hyper M.2 X16 series card or other M.2 adapter
              cards. Installing other devices may result in a boot-up failure. The number of SSDs supported
              varies with the PCIe bifurcation abilities enabled by each processor.

     HD Audio Controller
     Enable/Disable Azalia HD Audio.
     Configuration options: [Disabled] [Enabled]
     Intel LAN Controller
     Allows you to enable or disable Intel LAN Controller.
     Configuration options: [Disabled] [Enabled]
     10G LAN Card
     Allows you to enable or disable the 10G LAN card.
     Configuration options: [Disabled] [Enabled]

54

Wi-Fi Controller
Allows you to enable or disable Wi-Fi Controller.
Configuration options: [Disabled] [Enabled]
Bluetooth Controller
Allows you to enable or disable Bluetooth Controller.
Configuration options: [Disabled] [Enabled]
LED lighting
When system is in working state
Allows you to turn the RGB LED lighting on or off when the system is in the working state.
[All On]          RGB LEDs and Functional will be behave normally.
[Stealth Mode] All LEDs will be disabled.
[Aura Only]       RGB LEDs will light up, while all functional LEDs will be disabled.
[Aura Off]        Functional LEDs behave normally, while RGB LEDs will be disabled.

      NOTE: The RGB Header(s) and Addressable Header(s) will only work under the S0 (working) state.

Windows Dynamic Lighting
Windows Dynamic Lighting allows users to control RGB devices through Windows Settings.
Configuration options: [Disabled] [Enabled]

      NOTE:
      • Compatibility is limited to Windows 11 OS builds 22621.2361 and later, ensure to verify your
        system's compatibility before activating it.
      • The aura effect may be limited due to technical constraints when Windows Dynamic Lighting is
        enabled.

When system is in sleep, hibernate or soft off states
Allows you to turn the RGB LED lighting on or off when the system is in the sleep, hibernate
or soft off states.
[All On]            RGB LEDs and Functional will be behave normally.
[Stealth Mode] All LEDs will be disabled.
[Aura Only]         RGB LEDs will light up, while all functional LEDs will be disabled.
[Aura Off]          Functional LEDs behave normally, while RGB LEDs will be disabled.

      NOTE: The RGB Header(s) and Addressable Header(s) will only work under the S0 (working) state.

USB power delivery in Soft Off state (S5)
Allows you to enable or disable USB power when your PC is in the S5 state.
Configuration options: [Disabled] [Enabled]
Serial Port Configuration
This submenu allows you to set parameters for Serial Port.

      NOTE: This item will only function if there is a serial port (COM) connector on your motherboard.

                                                                                                          55

            Serial Port
            Allows you to enable or disable the Serial port.
            Configuration options: [Enabled] [Disabled]

            NOTE: The following item appears only when Serial Port is set to [Enabled].

            Change settings
            Allows you to select an optimal setting for super IO device.
            Configuration options: [IO=3F8h; IRQ=4] [IO=2F8h; IRQ=3] [IO=3E8h; IRQ=4] [IO=2E8h;
            IRQ=3]
     PCIE Link Speed
     This submenu allows you to set parameters for PCIE Link Speed.
            PCIEX16 Link Mode
            Allows you to set the link speed for PCIEX16 Slot.
            Configuration options: [Auto] [GEN 1] [GEN 2] [GEN 3] [GEN 4] [GEN 5]
            M.2 Link Mode
            Allows you to set the link speed for M.2 Device.
            Configuration options: [Auto] [GEN 1] [GEN 2] [GEN 3] [GEN 4] [GEN 5]
            Chipset Link Mode
            Allows you to set the link speed between CPU and Chipset.
            Configuration options: [Auto] [GEN 1] [GEN 2] [GEN 3] [GEN 4]
            PCIEX16(G4) Link Mode
            Allows you to set the link speed for PCIEX16 Slot.
            Configuration options: [Auto] [GEN 1] [GEN 2] [GEN 3] [GEN 4]

## 6.13 NB Configuration

     The items in this menu allow you to change the NB Configurations.

     Primary Video Device
     Allows you to select Primary Video Device BIOS will use for output.
     Configuration options: [IGFX Video] [PCIE Video]
     Integrated Graphics
     Enable Integrate Graphics Controller.
     Configuration options: [Disabled] [Force] [Auto]
     UMA Frame Buffer Size
     Allows you to set the UMA FB Size.
     Configuration options: [Auto] [64M] [80M] [96M] [128M] [256M] [384M] [512M] [768M] [1G]
     [2G] [3G] [4G] [8G] [16G]

56

## 6.14 AMD CBS

The items in this menu shows the AMD Common BIOS Specifications.

       NOTE: The configuration options for this section vary depending on the motherboard. Please refer
       to the BIOS of your motherboard for the actual settings and options.

Global C-state Control
Allows you to control IO based C-state generation and DF C-states.
Configuration options: [Disabled] [Enabled] [Auto]
IOMMU
Allows you to enable or disable IOMMU.
Configuration options: [Disabled] [Enabled] [Auto]
ECC
Allows you to enable or disable ECC. Setting this item to [Auto] will set ECC to enable.
Configuration options: [Disabled] [Enabled] [Auto]
SMT Control
Can be used to disable symmetric multithreading. To re-enable SMT, a POWER CYCLE is
needed after setting this item to [Auto].
Configuration options: [Disable] [Auto]
Core Performance Boost
Allows you to disable Core Performance Boost.
Configuration options: [Disabled] [Auto]
CPU Common Options
       Thread Enablement
       Performance
       Prefetcher settings
               L1 Stream HW Prefetcher
               Allows you to enable or disable L1 Stream HW Prefetcher.
               Configuration options: [Disable] [Enable] [Auto]
               L2 Stream HW Prefetcher
               Allows you to enable or disable L2 Stream HW Prefetcher.
               Configuration options: [Disable] [Enable] [Auto]
               L1 Stride Prefetcher
               Uses memory access history of individual instructions to fetch additional lines
               when each access is a constant distance from the previous.
               Configuration options: [Disable] [Enable] [Auto]
               L1 Region Prefetcher
               Uses memory access history to fetch additional lines when the data access
               for a given instruction tends to be followed by other data accesses.
               Configuration options: [Disable] [Enable] [Auto]
               L1 Burst Prefetch Mode
               Allows you to enable or disable L1 Burst Prefetch Mode.
               Configuration options: [Disable] [Enable] [Auto]

                                                                                                          57

             L2 Up/Down Prefetcher
             Uses memory access history to determine whether to fetch the next or
             previous line for all memory accesses.
             Configuration options: [Disable] [Enable] [Auto]
     Core Watchdog
             Core Watchdog Timer Enable
             Allows you to enable or disable CPU Watchdog Timer.
             Configuration options: [Disabled] [Enabled] [Auto]

     NOTE: The following items appear only when Core Watchdog Timer Enable is set to [Enabled].

             Core Watchdog Timer Interval
             Allows you to select CPU Watchdog Timer interval.
             Configuration options: [Auto] [39.68us] [80.64us] [162.56us] [326.4us]
             [654.08us] [1.309ms] [2.620ms] [5.241ms] [10.484ms] [20.970ms] [40.64ms]
             [82.53ms] [166.37ms] [334.05ms] [669.41ms] [1.340s] [2.681s] [5.364s]
             [10.730s] [21.461s]
             Core Watchdog Timer Severity
             Allows you to specify the CPU Watchdog Time severity
             (MSRC001_0074[CpuWdTmrCfgSeverity]).
             Configuration options: [No Error] [Transparent] [Corrected] [Deferred]
             [Uncorrected] [Fatal] [Auto]
     RedirectForReturnDis
     From a workaround for GCC/C000005 issue for XV Core on CZ A0, setting
     MSRC001_1029 Decode Configuration (DE_CFG) bit 14 [DecfgNoRdrctForReturns] to
     1.
     Configuration options: [1] [0] [Auto]
     Power Supply Idle Control
     Configuration options: [Low Current Idle] [Typical Current Idle] [Auto]
     Opcache Control
     Allows you to enable or disable the Opcache.
     Configuration options: [Disabled] [Enabled] [Auto]
     Streaming Stores Control
     Allows you to enable or disable the Streaming Stores functionality.
     Configuration options: [Disabled] [Enabled] [Auto]
     Local APIC MOde
     Allows you to select local APIC operation modes.
     Configuration options: [Compatibility] [xAPIC] [x2APIC] [Auto]
     ACPI _CST C1 Declaration
     Determines whether or not to declare the C1 state to the OS.
     Configuration options: [Disabled] [Enabled] [Auto]
     Platform First Error Handling
     Allows you to enable or disable PFEH, cloack individual banks, and mask deferred
     error interrupts from each bank.
     Configuration options: [Enabled] [Disabled] [Auto]

58

MCA error thresh enable
Allows you to enable MCA error thresholding.
Configuration options: [False] [True] [Auto]

NOTE: The following item appears only when MCA error thresh enable is set to [True].

MCA error thresh count
Effective error threshold count = 4095(0xFFF) - <this value> (e.g. the default value of
0xFF5 results in a threshold of 10)
MCA FruText
Allows you to enable MCA FruText.
Configuration options: [False] [True]
SMU and PSP Debug Mode
When this item is set to [Enabled], uncorrected errors detected by the PSP FW or SMU
FW that should cause a cold reset, will hang and not restart the system.
Configuration options: [Disabled] [Enabled] [Auto]
PPIN Opt-in
Allows you to turn on PPIN feature.
Configuration options: [Disabled] [Enabled] [Auto]
REP-MOV/STOS Streaming
Allow REP-MOV/STOS to use non-caching streaming store for large sizes.
Configuration options: [Disabled] [Enabled]
Enhanced REP MOVSB/STOSB
This item is set to 1 by default, but can be set to zero for analysis purposes as long as
OS supports it.
Configuration options: [Disabled] [Enabled]
Fast Short REP MOVSB (FSRM)
This item is set to 1 by default, but can be set to zero for analysis purposes as long as
OS supports it.
Configuration options: [Disabled] [Enabled]
SNP Memory (RMP Table) Coverage
When this item is set to [Enabled], the ENTIE system memory is covered.
Configuration options: [Disabled] [Enabled] [Custom] [Auto]

NOTE: The following item appears only when SNP Memory (RMP Table) Coverage is set to
[Custom].

Amount of Memory to Cover
Specify MB of System Memory to be covered in Hex.
SMEE
Control secure memory enryption enable.
Configuration options: [Disable] [Enable] [Auto]
Action on BIST Failure
Allows you to set the action to take when a CCD BIST failure is detected.
Configuration options: [Do nothing] [Down-CCD] [Auto]

                                                                                            59

         Log Transparent Errors
         Log transparent errors in MCA in addition to debug registers.
         Configuration options: [Disabled] [Enabled] [Auto]
         AVX512
         Configuration options: [Disabled] [Enabled] [Auto]
         MONITOR and MWAIT Disable
         When this option is enabled, MONITOR, MWAIT, MONITORX, and MWAITX opcodes
         become invalid.
         Configuration options: [Disabled] [Enabled] [Auto]
         Corrector Branch Predictor
         Enabling for branch heavy codes may reduce conditional branch mispredicts.
         Configuration options: [Disabled] [Enabled]
         PAUSE Delay
         Number of cycles thread will be idle after a PAUSE instruction.
         Configuration options: [Auto] [Disabled] [16 cycles] [32 cycles] [64 cycles] [128 cycles]
         CPU Speculative Store Modes
         [Balanced]		Store instructions may delay sending out their
                                     invalidations to remote cacheline copies when the
                                     cacheline is present but not in a writable state in the
                                     local cache.
         [More Speculative]	Store instructions will send out invalidations to
                             remote cacheline copies as soon as possible.
         [Less Speculative]	Store instructions may delay sending out their
                             invalidations to remote cacheline copies when the
                             cacheline is not present in the local cache or not in a
                             writable state in the local cache.
         [Auto]		                           Default setting is applied.
         SVM Lock
         Allows you to enable or disable VM_CR[Lock].
         Configuration options: [Enabled] [Disabled] [Auto]
         SVM Enable
         Allows you to enable or disable VM_CR[SvmeDisable].
         Configuration options: [Enabled] [Disabled] [Auto]
     DF Common Options
         Memory Addressing
                 Memory interleaving
                 Allows for disabling memory channel interleaving.
                 Configuration options: [Disabled] [Enabled] [Auto]
                 Memory interleaving size
                 Controls the memory interleaving size. The valid values are AUTO, 256 bytes,
                 512 bytes, 1 Kbytes, or 2 Kbytes. This determines the starting address of the
                 interleave (bit 8, 9, 10 or 11).
                 Configuration options: [256 Bytes] [512 Bytes] [1KB] [2KB] [Auto]

60

            DRAM map inversion
            Inverting the map will cause the highest memory channels to get assigned the
            lowest addresses in the system.
            Configuration options: [Disable] [Enable] [Auto]
            Location of private memory regions
            Controls whether or not the private memory regions (PSP, SMU and CC6) are
            at the top of DRAM pair or distributed. Note that distributed requires memory
            on all dies. Note that it will always be at the top of DRAM if some dies don’t
            have memory regardless of this option’s setting.
            Configuration options: [Distributed] [Consolidated] [Consolidated to 1st DRAM
            pair] [Auto]
    ACPI
            ACPI SRAT L3 Cache as NUMA Domain
            [Disabled]    Memory Addressing \ NUMA nodes per socket will be
            declared.
            [Enabled]	Each CCX in the system will be declared as a separate NUMA
                          domain.
            [Auto]		      Sets to the default option.
    Disable DF to external downstream IP Sync Flood Propagation
    Disables Error propagation to UMC or any downstream slaves eg. FCH. Use this to
    avoid reset in failure scenario.
    Configuration options: [Sync flood disabled] [Sync flood enabled] [Auto]
    Disable DF sync flood propagation
    Disables propagation from PIE to other DF components and eventually to SDP ports.
    Configuration options: [Sync flood disabled] [Sync flood enabled] [Auto]
    Freeze DF module queues on error
    This item allows you to enable or disable freezing of all DF queues on error and also
    forces a sync flood on HWA even if MCAs are disabled.
    Configuration options: [Disabled] [Enabled] [Auto]
    DF Cstates
    When DF Cstate feature is set to [Enabled], FW programs the registers required
    to enable this feature is the DF HW. (For [Auto] option, it means this option will
    synchronize with Global C State).
    Configuration options: [Disabled] [Enabled] [Auto]
    PSP error injection support
    Configuration options: [False] [True]
UMC Common Options
    DDR Options
            DDR Timing Configuration

    CAUTION! Damage caused by use of your AMD processor outside of specification or in excess of
    factory settings are not covered by your system manufacturers warranty.

                                                                                                   61

     NOTE: The following items appear only when [Accept] is selected for DRAM Timing Configuration.

                        Active Memory Timing Settings
                        Configuration options: [Auto] [Enabled]

     NOTE: The following items appear only when [Enabled] is selected for Active Memory Timing
     Settings.

                        Memory Target Speed
                        Specifies the memory target speed in MT/s. The valid input is 2000
                        MT/s, 2400 MT/s, and range of 3200 MT/s ~ 12000 MT/s (stepping
                        of 200 MT/s). The value is in decimal. The user input value will be
                        rounded down to align with the stepping of 200 MT/s. The maximum
                        speed defined in the JEDEC spec is 8400 MT/s, any input value that
                        is greater than 8400 MT/s will be limited to 8400 MT/s.
                        DDR SPD Timing
                                 Tcl Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Tcl Ctrl is set to [Manual].

                          Tcl
                        	Specifies the CAS Latency. Valid values: 0x16 ~ 0x40, with a
                          stepping of 2. The value is in hex.
                                 Trcd Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trcd Ctrl is set to [Manual].

                          Trcd
                        	Specifies the RAS# Active to CAS# Read Delay Time. Valid
                          values: 0x8 ~ 0x3E with a stepping of 2. The value is in hex.
                                 Trp Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trp Ctrl is set to [Manual].

                          Trp
                        	Specifies Row Precharge Delay Time. Valid values: 0x8 ~
                          0x3E with a stepping of 2. The value is in hex.
                                 Tras Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

62

NOTE: The following item appears only when Tras Ctrl is set to [Manual].

                     Tras
                   	Specifies Active to Precharge Delay Time. Valid values: 0x1E
                     ~ 0x7E with a stepping of 2.
                            Trc Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when Trc Ctrl is set to [Manual].

                     Trc
                   	Specifies Active to Active/Refresh Delay Time. Valid values:
                     0x20 ~ 0xFF. The value is in hex.
                            Twr Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when Twr Ctrl is set to [Manual].

                     Twr
                   	Specifies the Minimum Write Recovery Time. Valid values:
                     0x30 ~ 0x60. The value is in hex.
                            Trfc1 Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when Trfc1 Ctrl is set to [Manual].

                     Trfc1
                   	Specifies the Refresh Recovery Delay Time (tRFC1). Valid
                     values: 0x32 ~ 0xFFF. The value is in hex.
                            Trfc2 Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when Trfc2 Ctrl is set to [Manual].

                     Trfc2
                   	Specifies the Refresh Recovery Delay Time (tRFC2). Valid
                     values: 0x32 ~ 0xFFF. The value is in hex.
                            TrfcSb Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

                                                                                    63

     NOTE: The following item appears only when TrfcSb Ctrl is set to [Manual].

                          TrfcSb
                        	Specifies the Refresh Recovery Delay Time (tRFCSB). Valid
                          values: 0x32 ~ 0x7FF. The value is in hex.
                        DDR Non-SPD Timing
                                 Trtp Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trtp Ctrl is set to [Manual].

                          Trtp
                        	Specifies the Read CAS# to Precharge command delay time.
                          Valid values: 0x5 ~ 0x1F. The value is in hex.
                                 TrrdL Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when TrrdL Ctrl is set to [Manual].

                          TrrdL
                        	Specifies the Activate to Activate Delay Time, same bank
                          group (tRRD_L). Valid values: 0x4 ~ 0x20. The value is in hex.
                                 TrrdS Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when TrrdS Ctrl is set to [Manual].

                          TrrdS
                        	Specifies the Activate to Activate Delay Time, different bank
                          group (tRRD_S). Valid values: 0x4 ~ 0x14. The value is in hex.
                                 Tfaw Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Tfaw Ctrl is set to [Manual].

                          Tfaw
                        	Specifies the Four Activate Window Time. Valid values: 0x14
                          ~ 0x50. The value is in hex.
                                 TwtrL Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

64

NOTE: The following item appears only when TwtrL Ctrl is set to [Manual].

                     TwtrL
                   	Specifies the Minimum Write to Read Time, the same bank
                     group. Valid values: 0x8 ~ 0x30. The value is in hex.
                            TwtrS Ctrl
                            [Auto]         Follow default setting.
                            [Manual]       Manually specify.

NOTE: The following item appears only when TwtrS Ctrl is set to [Manual].

                     TwtrS
                   	Specifies the Minimum Write to Read Time, different bank
                     group. Valid values: 0x2 ~ 0x10. The value is in hex.
                            TrdrdScL Ctrl
                            [Auto]        Follow default setting.
                            [Manual]      Manually specify.

NOTE: The following item appears only when TrdrdScL Ctrl is set to [Manual].

                     TrdrdScL
                   	Specifies the CAS to CAS delay time, same bank group. Valid
                     values: 0x1 ~ 0xF. The value is in hex.
                            TrdrdSc Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

NOTE: The following item appears only when TrdrdSc Ctrl is set to [Manual].

                     TrdrdSc
                   	Specifies the Read to Read turnaround timing in the same
                     chipselect. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TrdrdSd Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

NOTE: The following item appears only when TrdrdSd Ctrl is set to [Manual].

                     TrdrdSd
                   	Specifies the Read to Read turnaround timing in the same
                     DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TrdrdDd Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

                                                                                   65

     NOTE: The following item appears only when TrdrdDd Ctrl is set to [Manual].

                         TrdrdDd
                       	Specifies the Read to Read turnaround timing in a different
                         DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                                TwrwrScL Ctrl
                                [Auto]      Follow default setting.
                                [Manual]    Manually specify.

     NOTE: The following item appears only when TwrwrScL Ctrl is set to [Manual].

                         TwrwrScL
                       	Specifies the CAS to CAS Delay Time, same bank group. Valid
                         values: 0x1 ~ 0x3F. The value is in hex.
                                TwrwrSc Ctrl
                                [Auto]       Follow default setting.
                                [Manual]     Manually specify.

     NOTE: The following item appears only when TwrwrSc Ctrl is set to [Manual].

                         TwrwrSc
                       	Specifies the Write to Write turnaround timing in the same
                         chipselect. Valid values: 0x1 ~ 0xF. The value is in hex.
                                TwrwrSd Ctrl
                                [Auto]       Follow default setting.
                                [Manual]     Manually specify.

     NOTE: The following item appears only when TwrwrSd Ctrl is set to [Manual].

                         TwrwrSd
                       	Specifies the Write to Write turnaround timing in the same
                         DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                                TwrwrDd Ctrl
                                [Auto]       Follow default setting.
                                [Manual]     Manually specify.

     NOTE: The following item appears only when TwrwrDd Ctrl is set to [Manual].

                         TwrwrDd
                       	Specifies the Write to Write turnaround timing in a different
                         DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                                Twrrd Ctrl
                                [Auto]          Follow default setting.
                                [Manual]        Manually specify.

66

NOTE: The following item appears only when Twrrd Ctrl is set to [Manual].

                     Twrrd
                   	Specifies the Write to Read turnaround timing. Valid values:
                     0x1 ~ 0xF. The value is in hex.
                            Trdwr Ctrl
                            [Auto]         Follow default setting.
                            [Manual]       Manually specify.

NOTE: The following item appears only when Trdwr Ctrl is set to [Manual].

                     Trdwr
                   	Specifies the Read to Write turnaround timing. Valid values:
                     0x1 ~ 0x1F. The value is in hex.
         DDR BUS Configuration
                   Processor CK drive strengths
                   Specifies the Processor CK drive strengths.
                   Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                   [30.0 Ohm]
                   Processor CA drive strengths
                   Specifies the Processor CA drive strengths.
                   Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                   [30.0 Ohm]
                   Processor CS drive strengths
                   Specifies the Processor CS drive strengths.
                   Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                   [30.0 Ohm]
                   CA ODT GroupA
                   Specifies the CA ODT.
                   Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
                   [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
                   (40)]
                   CK ODT GroupA
                   Specifies the CK ODT.
                   Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
                   [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
                   (40)]
                   CS ODT GroupA
                   Specifies the CS ODT.
                   Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
                   [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
                   (40)]
                   CA ODT GroupB
                   Specifies the CS ODT.
                   Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
                   [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
                   (40)]

                                                                                        67

     CK ODT GroupB
     Specifies the CK ODT.
     Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
     [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
     (40)]
     CS ODT GroupB
     Specifies the CS ODT.
     Configuration options: [Auto] [RTT_OFF (Disable)] [RZQ/0.5 (480)]
     [RZQ/1 (240)] [RZQ/2 (120)] [RZQ/3 (80)] [RZQ/4 (60)] [RFU] [RZQ/6
     (40)]
     Processor ODT impedance Pull Up P0-3
     Specifies the Processor ODT impedance Pull Up P0.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm]
     [160 ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm]
     [48 ohm] [43 ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28
     ohm] [26 ohm] [25 ohm]
     Processor ODT impedance Pull Down P0-3
     Specifies the Processor ODT impedance Pull Down P0.
     Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm]
     [160 ohm] [120 ohm] [96 ohm] [80 ohm] [68 ohm] [60 ohm] [53 ohm]
     [48 ohm] [43 ohm] [40 ohm] [36 ohm] [34 ohm] [32 ohm] [30 ohm] [28
     ohm] [26 ohm] [25 ohm]
     Processor DQ drive strengths Pull Up P0-3
     Specifies the Processor DQ drive strengths Pull Up P0.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm]
     [80 ohm] [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Processor DQ drive strengths Pull Down P0-3
     Specifies the Processor DQ drive strengths Pull Down P0.
     Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm]
     [80 ohm] [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
     Dram ODT Impedance RTT_NOM_WR P0-3
     Specifies the Dram ODT Impedance RTT_NOM_WR P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
     [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT Impedance RTT_NOM_RD P0-3
     Specifies the Dram ODT Impedance RTT_NOM_RD P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
     [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT Impedance RTT_WR P0-3
     Specifies the Dram ODT Impedance RTT_WR P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
     [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT Impedance RTT_PARK P0-3
     Specifies the Dram ODT Impedance RTT_PARK P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
     [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
     Dram ODT Impedance DQS_RTT_PARK P0-3
     Specifies the Dram ODT Impedance DQS_RTT_PARK P0.
     Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
     [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]

68

        DRAM DQ drive strengths Pull Up P0-3
        Specifies the DRAM DQ drive strengths Pull Up P0.
        Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
        DRAM DQ drive strengths Pull Down P0-3
        Specifies the DRAM DQ drive strengths Pull Up P0.
        Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]
DDR Controller Configuration
        DDR Power Options
                Power Down Enable
                Allows you to enable or disable DDR power down mode.
                Configuration options: [Disabled] [Enabled] [Auto]
DDR RAS
        Disable Memory Error Injection
        Configuration options: [False] [True] [Auto]
        DDR ECC Configuration
        Allows you to configure DDR ECC configurations.
DDR Security
        TSME
        Configuration options: [Auto] [Enabled] [Disabled]
        Data Scramble
        Configuration options: [Enabled] [Disabled] [Auto]
DDR Addressing Options
        Chipselect Interleaving
        Interleave memory blocks across the DRAM chip selects for node 0.
        Configuration options: [Disabled] [Auto]
        Address Hash Bank
        Allows you to enable or disable bank address hashing.
        Configuration options: [Disabled] [Enabled] [Auto]
        Address Hash CS
        Enable or disable CS address hashing.
        Configuration options: [Auto] [Enabled] [Disabled]
        Address Hash Subchannel
        Enable or disable sub-channel address hashing.
        Configuration options: [Auto] [Enabled] [Disabled]
        BankSwapMode
        Configuration options: [Auto] [Disabled] [Swap CPU] [Swap APU]
DDR Training Options
        DFE Read Training
        Perform 2D Read Training with DFE on.
        Configuration options: [Auto] [Enable] [Disable]
        DRAM PDA Enumerate ID Programming Mode
        Configuration options: [Auto] [Sequential PDA enumeration mode]
        [Legacy PDA enumeration mode]

                                                                            69

                       TX DFE Taps
                       Specifies the number of TX DFE taps.
                       Configuration options: [Auto] [1 Tap] [2 Taps] [3 Taps] [4 Taps]
                       PPT Control
                       Specifies the PPT Control.
                       Configuration options: [Auto] [Disabled] [Relock+Retrain only] [UMC
                       Snoop PPT] [DFI Retrain PPT] [Relock Only] [Relock Only with DFI
                       PPT]
                       DDR Training Runtime Reduction
                       [Disabled] Force Disable DDR Training Runtime Reduction.
                       [Enabled] Force Enable DDR Training Runtime Reduction.
                       [Auto]		Default code behavior. If OC is ENABLE, DDR Training
                                  Runtime Reduction will be DISABLE by DEFAULT.
                       RX Burst Length
                       Extended sequence for read training.
                       [Auto] Default code behavior.
                       [1 x ] 1 x burst length.
                       [2 x ] 2 x burst length.
                       [4 x ] 4 x burst length.
                       [8 x ] 8 x burst length.
                       Nitro TX Burst Length
                       Extended sequence for write training.
                       [Auto] Default code behavior.
                       [1 x ] 1 x burst length.
                       [2 x ] 2 x burst length.
                       [4 x ] 4 x burst length.
                       [8 x ] 8 x burst length.
                       RX2D_TrainOpt
                       Configuration options: [Auto] [Manual]

     NOTE: The following items appear only when RX2D_TrainOpt is set to [Manual].

                       RX2D_DFE
                       Used to force Rx DFE on or off.
                       Configuration options: [Auto] [Disabled] [Enabled]
                       RX2D Voltage Step Size (2^n)
                       0 = 1 DAC setting between checked values. 1 = 2 DAC settings
                       between checked values. 2 = 4 DAC settings between checked
                       values. 3 = 8 DAC settings between checked values.
                       RX2D Delay Step Size (2^n)
                       0 = 1 LCDL delays between checked values. 1 = 2 LCDL delays
                       between checked values. 2 = 4 LCDL delays between checked values.
                       3 = 8 LCDL delays between checked values.
                       TX2D_TrainOpt
                       Configuration options: [Auto] [Manual]

70

NOTE: The following items appear only when TX2D_TrainOpt is set to [Manual].

                  TX2D_DFE
                  Configuration options: [Auto] [Disabled] [Enabled]
                  TX2D Voltage Step Size (2^n)
                  0 = 1 DAC setting between checked values. 1 = 2 DAC settings
                  between checked values. 2 = 4 DAC settings between checked
                  values. 3 = 8 DAC settings between checked values.
                  TX2D Delay Step Size (2^n)
                  0 = 1 LCDL delays between checked values. 1 = 2 LCDL delays
                  between checked values. 2 = 4 LCDL delays between checked values.
                  3 = 8 LCDL delays between checked values.
                  TX2D Voltage Step Multiplier
                  0 = Voltage Step Size is not modified. 1 = Voltage Step Size is
                  multiplied by 16.
                  TX2D Delay Step Multiplier
                  0 = Delay Step Size is not modified. 1 = Delay Step Size is multiplied
                  by 16.
                  Configuration options: [Auto] [Multiply DAC step size by 16] [No
                  Multiplier]
                  RX DFE Taps
                  Specifies the number of RX DFE taps.
                  Configuration options: [Auto] [1 Tap] [2 Taps] [3 Taps] [4 Taps]
        DDR MBIST Options
                  MBIST Enable
                  Allows you to enable or disable Memory MBIST.
                  Configuration options: [Disabled] [Enabled] [Auto]

NOTE: The following items appear only when MBIST Enable is set to [Enabled].

                  MBIST Test Mode
                  Allows you to select the MBIST Test Mode - Interface Mode (Tests
                  Single and Multiple CS transactions and Basic Connectivity) or Data
                  Eye Mode (Measures Voltage vs. Timing).
                  Configuration options: [Interface Mode] [Data Eye Mode] [Both] [Auto]
                  MBIST Aggressors
                  Allows you to enable or disable Memory Aggressor test.
                  Configuration options: [Disabled] [Enabled] [Auto]
                  MBIST Per Bit Slave Die Reporting
                  Reports 2D Data Eye Results in ABL Log for each DQ, Chipselect, and
                  Channel.
                  Configuration options: [Disabled] [Enabled] [Auto]
                  DDR Data Eye
                           Pattern Select
                           Configuration options: [Auto] [PRBS] [SSO] [Both]
                           Pattern Length Select
                           Configuration options: [Auto] [Manual]

                                                                                           71

         NOTE: The following items appear only when Pattern Length Select is set to [Manual].

                             Pattern Length
                           	This token helps to determine the pattern length. The
                             possible options are N=3...12.
                             Aggressor Channel
                           	This helps read the aggressors channels. If set to [Enabled],
                             you can read from one or more than one aggressor channel.
                             The default is set to [Disabled].
                             Configuration options: [Auto] [Disabled] [1 Aggressor
                             Channel] [3 Aggressor Channels] [7 Aggressor Channels]
                 DDR Memory Features
                           Memory Context Restore
                           Allows you to configure the memory context restore mode. When
                           enabled, DRAM re-training is avoided when possible and the POST
                           latency is minimized.
                           Configuration options: [Auto] [Enabled] [Disabled]
                 DDR Turnaround Times
                           Read Drift Adjustment
                           AUTO - Read Drift Adjustment 0.
                           Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1]
                           [plus 1] [plus 2] [plus 3] [plus 4]
                           Read Drift Adjustment P0-3
                           AUTO - Read Drift Adjustment 0.
                           Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1]
                           [plus 1] [plus 2] [plus 3] [plus 4]
                           Write Drift Adjustment
                           AUTO - Write Drift Adjustment 0.
                           Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1]
                           [plus 1] [plus 2] [plus 3] [plus 4]
                           Write Drift Adjustment P0-3
                           AUTO - Write Drift Adjustment 0.
                           Configuration options: [Auto] [minus 4] [minus 3] [minus 2] [minus 1]
                           [plus 1] [plus 2] [plus 3] [plus 4]
     NBIO Common Options
         PCIe ARI Support
         Enables Alternative Routing-ID Interpretation.
         Configuration options: [Disabled] [Enabled] [Auto]
         PCIe All Port ECRC
         Enable or disable PCIe all port ECRC.
         Configuration options: [Disabled] [Enabled] [Auto]
         Advanced Error Reporting (AER)
         Enable or disable support for Advanced Error Reporting (AER).
         Configuration options: [Not Supported] [Supported] [Auto]
         PCIe ARI Enumeration
         ARI Forwarding enabled for each downstream port.
         Configuration options: [Disable] [Enable] [Auto]

72

    GFX Configuration
            UMA Version
            [Legacy]   UMA Legacy Version
            [Non-Legacy]            UMA Non-Legacy Version
            [Auto]     Hybrid Secure
            GPU Host Translation Cache
            Allows you to enable or disable GPU Host Translation Cache.
            Configuration options: [Disabled] [Enabled] [Auto]
    Audio Configuration
            NB Azalia
            Allows you to enable or disable the integrated HD audio controller.
            Configuration options: [Disabled] [Enabled] [Auto]
            Audio IOs
            Configuration options: [Auto] [HDA(3SDI) + PDM(2CH)(Default)] [HDA (1SDI)
            + PDM(6CH)] [HDA(1SDI) + SW0(1MDATA) + PDM(2CH)] [SW0(4MDATA) +
            PDM(6CH)] [SW0(4MDATA) + SW1(1MDATA) + PDM(2CH)]
    PCIe loopback Mode
    Allows you to enable or disable PcieLoopBackMode.
    Configuration options: [Auto] [Disabled] [Enabled]
    Persistence mode for legacy endpoints
    Enable or disable persistence mode for legacy endpoints. Enable this option if some
    legacy PCIe devices are not detected.
    Configuration options: [Auto] [Disabled] [Enabled]
    EQ Bypass to Highest Rate
    Controls the ability to advertise Equalization Bypass to Highest Rate Support in TSxs
    sent prior to LinkUp=1.
    Configuration options: [Disable] [Enable] [Auto]
    Retimer margining support
    [Auto]         Disabled. Root port receiver margining support is enabled by default.
    [Enabled]         Enables support for margining a retimer.
    [Disabled]        Retimer margining is not supported.

SMU Common Options
    CPPC Dynamic Preferred Cores
    Configuration options: [Frequency] [Cache] [Driver] [Auto]
    TDP Control
    [Auto]            Use the default sustained power limit.
    [Manual]          User can set customized sustained power limit.

    NOTE: The following item appears only when TDP Control is set to [Manual].

    TDP
    Allows you to set the sustained power limit [mW].

                                                                                            73

     ECO Mode
     Adjust the CPU control limits to manage operation within a 65w thermal design power.
     [Enable]        Enables 65W processor power definition.
     [Disable]          System uses default processor power definition.
     PPT Control
     Specifies the PPT Control.
     Configuration options: [Manual] [Auto]

     NOTE: The following item appears only when PPT Control is set to [Manual].

     PPT
     Allows you to set the PPT [mW].
     Thermal Control
     [Auto]          Use the default TctlMax.
     [Manual]           User can set customized TctlMax.

     NOTE: The following item appears only when Thermal Control is set to [Manual].

     TjMax
     Allows you to set the maximum operating temperature [‘C] (IRM limit will be enforced).
     TDC Control
     [Auto]             Use the default TDC Limits.
     [Manual]           User can set customized TDC Limits.

     NOTE: The following item appears only when TDC Control is set to [Manual].

     TDC_VDDCR_VDD
     Allows you to set the VDDCR_VDD TDC Limit [mA] (IRM limit will be enforced).
     EDC Control
     [Auto]             Use the default EDC Limits.
     [Manual]           User can set customized EDC Limits.

     NOTE: The following item appears only when EDC Control is set to [Manual].

     EDC_VDDCR_VDD
     Allows you to set the VDDCR_VDD EDC Limit [mA] (IRM limit will be enforced).
     Fan Control
     [Auto]		 Use the default fan controller settings.
     [Manual]    User can set customized fan controller setting.

     NOTE: The following item appears only when Fan Control is set to [Manual].

     Fan Table Control
     [Auto]          Use the default fan table.
     [Manual]           User can set customized fan table.

74

NOTE: The following items appear only when Fan Table Control is set to [Manual].

Low Temperature
Allows you to set the low temperature [‘C].
Medium Temperature
Allows you to set the medium temperature [‘C].
High Temperature
Allows you to set the high temperature [‘C].
Critical Temperature
Allows you to set the critical temperature [‘C].
Low Pwm
Configuration options: [0] - [100]
Medium Pwm
Configuration options: [0] - [100]
High Pwm
Configuration options: [0] - [100]
Temperature Hysteresis
Allows you to set the temperature hysteresis [‘C].
PWM Frequency
[Auto]       Sets to the default option
[1]                100Hz
[0]                25kHz
Fan Polarity
[Auto]             Sets to the default option
[1]                Positive
[0]                Negative
VDDP Voltage Control
[Auto]        Use the default VDDP Voltage.
[Manual]           User can set custom VDDP Voltage.

NOTE: The following items appear only when VDDP Voltage Control is set to [Manual].

VDDP Voltage
Allows you to specify the target VDDP voltage [mV].
Infinity Fabric Frequency and Dividers
Configuration options: [Auto] [100 MHz] - [1066 MHz]
SyncFifo Mode Override
Configuration options: [Disable] [Enable] [Auto]
Sustained PowerLimit
PcdMsgSetSustainedPowerLimit.

                                                                                      75

            Fast PPT Limit
            PcdMsgSetFastPPTLimit.
            Slow PPT Limit
            PcdMsgSetSlowPPTLimit.
            Slow PPT Time Constant
            Slow PPT Time Constant [seconds].
            GFXOFF
            Configuration options: [Disable] [Enable] [Auto]

## 6.15 AMD PBS

     The items in this menu shows the AMD PBS Setup page.

            NOTE: The configuration options for this section vary depending on the motherboard. Please refer
            to the BIOS of your motherboard for the actual settings and options.

     Graphics Features
     This submenu allows you to configure Graphics Featurs - HG, DGPU Features and BOMACO
     configurations.
            Special Display Features
            Allows you to enable or disable HybridGraphics.
            Configuration options: [Disabled] [HybridGraphics]
            D3Cold Support
            Allows you to enable or disable PCIe x8 Slot D3Cold.
            Configuration options: [Disabled] [Enabled] [Dummy D3Cold]
            Discrete CPU_DSM Function A
            Allows you to enable or disable PCI-SIG ECN_DSM Function A for Discrete GPU’s GPP
            Bridge.
            Configuration options: [Disabled] [Enabled]
            Discrete CPU_DSM Function B
            Allows you to enable or disable PCI-SIG ECN_DSM Function B for Discrete GPU’s GPP
            Bridge.
            Configuration options: [Disabled] [Enabled]
            NVIDIA DGPU Power Enable
            For NVIDIA mobile DGPU card only. Output DGPU_EN# A19 pin and DGPU_SEL# B17
            pin to high at every power on state.
            Configuration options: [Disabled] [Enabled]
            Non-Eval Discrete GPU Support
            Set to [Enabled] to support Non-Eval Discrete GPU that doesn’t have specific EVAL_
            PWRGD(B30), EVAL_PRESENT#(A5).
            Configuration options: [Disabled] [Enabled]

76

      Discrete GPU HPD Circuitry
      Allows you to enable or disable Discrete GPU Display HPD Circuitry.
      Configuration options: [OR Circuitry] [Pulse Circuitry]
      Discrete GPU’s USB Port
      Allows you to disable Discrete GPU’s USB Port or keep default setting.
      Configuration options: [Keep Default Setting] [Disabled]
      Discrete GPU’s SSID/SVID
      Program Discrete GPU’s SSID/SVID depends on HybridGraphics setting.
      Configuration options: [Keep Default Setting] [Program by Vendor]
      Discrete GPU BOMACO Support
      Allows you to enable or disable Discrete GPU BOMACO Support.
      Configuration options: [Disabled] [Enabled]
USB4 configuration (ASM4242 Controller)
USB4 configuration (ASM4242 Controller) - PCIe resource, D3 support, Native USB4 support,
and other options.
      USB4 (ASM4242 Controller) Support
      Enable or disable USB4 (ASM4242 Controller) PCIe slot.
      Configuration options: [Disabled] [Enabled]

      NOTE: The following items appear only when USB4 (ASM4242 Controller) Support is set to
      [Enabled].

      PCIe Bus Number
      Reserve USB4 (ASM4242 Controller) PCIe Bus number per port (16 ~ 56).
      PCIe Non-Prefetchable MMIO (MB)
      Reserve USB4 (ASM4242 Controller) PCIe Non-Prefetchable MMIO per port (256 ~
      4096 MB).
      PCIe Prefetchable MMIO (GB)
      Reserve USB4 (ASM4242 Controller) PCIe Prefetchable MMIO per port (1 ~ 512 GB).
      ACPI D3 Support
      Disable or enable USB4 (ASM4242 Controller) ACPI D3 Support.
      Configuration options: [Disabled] [D3Hot]
      XHCI Port0-1 Speed
      Configures the USB4 (ASM4242 Controller) XHCI Port0-1 Speed.
      Configuration options: [Gen1x1] [Gen1x2] [Gen2x1] [Gen2x2]
AMD Variable Protection
Protect some AMD specific variables for CBS, PBS and AOD. If locked, some utilities like RU
that modify variable at runtime do not work.
Configuration options: [Disabled] [Enabled]
Processor Aggregator Device
Enable or disable Processor Aggregator Device.
Configuration options: [Disabled] [Enabled]

                                                                                               77

            NOTE: The following item appears only when Processor Aggregator Device is set to [Enabled].

     Core Count Control
     Enable or disable Core Count Control.
     Configuration options: [Disabled] [Enabled]
     HDMI 3.0G Tx SLEW
     Configuration options: [Disabled] [Enabled]

            NOTE: The following item appears only when HDMI 3.0G Tx SLEW is set to [Enabled].

     HDMI 3.0G Tx Slew Control Value
     HDMI 3.0G Tx Slew Control Value (0 ~ 255).

## 6.16 AMD Overclocking

     The items in this menu shows the AMD Overclocking Setup page.

            NOTE: The configuration options for this section vary depending on the motherboard. Please refer
            to the BIOS of your motherboard for the actual settings and options.

            CAUTION! Damage caused by use of your AMD processor outside of specification or in excess of
            factory settings are not covered by your system manufacturers warranty.

            NOTE: The following items appear only when [Accept] is selected for AMD Overclocking.

     Manual CPU Overclocking
            CPU Core Count Control
                    CCD 00 Bit Map Down Core Control
                    Setting this item to 1 means core is enabled, setting this item to 0 means core
                    is software down.
                    Bit Map Down Core Discard Changes
                    Discard changes.
                    Bit Map Down Core Apply Changes
                    Check and apply changes, need to make sure core number is equaled in each
                    CCD.
                    SMT Control
                    Can be used to disable symmetric multithreading. To re-enable SMT, a POWER
                    CYCLE is needed after selecting the [Auto] option.
                    Configuration options: [Auto] [Disable]

            CAUTION! S3 is NOT SUPPORTED on systems where SMT is disabled.

78

DDR and Infinity Fabric Frequency/Timings
     DDR Options
              DDR Timing Configuration
                        EXPO
                        Enabling EXPO will detect if a Memory OC Profile is present on the
                        installed DIMMs and pretrain that profile / apple needed voltages to
                        later set that profile if desired.
                        Configuration options: [Auto] [Enabled]

     NOTE: The following item appears only when EXPO is set to [Enabled].

                        EXPO Profile
                        Select EXPO Profile. CL means Minimum CAS Latency.
                        Active Memory Timing Settings
                        Configuration options: [Auto] [Enabled]

     NOTE: The following items appear only when Active Memory Timing Settings is set to [Enabled].

                        Memory Target Speed
                        Specifies the memory target speed in MT/s. The valid input is 2000
                        MT/s, 2400 MT/s, and range of 3200 MT/s ~ 12000 MT/s (stepping
                        of 200 MT/s). The user input value will be rounded down to align with
                        the stepping of 200 MT/s.
                        DDR SPD Timing
                                 Tcl Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Tcl Ctrl is set to [Manual].

                          Tcl
                        	Specifies the CAS Latency. Valid values: 0x16 ~ 0x3E, with a
                          stepping of 2. The value is in hex.
                                 Trcd Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trcd Ctrl is set to [Manual].

                          Trcd
                        	Specifies the RAS# Active to CAS# Read Delay Time. Valid
                          values: 0x8 ~ 0x3E with a stepping of 2. The value is in hex.
                                 Trp Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

                                                                                                     79

     NOTE: The following item appears only when Trp Ctrl is set to [Manual].

                          Trp
                        	Specifies Row Precharge Delay Time. Valid values: 0x8 ~
                          0x3E with a stepping of 2. The value is in hex.
                                 Tras Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Tras Ctrl is set to [Manual].

                          Tras
                        	Specifies Active to Precharge Delay Time. Valid values: 0x1E
                          ~ 0x7E.The value is in hex.
                                 Trc Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trc Ctrl is set to [Manual].

                          Trc
                        	Specifies Active to Active/Refresh Delay Time. Valid values:
                          0x20 ~ 0xFF. The value is in hex.
                                 Twr Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Twr Ctrl is set to [Manual].

                          Twr
                        	Specifies the Minimum Write Recovery Time. Valid values:
                          0x30 ~ 0x60, stepping of 6. The value is in hex.
                                 Trfc1 Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

     NOTE: The following item appears only when Trfc1 Ctrl is set to [Manual].

                          Trfc1
                        	Specifies the Refresh Recovery Delay Time (tRFC1). Valid
                          values: 0x32 ~ 0xFFF. The value is in hex.
                                 Trfc2 Ctrl
                                 [Auto]          Follow default setting.
                                 [Manual]        Manually specify.

80

NOTE: The following item appears only when Trfc2 Ctrl is set to [Manual].

                     Trfc2
                   	Specifies the Refresh Recovery Delay Time (tRFC2). Valid
                     values: 0x32 ~ 0xFFF. The value is in hex.
                            TrfcSb Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when TrfcSb Ctrl is set to [Manual].

                     TrfcSb
                   	Specifies the Refresh Recovery Delay Time (tRFCSb). Valid
                     values: 0x32 ~ 0x7FF. The value is in hex.
                            Trtp Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when Trtp Ctrl is set to [Manual].

                     Trtp
                   	Specifies the Read CAS# to Precharge command delay time.
                     Valid values: 0x5 ~ 0x1F. The value is in hex.
                            TrrdL Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when TrrdL Ctrl is set to [Manual].

                     TrrdL
                   	Specifies the Activate to Activate Delay Time, same bank
                     group (tRRD_L). Valid values: 0x4 ~ 0x20. The value is in hex.
                            TrrdS Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

NOTE: The following item appears only when TrrdS Ctrl is set to [Manual].

                     TrrdS
                   	Specifies the Activate to Activate Delay Time, different bank
                     group (tRRD_S). Valid values: 0x4 ~ 0x14. The value is in hex.
                            Tfaw Ctrl
                            [Auto]          Follow default setting.
                            [Manual]        Manually specify.

                                                                                      81

     NOTE: The following item appears only when Tfaw Ctrl is set to [Manual].

                          Tfaw
                        	Specifies the Four Activate Window Time. Valid values: 0x14
                          ~ 0x50. The value is in hex.
                                 TwtrL Ctrl
                                 [Auto]         Follow default setting.
                                 [Manual]       Manually specify.

     NOTE: The following item appears only when TwtrL Ctrl is set to [Manual].

                          TwtrL
                        	Specifies the Minimum Write to Read Time, the same bank
                          group. Valid values: 0x8 ~ 0x30. The value is in hex.
                                 TwtrS Ctrl
                                 [Auto]         Follow default setting.
                                 [Manual]       Manually specify.

     NOTE: The following item appears only when TwtrS Ctrl is set to [Manual].

                          TwtrS
                        	Specifies the Minimum Write to Read Time, different bank
                          group. Valid values: 0x2 ~ 0x10. The value is in hex.
                        DDR Non-SPD Timing
                                 TrdrdScL Ctrl
                                 [Auto]        Follow default setting.
                                 [Manual]      Manually specify.

     NOTE: The following item appears only when TrdrdScL Ctrl is set to [Manual].

                          TrdrdScL
                        	Specifies the CAS to CAS delay time, same bank group. Valid
                          values: 0x1 ~ 0xF. The value is in hex.
                                 TrdrdSc Ctrl
                                 [Auto]       Follow default setting.
                                 [Manual]     Manually specify.

     NOTE: The following item appears only when TrdrdSc Ctrl is set to [Manual].

                          TrdrdSc
                        	Specifies the Read to Read turnaround timing in the same
                          chipselect. Valid values: 0x1 ~ 0xF. The value is in hex.
                                 TrdrdSd Ctrl
                                 [Auto]       Follow default setting.
                                 [Manual]     Manually specify.

82

NOTE: The following item appears only when TrdrdSd Ctrl is set to [Manual].

                     TrdrdSd
                   	Specifies the Read to Read turnaround timing in the same
                     DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TrdrdDd Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

NOTE: The following item appears only when TrdrdDd Ctrl is set to [Manual].

                     TrdrdDd
                   	Specifies the Read to Read turnaround timing in a different
                     DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TwrwrScL Ctrl
                            [Auto]      Follow default setting.
                            [Manual]    Manually specify.

NOTE: The following item appears only when TwrwrScL Ctrl is set to [Manual].

                     TwrwrScL
                   	Specifies the CAS to CAS Delay Time, same bank group. Valid
                     values: 0x1 ~ 0x3F. The value is in hex.
                            TwrwrSc Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

NOTE: The following item appears only when TwrwrSc Ctrl is set to [Manual].

                     TwrwrSc
                   	Specifies the Write to Write turnaround timing in the same
                     chipselect. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TwrwrSd Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

NOTE: The following item appears only when TwrwrSd Ctrl is set to [Manual].

                     TwrwrSd
                   	Specifies the Write to Write turnaround timing in the same
                     DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                            TwrwrDd Ctrl
                            [Auto]       Follow default setting.
                            [Manual]     Manually specify.

                                                                                   83

     NOTE: The following item appears only when TwrwrDd Ctrl is set to [Manual].

                          TwrwrDd
                        	Specifies the Write to Write turnaround timing in a different
                          DIMM. Valid values: 0x1 ~ 0xF. The value is in hex.
                                 Twrrd Ctrl
                                 [Auto]         Follow default setting.
                                 [Manual]       Manually specify.

     NOTE: The following item appears only when Twrrd Ctrl is set to [Manual].

                          Twrrd
                        	Specifies the Write to Read turnaround timing. Valid values:
                          0x1 ~ 0xF. The value is in hex.
                                 Trdwr Ctrl
                                 [Auto]         Follow default setting.
                                 [Manual]       Manually specify.

     NOTE: The following item appears only when Trdwr Ctrl is set to [Manual].

                          Trdwr
                        	Specifies the Read to Write turnaround timing. Valid values:
                          0x1 ~ 0x1F. The value is in hex.
              DDR BUS Configuration
                        Processor CS drive strengths
                        Specifies the Processor CS drive strengths.
                        Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                        [30.0 Ohm]
                        Processor CKI drive strengths
                        Specifies the Processor CK drive strengths.
                        Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                        [30.0 Ohm]
                        Processor CA drive strengths
                        Specifies the Processor CA drive strengths.
                        Configuration options: [Auto] [120.0 Ohm] [60.0 Ohm] [40.0 Ohm]
                        [30.0 Ohm]
                        Processor DQ drive strengths
                        Select the drive strength for all DQ and DMI IOs.
                        Configuration options: [Auto] [High Impedance] [240 ohm] [120 ohm]
                        [80 ohm] [60 ohm] [48 ohm] [40 ohm] [34.3 ohm]
                        Processor ODT impedance
                        Select the impedance for all DBYTE IOs.
                        Configuration options: [Auto] [High Impedance] [480 ohm] [240 ohm]
                        [160 ohm] [120 ohm] [96 ohm] [80 ohm] [68.8 ohm] [60 ohm]
                        Dram DQ drive strengths
                        Selects the Dram Pull-up ahnd Pull-down Output Driver Impedance
                        for all DQ and DMI IOs.
                        Configuration options: [Auto] [48 ohm] [40 ohm] [34 ohm]

84

                  Dram ODT impedance RTT_NOM_WR
                  Select the DRAMs On-die Termination impedance RTT_NOM_WR.
                  Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
                  [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
                  Dram ODT impedance RTT_NOM_RD
                  Select the DRAMs On-die Termination impedance RTT_NOM_RD.
                  Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
                  [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
                  Dram ODT impedance RTT_WR
                  Select the DRAMs On-die Termination impedance RTT_WR.
                  Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
                  [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
                  Dram ODT impedance RTT_PARK
                  Select the DRAMs On-die Termination impedance RTT_PARK.
                  Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
                  [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
                  Dram ODT impedance DQS_RTT_PARK
                  Select the DRAMs On-die Termination impedance DQS_RTT_PARK.
                  Configuration options: [Auto] [RTT_OFF] [RZQ (240)] [RZQ/2 (120)]
                  [RZQ/3 (80)] [RZQ/4 (60)] [RZQ/5 (48)] [RZQ/6 (40)] [RZQ/7 (34)]
        DDR Controller Configuration
                  DDR Power Options
                           Power Down Enable
                           Allows you to enable or disable DDR power down mode.
                           Configuration options: [Disabled] [Enabled] [Auto]
                  Additional Memory Tweaks
                           RX2D_TrainOpt
                           Configuration options: [Auto] [Manual]

NOTE: The following items appear only when RX2D_TrainOpt is set to [Manual].

                    RX2D_DFE
                  	Used to force Rx DFE on or off. This is always enabled when
                    Runtime Reduction is disabled.
                    Configuration options: [Auto] [Disable] [Enable]
                    RX2D Voltage Step Size (2^n)
                  	0 = 1 DAC setting between checked values. 1 = 2 DAC
                    settings between checked values. 2 = 4 DAC settings
                    between checked values. 3 = 8 DAC settings between
                    checked values.
                    Configuration options: [Auto] [1 DAC steps per loop] [2 DAC
                    steps per loop] [4 DAC steps per loop] [8 DAC steps per loop]
                    RX2D Delay Step Size (2^n)
                  	0 = 1 LCDL delays between checked values. 1 = 2 LCDL
                    delays between checked values. 2 = 4 LCDL delays between
                    checked values. 3 = 8 LCDL delays between checked values.
                    Configuration options: [Auto] [1 DAC steps per loop] [2 DAC
                    steps per loop] [4 DAC steps per loop] [8 DAC steps per loop]
                           TX2D_TrainOpt
                           Configuration options: [Auto] [Manual]

                                                                                      85

     NOTE: The following items appear only when TX2D_TrainOpt is set to [Manual].

                                TX2D_DFE
                                Configuration options: [Auto] [Disable] [Enable]
                         TX2D Voltage Step Size (2^n)
                       	0 = 1 DAC setting between checked values. 1 = 2 DAC
                         settings between checked values. 2 = 4 DAC settings
                         between checked values. 3 = 8 DAC settings between
                         checked values.
                         Configuration options: [Auto] [1 DAC steps per loop] [2 DAC
                         steps per loop] [4 DAC steps per loop] [8 DAC steps per loop]
                         TX2D Delay Step Size (2^n)
                       	0 = 1 LCDL delays between checked values. 1 = 2 LCDL
                         delays between checked values. 2 = 4 LCDL delays between
                         checked values. 3 = 8 LCDL delays between checked values.
                         Configuration options: [Auto] [1 DAC steps per loop] [2 DAC
                         steps per loop] [4 DAC steps per loop] [8 DAC steps per loop]
                         TX2D Voltage Step Multiplier
                       	0 = Voltage Step Size is not modified. 1 = Voltage Step Size is
                         multiplied by 16.
                         Configuration options: [Multiply DAC step size by 16] [No
                         Multiply]
                         TX2D Delay Step Multiplier
                       	0 = Delay Step Size is not modified. 1 = Delay Step Size is
                         multiplied by 16.
                         Configuration options: [Multiply DAC step size by 16] [No
                         Multiply]
                         RX DFE Taps
                       	Specifies the number of RX DFE taps. Value only applies
                         when RX2D_DFE is enabled.
                         Configuration options: [Auto] [1 Tap] [2 Tap] [3 Tap] [4 Tap]
                         TX DFE Taps
                       	Specifies the number of TX DFE taps. Value only applies
                         when TX2D_DFE is enabled.
                         Configuration options: [Auto] [1 Tap] [2 Tap] [3 Tap] [4 Tap]
             DDR5 Nitro Mode
             Can improve overclocked memory support for modules over 6000Mt/s with
             potential boot time and/or latency tradeoffs.
             Configuration options: [Auto] [Enable] [Disable]

     NOTE: The following items appear only when DDR Nitro Mode is set to [Enable].

             DDR5 Robust Training Mode
             A more comprehensive memory training algorithm that increases boot time
             but can result in improved stability at overclocked memory settings.
             Configuration options: [Auto] [Enable] [Disable]
             Nitro RX Data
             Configures the RX Timing between memory controller and PHY. Higher value
             may enable increased memory frequency at the expense of increased latency.
             Configuration options: [Auto] [1] [2] [Disabled]

86

             Nitro TX Data
             Configures the TX Timing between memory controller and PHY. Higher value
             may enable increased memory frequency at the expense of increased latency.
             Configuration options: [Auto] [0] [1] [2] [3] [Disabled]
             Nitro Control Line
             Configures the command timing latency between the memory controller and
             PHY. Higher value may enable increased memory frequency at the expense of
             increased latency.
             Configuration options: [Auto] [0] [1] [Disabled]
             Nitro RX Burst Length
             DQ Training Pattern Length - Higher number results in more robust training
             and longer runtime. Lower number results in less robust training and shorter
             runtime, but potentially less stability.
             Configuration options: [Auto] [1x] [2x] [4x] [8x]
             Nitro TX Burst Length
             DQ Training Pattern Length - Higher number results in more robust training
             and longer runtime. Lower number results in less robust training and shorter
             runtime, but potentially less stability.
             Configuration options: [Auto] [1x] [2x] [4x] [8x]
             Nitro DFE Vref Offset Limits
             Disabling the TxDFE/RxDEF Vref offset limit to give them more margin for
             those edge cases where the guardband is not sufficient.
             Configuration options: [Auto] [Disable]
     Infinity Fabric Frequency and Dividers
             Infinity Fabric Frequency and Dividers
             Allows you to set Infinity Fabric Frequency (FCLK). Auto = FCLK = MCLK.
             Manual = FCLK must be less than MCLK for best performance in most
             cases. Latency penalties are incurred if FCLK and MCLK are mismatched, but
             sufficiently high MCLK can negate or overcome this penalty.
             Configuration options: [Auto] [100 MHz] - [3000 MHz]
             UCLK DIV1 MODE
             Allows you to set UCLK DIV mode.
             Configuration options: [Auto] [UCLK=MEMCLK] [UCLK=MEMCLK/2]
Precision Boost Overdrive
     Precision Boost Overdrive
     When this item is enabled, it allows the processor to run beyond defined values for
     PPT, VDD_CPU EDC, VDD_CPU TDC, VDD_SOC EDC, VDD_SOC TDC to the limits of
     the board, and allows it to boost at higher voltages for longer durations than default
     operation.
     Configuration options: [Auto] [Disable] [Enabled] [Advanced]

                                                                                              87

     NOTE: The following items appear only when Precision Boost Overdrive is set to [Advanced].

     PBO Limits
     [Auto]	Loads AMD default socket power (PPT), electrically-limited VRM
                current (EDC), and thermally-limited VRM current (TDC) limits.
     [Disable]          Disabled PBO limits.
     [Motherboard]      Allows the processor to run according to increased PPT, EDC, and
                        TDC limits defined by your motherboard.
     [Manual]           Allows the processor to ignore AMD default limits for PPT, EDC, and
                        TDC and instead use manual values (up to the maximum capabilities
                        of the motherboard).

     NOTE: The following items appear only when PBO Limits is set to [Manual].

     PPT Limit [mW]
     Adjust total CPU socket power delivery capability. Adjustable up to the limit supported
     bu your motherboard.
     TDC Limit [mA]
     Adjust peak current from your motherboard’s CPU core VRM phases in thermally-
     limited scenarios. Adjustable up to the limit supported by you motherboard.
     EDC Limit [mA]
     Adjust peak current from your motherboard’s CPU core VRM phases in electrically-
     limited scenarios. Adjustable up to the limit supported by you motherboard.
     Precision Boost Overdrive Scalar Ctrl
     Configuration options: [Auto] [Manual]

     NOTE: The following item appears only when Precision Boost Overdrive Scalar Ctrl is set to
     [Manual].

     Precision Boost Overdrive Scalar
     Overrides the AMD default silicon health management to potentially achieve higher
     sustained frequencies under CPU load.
     Configuration options: [1X] - [10X]
     CPU Boost Clock Override
     Increases (Positive) or Decreases (Negative) the maximum CPU frequency that may
     be automatically achieved by the CPU Boost Algorithm.
     Configuration options: [Disabled] [Enabled (Positive)] [Enabled (Negative)]

     NOTE: The following item appears only when CPU Boost Clock Override is set to [Enabled
     (Positive)].

     Max CPU Boost Clock Override(+)
     Increases the maximum CPU frequency that may be automatically achieved by the
     Precision Boost 2 algorithm. Use the <+> or <-> to adjust the value.

88

NOTE: The following item appears only when CPU Boost Clock Override is set to [Enabled
(Negative)].

Max CPU Boost Clock Override(-)
Decreases the maximum CPU frequency that may be automatically achieved by the
Precision Boost 2 algorithm. Use the <+> or <-> to adjust the value.
Platform Thermal Throttle Ctrl
Allows the user to decrease the maximum allowed processor temperature (celsius)
Configuration options: [Manual] [Auto]

NOTE: The following item appears only when Platform Thermal Throttle Ctrl is set to [Manual].

Platform Thermal Throttle Limit
Allows the user to decrease the maximum allowed processor temperature (celsius)
GFX Curve Optimizer
         GFX Curve Optimizer
         Allows the user to shift the GFX Voltage / Frequency (AVFS) curve to include
         higher voltages (positive values) or lower voltages (negative values). The
         larger the value entered the larger the magnitude of the voltage shift.
         Configuration options: [Disable] [GFX Curve Optimizer]

NOTE: The following items appear only when GFX Curve Optimizer is set to [GFX Curve Optimizer].

         GFX Curve Optimizer Sign
         Determines the direction of the curve shift for GFX. Positive shifts the curve
         up to use higher voltages. Negative shifts the curve down to use lower
         voltages.
         Configuration options: [Positive] [Negative]
         GFX Curve Optimizer Magnitude
         Determines the magnitude of the GFX curve shift to be made (entered in
         whole numbers) the larger the value entered the larger the magnitude of the
         shift. Field defaults to 0 and the user can enter whole integer numbers. Value
         entered, combined with the sign above, is used to send the SMU and GFX
         Curve Optimizer.
Curve Optimizer
         Curve Optimizer
         Allows the user to shift the Voltage / Frequency (AVFS) curve to include higher
         voltages (positive values) or lower voltages (negative values). The larger the
         value entered the larger the magnitude of the voltage limit.
         Configuration options: [Disable] [All Cores] [Per Core] [Per CCD]

NOTE: The following items appear only when Curve Optimizer is set to [All Cores].

         All Core Curve Optimizer Sign
         Determines the direction of the curve shift on all cores. Positive shifts the
         curve up to use higher voltages. Negative shifts the curve down to use lower
         voltages.
         Configuration options: [Positive] [Negative]

                                                                                                  89

                 All Core Curve Optimizer Magnitude
                 Determines the magnitude of the curve shift to be made (entered in whole
                 numbers) the larger the value entered the larger the magnitude of the shift.

         NOTE: The following items appear only when Curve Optimizer is set to [Per Core].

                 Core 0-7 Curve Optimizer Sign
                 Determines the direction of the curve shift on this core. Positive shifts the
                 curve up to use higher voltages. Negative shifts the curve down to use lower
                 voltages.
                 Configuration options: [Positive] [Negative]
                 Core 0-7 Curve Optimizer Magnitude
                 Determines the magnitude of the curve shift to be made to this core (entered
                 in whole numbers) the larger the value entered the larger the magnitude of the
                 shift.

         NOTE: The following items appear only when Curve Optimizer is set to [Per CCD].

                 CCD 0 Curve Optimizer Sign
                 Determines the direction of the curve shift on this core. Positive shifts the
                 curve up to use higher voltages. Negative shifts the curve down to use lower
                 voltages.
                 Configuration options: [Positive] [Negative]
                 CCD 0 Curve Optimizer Magnitude
                 Determines the magnitude of the curve shift to be made to this core (entered
                 in whole numbers) the larger the value entered the larger the magnitude of the
                 shift.
     VDDG Voltage Control
         VDDG Voltage Control
         VDDG represents voltage for the data portion of the Infinity Fabric. It is derived
         from the CPU SoC/Uncore Voltage (VDD_SOC). VDDG can approach but not exceed
         VDD_SOC.
         Configuration options: [Auto] [Global VDDG Voltage Control] [Per-CCD VDDG Voltage
         Control]

         NOTE: The following items appear only when VDDG Voltage Control is set to [Global VDDG
         Voltage Control].

         Global VDDG CCD Voltage
         VDDG CCD represents voltage for the data portion of the Infinity Fabric. Range is
         650mV ~ 1650mV. Stepping is 10mV.
         Configuration options: [Auto] [VDDG voltage 650mV] - [VDDG voltage 1650mV]
         Global VDDG IOD Voltage
         VDDG IOD represents voltage for the data portion of the Infinity Fabric. . Range is
         650mV - 1650mV. Stepping is 10mV.
         Configuration options: [Auto] [VDDG voltage 650mV] - [VDDG voltage 1650mV]

90

    NOTE: The following items appear only when VDDG Voltage Control is set to [Per-CCD VDDG
    Voltage Control].

    CCD0-CCD VDDG Voltage
    VDDG CCD represents voltage for the data portion of the Infinity Fabric. Range is
    650mV ~ 1650mV. Stepping is 10mV.
    Configuration options: [Auto] [VDDG voltage 650mV] - [VDDG voltage 1650mV]
    CCD0-IOD VDDG Voltage
    VDDG IOD represents voltage for the data portion of the Infinity Fabric. . Range is
    650mV - 1650mV. Stepping is 10mV.
    Configuration options: [Auto] [VDDG voltage 650mV] - [VDDG voltage 1650mV]
VDDP Voltage Control
    VDDP Voltage Control
    Allows the user to adjust the VDDP voltage.
    [Auto]                VDDP is system default.
    [Manual]              Set voltage for the DDR bus signaling (PHY).

    NOTE: The following items appear only when VDDP Voltage Control is set to [Manual].

    VDDP Voltage Adjust
    VDDP is a voltage for the DDR bus signaling (PHY), and it is dervied from your DRAM
    Voltage (VDDIO_Mem). As a result, VDDP voltage in mV can approach but not exceed
    your DRAM Voltage. Stepping is 5mv.
SoC/Uncore OC Mode
    SoC/Uncore OC Mode
    Forces CPU SoC/Uncore components (e.g. Infinity Fabric, memory, and integrated
    graphics) to run at their maximum specified frequency at all times. May improve
    performance at the expense of idle power savings.
    Configuration options: [Auto] [Enabled] [Disabled]
SoC Voltage
    SoC Voltage
    Specifies the SoC/Uncore voltage (VDD_SOC) in mV to support memory and Infinity
    Fabric overclocking. VDD_SOC also determines the GPU voltage on processors with
    integrated graphics. Stepping is 5mv. Voltage ranges allowed to be set will be limited
    outside of LN2 mode. If in LN2 mode (and CPU temp is below -40c) the allowable
    range of settable voltages will be extended.
VDD Misc
    VDD Misc Control
    Allows the user to adjust the VDD Misc Voltage.
    [Auto]           VDD MISC is set to system default.
    [Manual]          Set voltage for the GMI PHY.

                                                                                              91

         NOTE: The following item appears only when VDD Misc Control is set to [Manual].

         VDD Misc Voltage
         Specifies the VDD MISC Voltage in mV, definitely follow SVI3 type 2 Slave VID (500-
         5600mV, step 10mV). Note that the minimum voltage supported is based on the
         specific processor, such as Raphael OC require the voltage higher than 1100mv.
         Voltage ranges allowed to be set will be limited outside of LN2 mode. If LN2 mode
         (and CPU temp is below -40c) the allowable range of settable voltages will be
         extended.
     LCLK Frequency Control
         LCLK Frequency Control
         [Auto]        Use default settings.
         [Manual]           Manually configure LCLK frequency.

         NOTE: The following item appears only when LCLK Frequency Control is set to [Manual].

         Maximum Frequency
         Allows you to set the maximum LCLK frequency. Range: 1029 ~ 2500.
     Onboard Voltage Control
         VDDIO Voltage Control
                  VDDIO Ctrl
                  Allows the user to adjust the VDDIO voltage.
                  [Auto]		         Use the default VDDIO voltage.
                  [Manual]         Set DIMM VDD/VDDQ to synchronize to APU VDDIO.
                  [Separate]       Independent control of APU VDDIO, DIMM VDD/VDDQ.

         IMPORTANT! Running VDDQ != VDD is non-standard and may cause memory stability issues. Take
         care that during ramp down and ramp up, the VDDQ-VDD voltage must be less than 200mV.

         NOTE: The following item appears only when VDDIO Ctrl is set to [Manual] or [Separate].

                  DIMM VDD Adjust
                  Adjust DIMM Power Supply, stepping is 10mV. Range is from 800mV to
                  1430mV. Take care that during ramp down and ramp up, the VDDQ-VDD
                  voltage must be less than 200mV.

         NOTE: The following items appear only when VDDIO Ctrl is set to [Separate].

                  DIMM VDDQ Adjust
                  Adjust DIMM DQ Power Supply, stepping is 10mV. Range is from 800mV
                  to 1430mV. Take care that during ramp down and ramp up, the VDDQ-VDD
                  voltage must be less than 200mV, and Vpp must always be equal to or greater
                  than VDDQ.
                  APU VDDIO Adjust
                  Adjust APO VDDIO, stepping is 10mV. Range is from 700mV to 1400mV.

92

        Enable Platform PMIC Control
        When Enable Platform PMIC Control is enabled, the DDR PMIC voltages are
        not adjusted by processor FW, and may be adjusted directly by EC or other
        platform based mechanism.
        Configuration options: [Auto] [Enable] [Disable]
VPP Voltage Control
        VPP Ctrl
        [Auto]		           Use the default setting.
        [Manual]           Manually specify the memory VPP Voltage.

NOTE: The following item appears only when VPP Ctrl is set to [Manual].

        VPP Adjust
        Adjust MEM VPP, stepping is 10mV. Range is from 1500mV to 2135mV.
        Configuration options: [1500] - [2135]
ECO Mode
        ECO Mode
        Configuration options: [Auto] [65W]

                                                                                    93

     7.           Monitor menu
     The Monitor menu displays the system temperature/power status, and allows you to change
     the fan settings.
     Scroll down to display the other BIOS items.

           NOTE: The settings and options of this menu may vary depending on your motherboard. Please
           refer to the BIOS of your motherboard for the actual settings and options.

     Temperature Monitor
           CPU Temperature, CPU Package Temperature, MotherBoard Temperature, VRM
           Temperature, Chipset Temperature, T_Sensor Temperature, DIMM A Temperature,
           DIMM B Temperature [xxx°C/xxx°F]
           The onboard hardware monitor automatically detects and displays the temperatures
           for the different components. Select [Ignore] if you do not wish to display the detected
           temperatures.
     Fan Speed Monitor
           CPU Fan Speed, CPU Optional Fan Speed, Chassis Fan Speed, AIO PUMP Speed
           [xxxx RPM]
           The onboard hardware monitor automatically detects and displays the fan speeds in
           rotations per minute (RPM). If the fan is not connected to the motherboard, the field
           shows N/A. Select [Ignore] if you do not wish to display the detected speed.
     Voltage and Current Monitor
           CPU Core Voltage, 12V Voltage, 5V Voltage, 3.3V Voltage, CPU VDDIO / MC Voltage
           [x.xxx V]
           The onboard hardware monitor automatically detects the voltage output through the
           onboard voltage regulators. Select [Ignore] if you do not want to detect this item.

94

Q-Fan Configuration
    Q-Fan Tuning
    Click this item to automatically detect the lowest speed and configure the minimum
    duty cycle for each fan.

     CAUTION! The process may take 2 to 5 minutes. DO NOT shut down or reset your system during
    the tuning process.

    CPU Q-Fan Control
    Allows you to set the CPU Q-Fan operating mode.
    [Auto Detect]      Detects the type of installed fan/pump and automatically switches
                       the control modes.
    [DC Mode]            Enables the Q-Fan Control feature in DC mode for 3-pin fan/pump.
    [PWM Mode]           Enables the Q-Fan Control feature in PWM mode for 4-pin fan/
                         pump.

    CPU Fan Profile
    Allows you to set the appropriate performance level of the assigned fan/pump. When
    selecting [Manual], we suggest raising your fan/pump duty to 100% if your CPU
    temperature exceeds 75°C. Please be noted CPU performance will throttle due to
    overheating with inefficient fan/pump duty.
    Configuration options: [Standard] [Silent] [Turbo] [Full Speed] [Manual]

    NOTE: The following items appear only when CPU Fan Profile is set to [Standard], [Silent], [Turbo],
    or [Manual].

    CPU Fan Q-Fan Source
    The assigned fan/pump will be controlled according to the selected temperature
    source.
    Configuration options: [CPU] [CPU Package]
    CPU Fan Step Up
    Step up allows you to adjust how quickly the fan rotation speed increases, with
    level 0 being an instantaneous change in speed. The higher the level, the slower the
    change in speed, and may also result in less noise, but this will also cause slower heat
    dissipation.
    Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]
    CPU Fan Step Down
    Step down allows you to adjust how quickly the fan rotation speed decreases, with
    level 0 being an instantaneous change in speed. The higher the level, the slower the
    change in speed, and may also result in less noise, but this will also cause slower heat
    dissipation.
    Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]

                                                                                                          95

     CPU Fan Speed Low Limit
     Allows you to set the lower speed limit for assigned fan/pump. A warning message
     will appear when the limit is reached; the warning message will not appear if [Ignore]
     is selected.
     Configuration options: [Ignore] [200 RPM] [300 RPM] [400 RPM] [500 RPM] [600 RPM]

     NOTE: The following items appear only when CPU Fan Profile is set to [Manual].

     CPU Fan Point8 Temperature
     When the temperature source is lower than the temperature of P8, the duty cycle
     will be determined according to the P7-P8 and the temperature source. When the
     temperature source is higher than the temperature of P8, the fan will operate at the
     duty cycle of P8.
     CPU Fan Point8 Duty Cycle (%)
     When the temperature source is lower than the temperature of P8, the duty cycle
     will be determined according to the P7-P8 and the temperature source. When the
     temperature source is higher than the temperature of P8, the fan will operate at the
     duty cycle of P8.
     CPU Fan Point7 Temperature
     When the temperature source is lower than the temperature of P7, the duty cycle
     will be determined according to the P6-P7 and the temperature source. When the
     temperature source is higher than the temperature of P7, the duty cycle will be
     determined according to the P7-P8 and the temperature source.
     CPU Fan Point7 Duty Cycle (%)
     When the temperature source is lower than the temperature of P7, the duty cycle
     will be determined according to the P6-P7 and the temperature source. When the
     temperature source is higher than the temperature of P7, the duty cycle will be
     determined according to the P7-P8 and the temperature source.
     CPU Fan Point6 Temperature
     When the temperature source is lower than the temperature of P6, the duty cycle
     will be determined according to the P5-P6 and the temperature source. When the
     temperature source is higher than the temperature of P6, the duty cycle will be
     determined according to the P6-P7 and the temperature source.
     CPU Fan Point6 Duty Cycle (%)
     When the temperature source is lower than the temperature of P6, the duty cycle
     will be determined according to the P5-P6 and the temperature source. When the
     temperature source is higher than the temperature of P6, the duty cycle will be
     determined according to the P6-P7 and the temperature source.
     CPU Fan Point5 Temperature
     When the temperature source is lower than the temperature of P5, the duty cycle
     will be determined according to the P4-P5 and the temperature source. When the
     temperature source is higher than the temperature of P5, the duty cycle will be
     determined according to the P5-P6 and the temperature source.
     CPU Fan Point5 Duty Cycle (%)
     When the temperature source is lower than the temperature of P5, the duty cycle
     will be determined according to the P4-P5 and the temperature source. When the
     temperature source is higher than the temperature of P5, the duty cycle will be
     determined according to the P5-P6 and the temperature source.

96

CPU Fan Point4 Temperature
When the temperature source is lower than the temperature of P4, the duty cycle
will be determined according to the P3-P4 and the temperature source. When the
temperature source is higher than the temperature of P4, the duty cycle will be
determined according to the P4-P5 and the temperature source.
CPU Fan Point4 Duty Cycle (%)
When the temperature source is lower than the temperature of P4, the duty cycle
will be determined according to the P3-P4 and the temperature source. When the
temperature source is higher than the temperature of P4, the duty cycle will be
determined according to the P4-P5 and the temperature source.
CPU Fan Point3 Temperature
When the temperature source is lower than the temperature of P3, the duty cycle
will be determined according to the P2-P3 and the temperature source. When the
temperature source is higher than the temperature of P3, the duty cycle will be
determined according to the P3-P4 and the temperature source.
CPU Fan Point3 Duty Cycle (%)
When the temperature source is lower than the temperature of P3, the duty cycle
will be determined according to the P2-P3 and the temperature source. When the
temperature source is higher than the temperature of P3, the duty cycle will be
determined according to the P3-P4 and the temperature source.
CPU Fan Point2 Temperature
When the temperature source is lower than the temperature of P2, the duty cycle
will be determined according to the P1-P2 and the temperature source. When the
temperature source is higher than the temperature of P2, the duty cycle will be
determined according to the P2-P3 and the temperature source.
CPU Fan Point2 Duty Cycle (%)
When the temperature source is lower than the temperature of P2, the duty cycle
will be determined according to the P1-P2 and the temperature source. When the
temperature source is higher than the temperature of P2, the duty cycle will be
determined according to the P2-P3 and the temperature source.
CPU Fan Point1 Temperature
When the temperature source is lower than the temperature of P1, the fan will operate
at the duty cycle of P1. When the temperature source is higher than the temperature
of P1, the duty cycle will be determined according to the P1-P2 and the temperature
source.
CPU Fan Point1 Duty Cycle (%)
When the temperature source is lower than the temperature of P1, the fan will operate
at the duty cycle of P1. When the temperature source is higher than the temperature
of P1, the duty cycle will be determined according to the P1-P2 and the temperature
source.

                                                                                        97

     Chassis Fan(s) Configuration
              Chassis Fan Q-Fan Control
              Allows you to set the Chassis Fan operating mode.
              [Auto Detect]        Detects the type of installed fan/pump and
                                   automatically switches the control modes.
              [DC Mode]            Enables the Q-Fan Control feature in DC mode for 3-pin
                                   fan/pump.
              [PWM Mode]           Enables the Q-Fan Control feature in PWM mode for
                                   4-pin fan/pump.
              Chassis Fan Profile
              Allows you to set the appropriate performance level of the assigned fan/
              pump. When selecting [Manual], we suggest raising your fan/pump duty
              to 100% if your CPU temperature exceeds 75°C. Please be noted CPU
              performance will throttle due to overheating with inefficient fan/pump duty.
              Configuration options: [Standard] [Silent] [Turbo] [Full Speed] [Manual]

     NOTE: The following items appear only when CPU Fan Profile is set to [Standard], [Silent], [Turbo],
     or [Manual].

              Chassis Fan Q-Fan Source
              The assigned fan/pump will be controlled according to the selected
              temperature source.
              Configuration options: [CPU] [CPU Package] [MotherBoard] [VRM] [T_Sensor]
              [Multiple Sources]

     NOTE: For Multiple Sources, select up to three temperature sources and the fan will automatically
     change based on the highest temperature.

              Chassis Fan Step Up
              Step up allows you to adjust how quickly the fan rotation speed increases,
              with level 0 being an instantaneous change in speed. The higher the level, the
              slower the change in speed, and may also result in less noise, but this will also
              cause slower heat dissipation.
              Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]
              Chassis Fan Step Down
              Step down allows you to adjust how quickly the fan rotation speed decreases,
              with level 0 being an instantaneous change in speed. The higher the level, the
              slower the change in speed, and may also result in less noise, but this will also
              cause slower heat dissipation.
              Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]
              Chassis Fan Speed Low Limit
              Allows you to set the lower speed limit for assigned fan/pump. A warning
              message will appear when the limit is reached; the warning message will not
              appear if [Ignore] is selected.
              Configuration options: [Ignore] [200 RPM] [300 RPM] [400 RPM] [500 RPM]
              [600 RPM]

98

NOTE: The following items appear only when Chassis Fan Profile is set to [Manual].

        Chassis Fan Point8 Temperature
        When the temperature source is lower than the temperature of P8, the duty
        cycle will be determined according to the P7-P8 and the temperature source.
        When the temperature source is higher than the temperature of P8, the fan will
        operate at the duty cycle of P8.
        Chassis Fan Point8 Duty Cycle (%)
        When the temperature source is lower than the temperature of P8, the duty
        cycle will be determined according to the P7-P8 and the temperature source.
        When the temperature source is higher than the temperature of P8, the fan will
        operate at the duty cycle of P8.
        Chassis Fan Point7 Temperature
        When the temperature source is lower than the temperature of P7, the duty
        cycle will be determined according to the P6-P7 and the temperature source.
        When the temperature source is higher than the temperature of P7, the duty
        cycle will be determined according to the P7-P8 and the temperature source.
        Chassis Fan Point7 Duty Cycle (%)
        When the temperature source is lower than the temperature of P7, the duty
        cycle will be determined according to the P6-P7 and the temperature source.
        When the temperature source is higher than the temperature of P7, the duty
        cycle will be determined according to the P7-P8 and the temperature source.
        Chassis Fan Point6 Temperature
        When the temperature source is lower than the temperature of P6, the duty
        cycle will be determined according to the P5-P6 and the temperature source.
        When the temperature source is higher than the temperature of P6, the duty
        cycle will be determined according to the P6-P7 and the temperature source.
        Chassis Fan Point6 Duty Cycle (%)
        When the temperature source is lower than the temperature of P6, the duty
        cycle will be determined according to the P5-P6 and the temperature source.
        When the temperature source is higher than the temperature of P6, the duty
        cycle will be determined according to the P6-P7 and the temperature source.
        Chassis Fan Point5 Temperature
        When the temperature source is lower than the temperature of P5, the duty
        cycle will be determined according to the P4-P5 and the temperature source.
        When the temperature source is higher than the temperature of P5, the duty
        cycle will be determined according to the P5-P6 and the temperature source.
        Chassis Fan Point5 Duty Cycle (%)
        When the temperature source is lower than the temperature of P5, the duty
        cycle will be determined according to the P4-P5 and the temperature source.
        When the temperature source is higher than the temperature of P5, the duty
        cycle will be determined according to the P5-P6 and the temperature source.
        Chassis Fan Point4 Temperature
        When the temperature source is lower than the temperature of P4, the duty
        cycle will be determined according to the P3-P4 and the temperature source.
        When the temperature source is higher than the temperature of P4, the duty
        cycle will be determined according to the P4-P5 and the temperature source.

                                                                                         99

             Chassis Fan Point4 Duty Cycle (%)
             When the temperature source is lower than the temperature of P4, the duty
             cycle will be determined according to the P3-P4 and the temperature source.
             When the temperature source is higher than the temperature of P4, the duty
             cycle will be determined according to the P4-P5 and the temperature source.
             Chassis Fan Point3 Temperature
             When the temperature source is lower than the temperature of P3, the duty
             cycle will be determined according to the P2-P3 and the temperature source.
             When the temperature source is higher than the temperature of P3, the duty
             cycle will be determined according to the P3-P4 and the temperature source.
             Chassis Fan Point3 Duty Cycle (%)
             When the temperature source is lower than the temperature of P3, the duty
             cycle will be determined according to the P2-P3 and the temperature source.
             When the temperature source is higher than the temperature of P3, the duty
             cycle will be determined according to the P3-P4 and the temperature source.
             Chassis Fan Point2 Temperature
             When the temperature source is lower than the temperature of P2, the duty
             cycle will be determined according to the P1-P2 and the temperature source.
             When the temperature source is higher than the temperature of P2, the duty
             cycle will be determined according to the P2-P3 and the temperature source.
             Chassis Fan Point2 Duty Cycle (%)
             When the temperature source is lower than the temperature of P2, the duty
             cycle will be determined according to the P1-P2 and the temperature source.
             When the temperature source is higher than the temperature of P2, the duty
             cycle will be determined according to the P2-P3 and the temperature source.
             Chassis Fan Point1 Temperature
             When the temperature source is lower than the temperature of P1, the fan will
             operate at the duty cycle of P1. When the temperature source is higher than
             the temperature of P1, the duty cycle will be determined according to the P1-
             P2 and the temperature source.
             Chassis Fan Point1 Duty Cycle (%)
             When the temperature source is lower than the temperature of P1, the fan will
             operate at the duty cycle of P1. When the temperature source is higher than
             the temperature of P1, the duty cycle will be determined according to the P1-
             P2 and the temperature source.
             Allow Fan Stop
             This function allows the fan to run at 0% duty cycle when the temperature of
             the source is dropped below the lower temperature.
             Configuration options: [Disabled] [Enabled]
      AIO Pump Q-Fan Control
      Allows you to set the AIO Pump operating mode.
      [Auto Detect]    Detects the type of installed fan/pump and automatically switches
                       the control modes.
      [DC Mode]        Enables the Q-Fan Control feature in DC mode for 3-pin fan/pump.
      [PWM Mode]       Enables the Q-Fan Control feature in PWM mode for 4-pin fan/
                       pump.

100

AIO Pump Profile
Allows you to set the appropriate performance level of the assigned fan/pump. When
selecting [Manual], we suggest raising your fan/pump duty to 100% if your CPU
temperature exceeds 75°C. Please be noted CPU performance will throttle due to
overheating with inefficient fan/pump duty.
Configuration options: [Standard] [Silent] [Turbo] [Full Speed] [Manual]

NOTE: The following items appear only when AIO Pump Profile is set to [Standard], [Silent],
[Turbo], or [Manual].

AIO Pump Q-Fan Source
The assigned fan/pump will be controlled according to the selected temperature
source.
Configuration options: [CPU] [CPU Package] [MotherBoard] [VRM] [T_Sensor] [Multiple
Sources]
AIO Pump Step Up
Step up allows you to adjust how quickly the fan rotation speed increases, with
level 0 being an instantaneous change in speed. The higher the level, the slower the
change in speed, and may also result in less noise, but this will also cause slower heat
dissipation.
Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]
AIO Pump Step Down
Step down allows you to adjust how quickly the fan rotation speed decreases, with
level 0 being an instantaneous change in speed. The higher the level, the slower the
change in speed, and may also result in less noise, but this will also cause slower heat
dissipation.
Configuration options: [Level 0] [Level 1] [Level 2] [Level 3] [Level 4] [Level 5]
AIO Pump Speed Low Limit
Allows you to set the lower speed limit for assigned fan/pump. A warning message
will appear when the limit is reached; the warning message will not appear if [Ignore]
is selected.
Configuration options: [Ignore] [200 RPM] [300 RPM] [400 RPM] [500 RPM] [600 RPM]

NOTE: The following items appear only when Chassis Fan Profile is set to [Manual].

AIO Pump Point8 Temperature
When the temperature source is lower than the temperature of P8, the duty cycle
will be determined according to the P7-P8 and the temperature source. When the
temperature source is higher than the temperature of P8, the fan will operate at the
duty cycle of P8.
AIO Pump Point8 Duty Cycle (%)
When the temperature source is lower than the temperature of P8, the duty cycle
will be determined according to the P7-P8 and the temperature source. When the
temperature source is higher than the temperature of P8, the fan will operate at the
duty cycle of P8.

                                                                                              101

      AIO Pump Point7 Temperature
      When the temperature source is lower than the temperature of P7, the duty cycle
      will be determined according to the P6-P7 and the temperature source. When the
      temperature source is higher than the temperature of P7, the duty cycle will be
      determined according to the P7-P8 and the temperature source.
      AIO Pump Point7 Duty Cycle (%)
      When the temperature source is lower than the temperature of P7, the duty cycle
      will be determined according to the P6-P7 and the temperature source. When the
      temperature source is higher than the temperature of P7, the duty cycle will be
      determined according to the P7-P8 and the temperature source.
      AIO Pump Point6 Temperature
      When the temperature source is lower than the temperature of P6, the duty cycle
      will be determined according to the P5-P6 and the temperature source. When the
      temperature source is higher than the temperature of P6, the duty cycle will be
      determined according to the P6-P7 and the temperature source.
      AIO Pump Point6 Duty Cycle (%)
      When the temperature source is lower than the temperature of P6, the duty cycle
      will be determined according to the P5-P6 and the temperature source. When the
      temperature source is higher than the temperature of P6, the duty cycle will be
      determined according to the P6-P7 and the temperature source.
      AIO Pump Point5 Temperature
      When the temperature source is lower than the temperature of P5, the duty cycle
      will be determined according to the P4-P5 and the temperature source. When the
      temperature source is higher than the temperature of P5, the duty cycle will be
      determined according to the P5-P6 and the temperature source.
      AIO Pump Point5 Duty Cycle (%)
      When the temperature source is lower than the temperature of P5, the duty cycle
      will be determined according to the P4-P5 and the temperature source. When the
      temperature source is higher than the temperature of P5, the duty cycle will be
      determined according to the P5-P6 and the temperature source.
      AIO Pump Point4 Temperature
      When the temperature source is lower than the temperature of P4, the duty cycle
      will be determined according to the P3-P4 and the temperature source. When the
      temperature source is higher than the temperature of P4, the duty cycle will be
      determined according to the P4-P5 and the temperature source.
      AIO Pump Point4 Duty Cycle (%)
      When the temperature source is lower than the temperature of P4, the duty cycle
      will be determined according to the P3-P4 and the temperature source. When the
      temperature source is higher than the temperature of P4, the duty cycle will be
      determined according to the P4-P5 and the temperature source.
      AIO Pump Point3 Temperature
      When the temperature source is lower than the temperature of P3, the duty cycle
      will be determined according to the P2-P3 and the temperature source. When the
      temperature source is higher than the temperature of P3, the duty cycle will be
      determined according to the P3-P4 and the temperature source.

102

      AIO Pump Point3 Duty Cycle (%)
      When the temperature source is lower than the temperature of P3, the duty cycle
      will be determined according to the P2-P3 and the temperature source. When the
      temperature source is higher than the temperature of P3, the duty cycle will be
      determined according to the P3-P4 and the temperature source.
      AIO Pump Point2 Temperature
      When the temperature source is lower than the temperature of P2, the duty cycle
      will be determined according to the P1-P2 and the temperature source. When the
      temperature source is higher than the temperature of P2, the duty cycle will be
      determined according to the P2-P3 and the temperature source.
      AIO Pump Point2 Duty Cycle (%)
      When the temperature source is lower than the temperature of P2, the duty cycle
      will be determined according to the P1-P2 and the temperature source. When the
      temperature source is higher than the temperature of P2, the duty cycle will be
      determined according to the P2-P3 and the temperature source.
      AIO Pump Point1 Temperature
      When the temperature source is lower than the temperature of P1, the fan will operate
      at the duty cycle of P1. When the temperature source is higher than the temperature
      of P1, the duty cycle will be determined according to the P1-P2 and the temperature
      source.
      AIO Pump Point1 Duty Cycle (%)
      When the temperature source is lower than the temperature of P1, the fan will operate
      at the duty cycle of P1. When the temperature source is higher than the temperature
      of P1, the duty cycle will be determined according to the P1-P2 and the temperature
      source.
Chassis Intrusion Detection Support
Set this item to [Enabled] to enable the chassis intrusion detection function.
Configuration options: [Enabled] [Disabled]

                                                                                              103

      8.           Boot menu
      The Boot menu items allow you to change the system boot options.

      CSM (Compatibility Support Module)
      Allows you to configure the CSM (Compatibility Support Module) items to fully support the
      various VGA, bootable devices and add-on devices for better compatibility.

            IMPORTANT! Launch CSM will be set to [Disabled] and cannot be configured when using the
            integrated graphics.

            Launch CSM
            [Enabled]         For better compatibility, enable the CSM to fully support the non-UEFI
                              driver add-on devices or the Windows® UEFI mode.
            [Disabled]        Disable the CSM to fully support the non-UEFI driver add-on devices
                              or the Windows® UEFI mode.

            NOTE: The following items appear only when Launch CSM is set to [Enabled].

            Boot Device Control
            Allows you to select the type of devices that you want to boot.
            Configuration options: [UEFI and Legacy OPROM] [Legacy OPROM only] [UEFI only]
            Boot from Network Devices
            Allows you to select the type of network devices that you want to launch.
            Configuration options: [Ignore] [Legacy only] [UEFI only]
            Boot from Storage Devices
            Allows you to select the type of storage devices that you want to launch.
            Configuration options: [Ignore] [Legacy only] [UEFI only]

104

      Boot from PCI-E/PCI Expansion Devices
      Allows you to select the type of PCI-E/PCI expansion devices that you want to launch.
      Configuration options: [Ignore] [Legacy only] [UEFI only]
Secure Boot
Allows you to configure the Windows® Secure Boot settings and manage its keys to protect
the system from unauthorized access and malwares during POST.
      OS Type
      [Windows UEFI Mode]         This item allows you to select your installed operating
                                  system. Execute the Microsoft® Secure Boot check. Only
                                  select this option when booting on Windows® UEFI mode
                                  or other Microsoft® Secure Boot compliant OS.
      [Other OS]                  Get the optimized function when booting on Windows®
                                  non-UEFI mode. Microsoft® Secure Boot only supports
                                  Windows® UEFI mode.

      NOTE: The Microsoft secure boot can only function properly on Windows UEFI mode.

      Secure Boot Mode
      This option allows you to select the Secure Boot mode from between Standard
      or Custom. In Custom mode, Secure Boot Policy variables can be configured by a
      physically present user without full authentication.
      Configuration options: [Standard] [Custom]

      NOTE: The following item appears only when Secure Boot Mode is set to [Custom].

      Key Management
      Install Default Secure Boot keys
      Allows you to immediately load the default Security Boot keys, Platform key (PK), Key-
      exchange Key (KEK), Signature database (db), and Revoked Signatures (dbx). When
      the default Secure boot keys are loaded, the PK state will change from Unloaded
      mode to loaded mode.
      Clear Secure Boot keys
      This item appears only when you load the default Secure Boot keys. Allows you to
      clear all default Secure Boot keys.
      Save all Secure Boot variables
      Allows you to save all secure boot keys to a USB storage device.
      PK Management
      The Platform Key (PK) locks and secures the firmware from any permissible changes.
      The system verifies the PK before your system enters the OS.
              Save To File
              Allows you to save the PK to a USB storage device.
              Set New key
              Allows you to load the downloaded PK from a USB storage device.

                                                                                               105

              Delete key
              Allows you to delete the PK from your system. Once the PK is deleted, all the
              system’s Secure Boot keys will not be active.
              Configuration options: [Yes] [No]

      IMPORTANT! The PK file must be formatted as a UEFI variable structure with time-based
      authenticated variable.

      KEK Management
      The KEK (Key-exchange Key or Key Enrollment Key) manages the Signature database
      (db) and Revoked Signature database (dbx).

      NOTE: Key-exchange Key (KEK) refers to Microsoft® Secure Boot Key-Enrollment Key (KEK).

              Save to file
              Allows you to save the KEK to a USB storage device.
              Set New key
              Allows you to load the downloaded KEK from a USB storage device.
              Append Key
              Allows you to load the additional KEK from a storage device for an additional
              db and dbx loaded management.
              Delete key
              Allows you to delete the KEK from your system.
              Configuration options: [Yes] [No]

      IMPORTANT! The KEK file must be formatted as a UEFI variable structure with time-based
      authenticated variable.

      DB Management
      The db (Authorized Signature database) lists the signers or images of UEFI
      applications, operating system loaders, and UEFI drivers that you can load on the
      single computer.
              Save to file
              Allows you to save the db to a USB storage device.
              Set New key
              Allows you to load the downloaded db from a USB storage device.
              Append Key
              Allows you to load the additional db from a storage device for an additional db
              and dbx loaded management.
              Delete key
              Allows you to delete the db file from your system.
              Configuration options: [Yes] [No]

      IMPORTANT! The db file must be formatted as a UEFI variable structure with time-based
      authenticated variable.

106

     DBX Management
     The dbx (Revoked Signature database) lists the forbidden images of db items that are
     no longer trusted and cannot be loaded.
              Save to file
              Allows you to save the dbx to a USB storage device.
              Set New key
              Allows you to load the downloaded dbx from a USB storage device.
              Append Key
              Allows you to load the additional dbx from a storage device for an additional
              db and dbx loaded management.
              Delete key
              Allows you to delete the dbx file from your system.
              Configuration options: [Yes] [No]

     IMPORTANT! The dbx file must be formatted as a UEFI variable structure with time-based
     authenticated variable.

Boot Configuration
     Fast Boot
     Allows you to enable or disable boot with initialization of a minimal set of devices
     required to launch active boot option. Has no effect for BBS boot options.
     Configuration options: [Disabled] [Enabled]

     NOTE: The following item appears only when Fast Boot is set to [Enabled].

     Next Boot after AC Power Loss
     [Normal Boot]	Returns to normal boot on the next boot after an AC power loss.
     [Fast Boot]	Accelerates the boot speed on the next boot after an AC power loss.
     Boot Logo Display
     [Auto]	Automatically adjust the boot logo size for Windows requirements.
     [Full Screen]      Maximize the boot logo size.
     [Disabled]         Hide the logo during POST.

     NOTE: The Following item appears only when Boot Logo Display is set to [Auto] or [Full Screen].

     Post Delay Time
     Allows you to select a desired additional POST waiting time to easily enter the BIOS
     Setup. You can only execute the POST delay time during normal boot.
     Configuration options: [0 sec] - [10 sec]

     IMPORTANT! This feature only works when set under normal boot.

                                                                                                       107

            NOTE: The following item appears only when Boot Logo Display is set to [Disabled].

            Post Report
            Allows you to select a desired POST report waiting time or until ESC is pressed.
            Configuration options: [1 sec] - [10 sec] [Until Press ESC]
            Boot up NumLock State
            Allows you to select the keyboard NumLock state.
            Configuration options: [On] [Off]
            Wait For ‘F1’ If Error
            Allows your system to wait for the <F1> key to be pressed when error occurs.
            Configuration options: [Disabled] [Enabled]
            Option ROM Messages
            [Force BIOS]     The Option ROM Messages will be shown during the POST.
            [Keep Current]   Only the ASUS logo will be shown during the POST.
            Interrupt 19 Capture
            Enable this item to allow the option ROMs to trap the interrupt 19.
            Configuration options: [Enabled] [Disabled]
            AMI Native NVMe Driver Support
            Allows you to enable or disable AMI Native NVMe driver.
            Configuration options: [Disabled] [Enabled]
            Setup Mode
            [Advanced Mode]	This item allows you to go to Advanced Mode of the BIOS after
                             POST.
            [EZ Mode]        This item allows you to go to EZ Mode of the BIOS after POST.
      Boot Option Priorities
      These items specify the boot device priority sequence from the available devices. The
      number of device items that appears on the screen depends on the number of devices
      installed in the system.

            IMPORTANT!
            • To access Windows® OS in Safe Mode, press <F8 > after POST (Windows® 8 not supported).
            • To select the boot device during system startup, press <F8> when ASUS Logo appears.

      Boot Override
      These item displays the available devices. The number of device items that appear on the
      screen depends on the number of devices installed in the system. Click an item to start
      booting from the selected device.

108

9.           Tool menu
The Tool menu items allow you to configure options for special functions. Select an item
then press <Enter> to display the submenu.

BIOS Image Rollback Support
[Enabled]	Support roll back your BIOS to a previous version, but this setting violates
            the NIST SP 800-147 requirement.
[Disabled]	Only support updating your BIOS to a newer version, and this setting
            meets the NIST SP 800-147 requirement.
Publish HII Resources
Configuration options: [Disabled] [Enabled]

      NOTE: The availability of the following items may vary according to your motherboard. Please refer
      to the BIOS of your motherboard for the actual settings and options.

Flexkey
[Reset]        Reboots the system.
[Aura On/Off]	Enable or Disable Aura LEDs. This setting does not sync with the BIOS/
               software option.
[DirectKey]    Boot directly into the BIOS.
Setup Animator
Allows you to enable or disable the Setup animator.
Configuration options: [Disabled] [Enabled]

Full HD Setup
Enable this feature to have a 1920x1080 resolution for BIOS Setup. Please note the feature
is supported when your monitor and graphics card are both 1080p or above. This feature
may be limited by the compatibility of your GPU and monitor pairing. When the BIOS detects
a Clear CMOS action, the BIOS will forcibly set the Full HD Setup to [Disabled] during this
boot process.
Configuration options: [Disabled] [Enabled]

                                                                                                           109

## 9.1 ASUS EZ Flash 3 Utility

      This item allows you to run ASUS EZ Flash 3. When you press <Enter>, a confirmation
      message appears. Use the left/right arrow key to select between [Yes] or [No], then press
      <Enter> to confirm your choice.

            NOTE: For more details, refer to section ASUS EZ Flash 3.

## 9.2 ASUS Secure Erase

      SSD speeds may lower over time as with any storage medium due to data processing.
      Secure Erase completely and safely cleans your SSD, restoring it to factory performance
      levels.
      To launch Secure Erase, click Tool > ASUS Secure Erase on the Advanced mode menu.

            NOTE:
            • The time to erase the contents of your SSD may take a while depending on its size. Do not turn
              off the system during the process.
            • Secure Erase is only supported on Intel SATA port. For more information about Intel SATA ports,
              refer to section Motherboard layout in your user manual.
            • Status definition:
               -	Frozen. The frozen state is the result of a BIOS protective measure. The BIOS guards drives
                  that do not have password protection by freezing them prior to booting. If the drive is frozen,
                  a power off or hard reset of your PC must be performed to proceed with the Secure Erase.
               -	Locked. SSDs might be locked if the Secure Erase process is either incomplete or was
                  stopped. This may be due to a third party software that uses a different password defined by
                  ASUS. You have to unlock the SSD in the software before proceeding with Secure Erase.

## 9.3 BIOS Q-Dashboard

      This item allows you to access the BIOS Q-Dashboard feature. This feature provides you with
      a perspective of the motherboard with vital components and connectors labeled for quick
      access.

            NOTE: For more details, refer to section Q-Dashboard.

110

## 9.4 ASUS User Profile

This item allows you to store or load multiple BIOS settings.

Load from Profile
Allows you to load the previous BIOS settings saved in the BIOS Flash. Key in the profile
number that saved your BIOS settings, press <Enter>, and then select Yes.

      NOTE:
      • DO NOT shut down or reset the system while updating the BIOS to prevent the system boot
        failure!
      • We recommend that you update the BIOS file only coming from the same memory/CPU
        configuration and BIOS version.

Profile Name
Allows you to key in a profile name.
Save to Profile
Allows you to save the current BIOS settings to the BIOS Flash, and create a profile. Key in a
profile number from one to eight, press <Enter>, and then select Yes.

Load/Save Profile from/to USB Drive
Allows you to load or save profile from your USB drive, load and save profile to your USB
drive.

## 9.5 ASUS SPD Information

This item allows you to view the DRAM SPD information.

## 9.6 ASUS MyHotkey

This menu allow you to configure Hotkeys.

      NOTE: The availability of this menu, as well as the settings and options may vary depending
      on your motherboard. Please refer to the BIOS of your motherboard for the actual settings and
      options.

Hotkey F3
Press <F3> to enter UEFI-USB or UEFI-HDD or UEFI-CDROM/DVDROM or UEFI-PXE or ASUS
AZ Flash 3 in POST.
Configuration options: [Disabled] [Boot from UEFI USB] [Boot from UEFI HDD] [Boot from
UEFI CDROM/DVDROM] [Boot from UEFI PXE] [Toggle ASUS EZ Flash 3]

      NOTE: Please make sure Network is enabled before AsusMyHotkey is set to Boot From UEFI PXE.
      (Advanced -> Network Stack Configuration -> Network Stack)

                                                                                                      111

      Hotkey F4
      Press F4 to enter UEFI-USB or UEFI-HDD or UEFI-CDROM/DVDROM or UEFI-PXE or ASUS EZ
      Flash 3 in POST.
      Configuration options: [Disabled] [Boot from UEFI USB] [Boot from UEFI HDD] [Boot from
      UEFI CDROM/DVDROM] [Boot from UEFI PXE] [Toggle ASUS EZ Flash 3]

            NOTE: Please make sure Network is enabled before AsusMyHotkey is set to Boot From UEFI PXE.
            (Advanced -> Network Stack Configuration -> Network Stack)

## 9.7 ASUS DriverHub

      This menu allow you to download and install the ASUS DriverHub app.

            NOTE: The availability of this menu, as well as the settings and options may vary depending
            on your motherboard. Please refer to the BIOS of your motherboard for the actual settings and
            options.

      Download & Install ASUS DriverHub app
      Allows you to enable DriverHub download process. DriverHub app can help you manage and
      download the latest drivers and utility updates for your motherboard.
      Configuration options: [Disabled] [Enabled]

112

10.          Exit menu
The Exit menu items allow you to load the optimal default values for the BIOS items, and
save or discard your changes to the BIOS items. You can access the EZ Mode from the Exit
menu.

Load Optimized Defaults
This option allows you to load the default values for each of the parameters on the Setup
menus. When you select this option or if you press <F5>, a confirmation window appears.
Select OK to load the default values.

Save Changes & Reset
Once you are finished making your selections, choose this option from the Exit menu to
ensure the values you selected are saved. When you select this option or if you press <F10>,
a confirmation window appears. Select OK to save changes and exit.

Discard Changes & Exit
This option allows you to exit the Setup program without saving your changes. When you
select this option or if you press <Esc>, a confirmation window appears. Select Yes to
discard changes and exit.

Launch EFI Shell from USB drives
This option allows you to attempt to launch the EFI Shell application (shellx64.efi) from one
of the available filesystem devices.

                                                                                                113

      11.           Updating BIOS
      The ASUS website publishes the latest BIOS versions to provide enhancements on system
      stability, compatibility,and performance. However, BIOS updating is potentially risky. If
      there is no problem using the current version of BIOS, DO NOT manually update the BIOS.
      Inappropriate BIOS updating may result to system’s failure to boot. Carefully follow the
      instructions in this chapter to update your BIOS when necessary.

             IMPORTANT! Visit http://www.asus.com to download the latest BIOS file for this motherboard.

      The following utilities allow you to manage and update the motherboard BIOS setup
      program.
      1.     ASUS EZ Flash 3: Updates the BIOS using a USB flash drive.
      2.     ASUS CrashFree BIOS 3: Restores the BIOS using a USB flash drive when the BIOS file
             fails or gets corrupted.

## 11.1 ASUS EZ Flash

      ASUS EZ Flash 3 allows you to download and update to the latest BIOS using a USB drive.

      To update the BIOS:
      1.     Insert the USB flash drive that contains the latest BIOS file to a USB port.
      2.     Enter the Advanced Mode of the BIOS setup program. Go to the Tool menu to select
             ASUS EZ Flash 3 Utility and press <Enter>.
      3.     Press Left arrow key to switch to the Drive field.
      4.     Press the Up/Down arrow keys to find the USB flash drive that contains the latest
             BIOS, and then press <Enter>.
      5.     Press Right arrow key to switch to the Folder field.
      6.     Press the Up/Down arrow keys to find the BIOS file, and then press <Enter> to perform
             the BIOS update process. Reboot the system when the update process is done.

114

## 11.2 ASUS CrashFree BIOS

The ASUS CrashFree BIOS 3 utility is an auto recovery tool that allows you to restore the
BIOS file when it fails or gets corrupted during the updating process. You can restore a
corrupted BIOS file using a USB flash drive that contains the BIOS file.

       IMPORANT! Make sure to download the latest BIOS file at https://www.asus.com/support/ and
       save it to a USB flash drive.

Recovering the BIOS
To recover the BIOS:
1.     Turn on the system.
2.     Insert the USB flash drive containing the BIOS file to the USB port.
3.     The utility automatically checks the devices for the BIOS file. When found, the utility
       reads the BIOS file and enters ASUS EZ Flash 3 automatically.
4.     The system requires you to enter BIOS Setup to recover the BIOS setting. To ensure
       system compatibility and stability, we recommend that you press <F5> to load default
       BIOS values.

       CAUTION! DO NOT shut down or reset the system while updating the BIOS! Doing so can cause
       system boot failure!

                                                                                                   115

116

