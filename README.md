# nophone
Replace phone by other devices where possible

## Why
<details><summary>1. A waste of money is a waste of life</summary><p>
  A phone sold for $100 in USA costs 1 month of the average income in Brazil. There is also a law that forbids banks of offering services to individuals without a phone app. This is very convenient for the 4 big banks, which can afford to have multiple development teams for Android and iOS instead of just one team for just one responsive website. The usual excuse is "security", of course. An individual, better described as a "slave", is forced to have a phone in order to access its own fake money at the bank, but such phone will stop working soon and the slave will need to buy a new one. How much can the slave save of its meaningless lifespan by being aware of all this?

  1. Baseline slave: 24 h/day, always fast-charging, unaware of the damage caused by trickle charging.

    100 / 2 $/year = 0.5 month/year = 0.5/12 month/month = 4.2% of slave lifespan

  2. Smart slave who bought an alarm clock, so the phone is kept off during sleep hours:
    
    (24-8) h/day + $5 for an alarm clock with 6-year lifespan + $1/year for the alkaline batteries.

    Each 72h of slave life only consume 48h of phone lifetime. So:
    New phone lifespan: 2 * 72/48 = 3 years
    Alarm clock: lasts 6 years, so it costs (5/6 + 1) $/year, being 1 $/year for the alkaline batteries

    (5/6 + 1) + 100/3 = 35.16 $/year = 0.3516/12 = 2.9 % of human lifespan

    The alarm clock is worth 1.2% of lifespan. 
    Equivalent to a huge discount of 1 - 2.9/4.2 = 31 % in the phone purchase.

  3. Expert slave: phone on only 06 h/day, most of the time in flight-mode, controlled slow charging at night with cooling, no trickle-charging and a custom debloated ROM like LineageOS.
    
    Change: the limiting factor is not the battery, but phone slowness. Software demands more and more whereas hardware wears down.

    The alarm clock is still the same, but the more complex setup adds both cost and extra longevity.

    Each 96h of slave life only consume 24h of phone life. So:
    New phone lifespan simply due to turning it off: 2 * 96/24 = 8 years
    Emerging extra phone lifespan added by the new setup (guess): +1 year
    Extra cost added by the new setup (guess): $80
    
    (5/6 + 1) + (100 + 80)/(8+1) $/year = $21.83/year = 0.2183/12 = 1.8% of human life

    Thus, first a simple clock saves 1.2% of life, but after that, saving 1.1% is much harder.
    The marginal gain decreases. This is realistic. Paretto's principle, Law of Diminishing Returns, etc.
    
    But it still equates to a whopping discount of 1 - 1.8/4.2 = 57 % in the phone purchase!
  
</p></details>

<details><summary>2. OPSEC and privacy, ultimately freedom</summary><p>
  A loose piece of information is worthless for the higher slaves trying to scam, tax, censor, harm or control the lower slave. The phone ties together all the data the slave generates there to its identity and location, which makes it a goldmine to the higher slaves. The more the lower slave replaces its phone with devices under its full control in its daily routine, the more the lower slave turns the goldmine into a garbage dump.
  
</p></details>

</p></details>

<details><summary>3. flexibility, ultimately peace</summary><p>
  The lower slave decides how his devices work, not a higher slave worried about ad revenue and whatnot.
  
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
6. The Rock64 will boot. Use the keyboard, mouse and monitor to configure whatever is needed. For example, the default keyboard layout and passwords, and hostname. Default password is `dietpi`. In step 4, X and XFCE were installed. They can be tested with the command `startx`.
7. Find the IP of the Rock64 within the network: <details><summary>some ways to do this. In this example, it is `192.168.15.18`</summary><p>
   a. logout (`exit`) and login again in DietPi (default password: `dietpi`). This will be shown in the HDMI monitor:
   ![r64_setup2](https://github.com/user-attachments/assets/f1d77ec0-e9ff-48ac-9c32-453e552ab420)
   
   b. in DietPi, issue the command `ip a`:
   ![r64_setup3](https://github.com/user-attachments/assets/72ae5736-bf85-4d41-a3de-64e13a989d73)

    </p></details>
8. Go back to the computer, open a terminal and issue `ssh dietpi@192.168.15.18`, replacing `192.168.15.18` by the actual IP found in step 7. Type your DietPi password (default: `dietpi`). This is remote SSH access, a much easier way to control the Rock64. The keyboard, mouse and HDMI monitor are no longer needed and can be disconnected from the Rock64.
9. Test the internet connection and update the system:
    ```
    sudo apt update
    sudo apt full-upgrade
    ```
    <details><summary>Why the internet connection matters even if the slave will not use a web app</summary><p>
    
    A computer has an RTC clock powered by an independent battery, this is why its clock does not reset at every boot. An SBC like the Rock64 does not have this. DietPi corrects the time at every boot by syncing the system clock to an NTP server over the internet. So, without internet, the clock will be wrong. That will prevent HTTPS connections, but the error messages will not indicate the problem is the clock. To avoid this snowball of stupidity, it is easier to make sure the internet always works than to install an RTC module. Moreover, the setup for the internet is the same for SSH access, which is the best solution to interface with an SBC anyway.
   
    </p></details>
    
11. Without `sftp-server`, `scp` won't work to transfer files between the computer and Rock64. So install that package: `sudo apt install openssh-sftp-server`
12. 


