# nophone
Replace phone by other devices where possible

## Why
<details><summary>1. A waste of money is a waste of life</summary><p>
  The average thirdworldian slave must work 1 month to buy a phone which is sold at $100 in USA. The slave is also forced to have a phone to be able to access the fake money it has in the bank. The battery is designed to fail first. If the slave sleeps 8h/day and does not use the phone to wake up in the next morning, said phone can be turned off without charging at night. This will delay the need to buy a new phone. How much is that worth?

  1. Baseline slave: 24 h/day, always fast-charging, unaware of the damage caused by trickle charging.

    100 / 2 $/year = 0.5 month/year = 0.5/12 month/month = 4.2% of slave life

  2. Smart slave who bought an alarm clock: (24-8) h/day + $5 for an alarm clock with 6-year lifespan + $1/year for the alkaline batteries.

    Each 72h of slave life only consume 48h of phone life. So:
    New durability: 2 * 72/48 = 3 years
    Alarm clock: lasts 6 years, so it costs (5/6 + 1) $/year, being 1 $/year for the alkaline batteries

    (5/6 + 1) + 100/3 = 35.16 $/year = 0.3516/12 = 2.9 % of human life

    The alarm clock is worth 1.2% of life. 
    Equivalent to a huge discount of 1 - 2.9/4.2 = 31 % in the phone purchase.

  3. Expert: 06 h/day, most of the time in flight-mode, controlled slow charging at night with cooling, no trickle-charging and a custom debloated ROM like LineageOS. The limiting factor is no longer the battery life, but the slowness of the phone as the software gets more and more complex over time and the hardware wears down physically. The alarm clock is the same, but now there is both extra cost and extra longevity besides the baseline of phone off-time.

    Each 96h of slave life only consume 24h of phone life. So:
    New baseline durability: 2 * 96/24 = 8 years
    Emerging extra longevity (guess): +1 year
    Extra cost due to all the extra complexity (guess): $80
    
    (5/6 + 1) + (100 + 80)/(8+1) $/year = $21.83/year = 0.2183/12 = 1.8% of human life

    Thus, first a simple clock saves 1.2% of life, but after that, saving 1.1% is much harder.
    The marginal gain decreases. This is realistic. Paretto's principle, Law of Diminishing Returns, etc.
    
    But it is still a whopping discount of 1 - 1.8/4.2 = 57 % in the phone purchase!
  
</p></details>

<details><summary>2. OPSEC and privacy, ultimately freedom</summary><p>
  A loose piece of information is worthless for people trying to scam, tax, censor, harm or control the slave. The phone ties together all the data the slave generates there to its identity and location, which makes it a goldmine to these people. The more the slave replaces its phone with devices under its full control in its daily routine, the more the slave turns the goldmine into a garbage dump.
  
</p></details>

</p></details>

<details><summary>3. flexibility, ultimately peace</summary><p>
  The slave decides how his devices work, not a designer worried about ad revenue and whatnot.
  
</p></details>

## How
### Parts
1. A computer with MX Linux, a USB microSD card reader/writter and a wired Ethernet RJ45 connection to a router (**recommended: admin access. Routers may block devices or not display info like their IP otherwise**)
2. An old Rock64 2gb board (dead platform. Was never used)
3. A 5V 3A power supply with a...<details><summary>strange connector:</summary><p>
    ```
    Spec: 3.5mm outer diameter, 1.35mm inner diameter.
    Thridworldian slaves don't understand the concept of specs.
    They describe this sometimes as 3.4x1.4 or even Mini P4.
    This is a thirdworldian example of correct spec:
    ```
    https://produto.mercadolivre.com.br/MLB-3729696460-fonte-carregador-5v-3a-notebook-positivo-motion-cruy-q464c--_JM
    </p></details>
4. A 32 gb microSD card
5. An extra RJ45 Ethernet cable to connect the Rock64 to the same network as the computer
6. A keyboard, mouse and HDMI monitor to do the first setup of the Rock64
7. An old set of stereo speakers (rarely used many years ago)
8. Some pushbuttons, resistors, wires

### Rock64 setup
1. Download DietPi image: https://dietpi.com/#downloadinfo -> select PINE64 -> select ROCK64
2. Download Balena Etcher: https://etcher.balena.io/
3. Use Balena to flash the DietPi Image into the SD card
4. Edit the file `/boot/dietpi.txt`: <details><summary>click to expand</summary><p>
    ```
    # this is a comment. Valid timezone strings: https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
    AUTO_SETUP_TIMEZONE=Europe/London
    # unfortunately, the setting below does not work. Keyboard layout must be changed interactively after install...
    # AUTO_SETUP_KEYBOARD_LAYOUT=gb
    # automated install
    AUTO_SETUP_AUTOMATED=1
    # X server and XFCE
    AUTO_SETUP_INSTALL_SOFTWARE_ID=25
    # LightDM login mask
    AUTO_SETUP_AUTOSTART_TARGET_INDEX=16
    # xrdp
    AUTO_SETUP_INSTALL_SOFTWARE_ID=29
    # disable survey and don't ask about it. If the slave wants, the slave can re-enable this later.
    SURVEY_OPTED_IN=0
    ```
    </p></details>
5. Remove the SD from the computer and put it in the Rock64. Connect the keyboard, mouse, HDMI monitor and RJ45 cable. Only then connect the power supply
6. The Rock64 will boot. Use the keyboard, mouse and monitor to configure whatever is needed. For example, the default keyboard layout and passwords, and hostname.
7. Find the IP of the Rock64 within the network. After you login, this info is shown in the HDMI monitor. You can also use a command like `ip a`. This will also be shown in the router admin page.

    

8. 
